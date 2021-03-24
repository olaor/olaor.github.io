---
title: Getting yum on RHEL to work with a proxy over ssh
author: oo
---

# Getting yum on RHEL to work with a proxy over ssh

Ever had a machine on a very locked down network where the network
admins will not give you access to RedHat network for installing and
updating packages with yum? If so, it sucks to be you. But do not
despair, SSH to the rescue!

First, make sure you have an available http/https proxy. Setting up
one of those is beyond the scope of this little reminder-to-self, so
JFGI. Then, connect to the remote host with this command:

> ssh -R 8080:&lt;Adress to proxy server&gt;:&lt;proxy server port&gt; root@remotehost

Then, on remotehost, make sure [/etc/sysconfig/rhn/up2date contains
the following (if your proxy needs authentication you will need
additional configuration, that file is properly documented so just
dive into it.):]

> grep -e enableProxy= -e httpProxy= /etc/sysconfig/rhn/up2date
>
> [enableProxy=1]
>
> [httpProxy=localhost:8080]

Now you can run yum to your hearts content.
