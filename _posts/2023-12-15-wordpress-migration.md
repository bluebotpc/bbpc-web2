---
layout: posts
title:  "Ditching WordPress"
date:   2023-12-15 08:00:00 -0600
categories: technology
---
WordPress is an exceptionally popular [PHP](https://www.php.net/) application that operates as a Content Management System (CMS), an HTML/PHP templating software, and provides an extensible platform. Being PHP-based, it allows an easy method for performing backend server processing such as reading and writing to a database. This is a major requirement for Web Stores. Based on all these features, a quick Google search indicates that approximately 43% of the public facing internet has some flavour of WordPress running in the backend. Until Chistmas Day 2023, my website was also running WordPress.

## Lets Talk Requirements

When I originally deployed my WordPress blog I did not have a defined end goal other than check out the Linode One-Click installer. After a year of playing with WordPress themes, plugins, and database admin tools; I have determined that WordPress has more software bloat than I require.

## Benefits for My Website

WordPress is an open-source project, and given the nature of open-source and the random nature of plugins; it 

### Change Procedure Followed

- Create Snapshot of my Linode
- Install GitHub CLI and Authenticate
- Install JekyllRB and pre-requisites.
- Create a new Site Directory

