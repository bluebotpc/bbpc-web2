---
layout: posts
title:  "Ditching WordPress"
date:   2023-12-15 08:00:00 -0600
categories: technology
---
A quick Google search indicates that approximately 43% of the public facing internet is running [WordPress](https://wordpress.org/). WordPress is a popular free and open-source[PHP](https://www.php.net/) application that operates as a Content Management System (CMS), an HTML templating software, and provides an extensible platform for developers to write server-side or _"backend"_ code.

The Content Management System and HTML Templating features go hand in hand. Together they create an overarching "Web Page Builder". By utilizing "Themes" - This Web Page Builder provides users an easy process for creating and managing pages, blog posts, media, forms, and more. All while maintaining consistent design across the site. These Themes are a huge aspect of the WordPress platform. The WordPress Organization releases a new "default" theme every year; additionally it is common to purchase a pre-built Theme from a company or a Web Designer.

## Major Drawbacks

WordPress requires a database to operate. This database keeps usernames, passwords, post information, and more. While the presence of a database is a critical requirement for the operation of an online web-store; I do not sell anything on my personal website. Furthermore, this website is running on a $5/mo [Nanode](https://www.linode.com/pricing/). My available resources are rather limited. While the underlying AMD EYPC 7713 (Milan Series) is a database-crunching monster, I only have 1GB of system memory available. The operation of any database consumes valuable resources.

This web server is exposed over TCP ports 80 and 443. Port 80 listens for HTTP requests while Port 443 listens for HTTPS requests. When folks ask me about port forwarding, I always advise that port forwarding itself is not dangerous. Most times, it is an out-right necessity to operate a server. The port is only as "exposed" as the listening Application. However I would estimate most WordPress-based websites use 10+ plugins from 10+ unique developers. This introduces a wide-range of code quality. This **increases attack vectors** which inherently **increases risk of data loss**.

My final gripe is with the PHP-based templating function. While it helps retains artistic consistency and provides a graphical web page builder; it decreases your ability to effectively leverage a Content Delivery Network (CDN). When a visitor loads a webpage to view, it starts an underlying PHP process to "build", "serve", and "cache" the page. Typically after a small period of time, the underlying server (CPU/Memory/Storage) needs to rebuild the pages. This is because you are serving _.php_ files. (Seen in the URL) This can result in decreased overall capacity and an in increase in page load times.

## Personal Requirements

Until Chirstmas Day 2023, my website was running WordPress. It looked really good, and it would load quick enough. My disappointment was always in the Themes. If the Theme is free, it has watermarks and limited customization. Otherwise the Themes come with heafty yearly fee. As an experinced Techhy, I was no longer satisfied with the watermarks, ugly text colors, and I sure wasn't going to pay a yearly fee. I did some tinkering with GitHub Pages and CloudFlare Pages. These exposed me to [JekyllRB](https://jekyllrb.com/) and [Hugo](https://gohugo.io/). I've found **JekyllRB** to be my preference.

By leveraging JekyllRB, I can easily convert [Markdown](https://www.markdownguide.org/) into plain ol' HTML5 and CSS3. This means that I only need to "build" the site one-time. Now the underlying server only needs to "serve" the requested webpage HTML file. This greatly increases the overall capacity and reduces attack vectors by removing the reachability of a local or remote SQL database. This provides me the **freedom** to manipulate any aspect of my website as I wish, all without paying anyone.

### Change Procedure

- Create Snapshot of my Linode.
- Install GitHub CLI and Authenticate it.
- Sync GitHub Repo into a folder in my Home Directory.
- Install JekyllRB and pre-requisites.
- Build the Site using Jekyll into my Homr Directory.
- Empty the /var/www/html folder.
- Move new content into /var/www/html/.
- Fix file permissions in /var/www/html/.
- Reload Web Server processes.
- Clear CDN cache.
- Restart the underlying Server.
- Verify functionallity on Home PC, Cell Phone, and PageSpeed Insights.
