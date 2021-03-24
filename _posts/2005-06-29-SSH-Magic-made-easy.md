---
title: SSH Magic made easy
author: oo
---

# SSH Magic made easy

**Semi-VPN through a ssh SOCKS4 proxy**
---------------------------------------

VPN setup in Linux is, depending on your distro, a time-consuming and technically challenging task often involving kernel patching and a whole lot of
setup-file-editing. With ssh and [tsocks](http://tsocks.sourceforge.net/) much of the same functionality may be achieved.

### Overview

What basically happens is that you open an encrypted tunnel to a Linux/UNIX machine connected to the remote network where the services you wish to use
are available. All network traffic requested by your programs are routed through that encrypted channel so that programs on your local desktop
network-wise appears to be running at the remote Linux/UNIX machine.

### Requirements

You will need:

-   A \*nix server which allows remote logins with ssh on some port (usually port 22)
-   The firewall must allow traffic to the ssh port on the \*nix machine
-   ssh client-side software. In Debian all you have to write is, as root:

    `apt-get install ssh`

-   the tsocks library and user software. Again, in Debian, as root:

    `apt-get install tsocks`

### Topology

Our network setup looks like this.

![Network setup](https://ormset.no/img/network.png)

### Setup tsocks

Edit the file */etc/tsocks.conf*. The minimum content may look like this:

          # Our local network
          local = 192.168.0.0/255.255.255.0
          local = 127.0.0.0/255.255.255.0
          # The SOCKS4 proxy servers IP address - the desktop box.
          server = 127.0.0.1
          # The SOCKS4 server will be running on port 7667      
          server_port = 7667 
          # We use SOCKS4, not 5
          server_type = 4

### Usage

Ok, we have installed everything and set up tsocks. Next we need to make ssh behave like a SOCKS4 proxy. Your username on `server` is `user`, by the
way :)

Now, in a terminal window write the following:

`ssh -D 7667 user@server`

Typicaly, this is what will happen:

         user@desktop% ssh -D 7667 user@server    
         user@server's password: 
         Last login: Sat Jan 17 16:59:51 2004
         [ user@server ~ ]%

You are now logged in as normal to `server`. However, in addition to just logging in your ssh session acts as an SOCKS4 proxy. Neat?

To test the setup open a new terminal window. In this example I use Mozilla as web browser, but any other one will do. Make sure no instances of
mozilla is running. We will try accessing the web page on the web server `webserver`, which is not reachable from the Internet, only from the Remote
network where `server` also resides:

          user@desktop% mozilla

Try accessing the url `http://webserver`. This should fail. Now try this:


          user@desktop% tsocks mozilla

And what do you know! You may now view an internal webpage, `http://webserver`, from the Remote network! Congratulations, it worked :)

### Automatic startup and semi-vpn

In order to make all your applications use the proxy for network traffic going to non-local sites we need to edit your X-server login file, most
commonly `~/.xsession`, a bit so that all settings are loaded at startup. Here we need a helper application called ssh-askpass:

          % su -
          $ apt-get install ssh-askpass

ssh-askpass enables ssh to pop up an graphical window to ask for our password.

Now make your `.xsession` file look like this:

          #!/bin/sh

          # Where SSH may find ssh-askpass
          export SSH_ASKPASS=/usr/lib/ssh/x11-ssh-askpass

          # Start the ssh SOCKS4 proxy - but do not open an login shell.
          ssh -N -D 7667 user@server &

          # Make all applications use the tsocks library
          # It is important to do this _after_ we open the ssh connection..
          export LD_PRELOAD=/usr/lib/libtsocks.so

          # Start your window manager - I use gnome sometimes
          gnome-session
