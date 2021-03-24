---
title: RSS action daemon
author: oo
---

# RSS action daemon

I hang out at an IRC channel where this guy agonyzer started talking
about wanting a rss feed reader that could do configurable actions on
feed items.  But then he claimed to suck at programming... 

So i made
RSS Daemon. It uses a standard .cfg file to specify RSS feeds or pipes
that provide rss feeds, what element in the feed item to look for,
what to look for in that item, and what to do if you find what you
look for. The RSS daemon will reload it's configuration if you change
the config file. The config file is as easy as
rssdaemon\_example.cfg - just read it and rename it to rssdaemon.cfg .
There are comments in the file. 

Oh, yes - rssdaemon.py --dump-only
will give you the first element of every configured feed with the name
of each element. VERY useful. 

If there are any problems, patches, feature requests or questions -
please email me at ola-rssdaemon \[at\] ormset.no Alright, now [press
this link and download rssdaemon](http://ormset.no/~oo/src/rssdaemon-0.1.tar.gz)

### EDIT 2021

Updated version can be found [here](/2011/08/22/RSS-Action-Daemon-02.html)

