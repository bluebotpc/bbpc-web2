---
layout: posts
title:  "Experience OpenLiteSpeed"
date:   2023-09-21 08:00:00 -0700
categories: technology
---
Howdy Friends! I would like to take you on a journey with me. Today I will be tuning the underlying web server that is running this very WordPress application. My hopes is to reduce overall CPU load as well as get experience with the more advanced settings.

OpenLiteSpeed is an open-source project hosted on GitHub under the GPLv3 license.

## HTTP Servers and History

Apache is the OG web server. Released in 1993; its daemon name within Linux is httpd. It essentially serves HTML file over the HTTP protocol using port 80. To accomplish this, each concurrent connection spins up a thread on the CPU. Eventually these threads can consume all the compute resources available.

Next comes NGINX. Released in 2003 it was originally a proxy software that has evolved into a full fledged HTTP server. Instead of a process/thread heavy design, they created an event-driven method. This allows a single thread to remain open at all times and serving HTTP requests until enough load generates an additional thread. This allows NGINX to serve more customers with fewer resources.

Apache Documentation
NGINX Documentation

## More About OpenLiteSpeed

- BlackIkeEagles Blog - Benchmarking Results

I have linked an article that folks should read. It is a well written and in-depth benchmark comparing Apache, NGINX, and OpenLiteSpeed. My takeaway from this article is that while OpenLiteSpeed is event-driven and very quick to respond to socket requests, it has a much heavier memory footprint than its nearest competitor. It is not clear if this increased memory usage is due to the underlying memory GUI or an architecture decision considering this is written in C++.

However even with this caveat, my $5/month Nanode has been running this site and combo just fine for months with satisfactory performance.

## Web Server Tuning & Additional Setup

Once you have accessed the WebAdmin, go ahead and navigate into Server Configuration. From here I went ahead and configured...

- Server Name
- Disable Geo Location Lookup
- Certificate Administrator Email

By declaring the Server Name here in the Application and within /etc/hosts file within the OS, we can reduce INFO logs regarding mismatched hostnames.

Disabling Geo Location will reduce CPU load during concurrent connections.

If you navigate over towards the App Server tab, you can configure and tweak the environment variables for underlying applications such as NodeJS, Ruby, and PythonWSGI.

Geekflare - Install Ruby on Ubuntu
NodeJS Documentation - Install NodeJS

Once I had installed the listed packages above, I went ahead and used the "which" command to identify the $PATH for these applications. I left most other settings as their defaults. They are rather sane.
