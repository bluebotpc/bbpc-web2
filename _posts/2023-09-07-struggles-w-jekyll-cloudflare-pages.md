---
layout: posts
title:  "Struggles with Jekyll and Cloudflare Pages"
date:   2023-08-11 08:00:00 -0700
categories: technology
---
## TL;DR Solution

- Open your Application
- Navigate to Settings
- Click Builds & Deployments
- Change Build System Version from 2 to 1

## My Introduction to the Issue

Over the last few years working for Nordstrom, I've grown more into a lightweight Engineering role and it has been very interesting. I've recently begun to use Git for version control on my scripts and tracking our Ansible and Terraform IaC templates.

This got me interested in using GitHub at home for tracking some basic python3, or HTML5 that I might write. As I spent time on GitHub, of course I checked out GitHub Pages. Played around enough to install Ruby and Jekyll onto my PC and utilize it to build on a few templates. However GitHub Pages doesn't allow commercial usage of their Pages platform and I would want to do this semi-commercially. Cloudflare Free Tier however provides unlimited repos given less than 500 commits a month. I can keep my commits lower than 500 a month.

For the last 6 months my Business has ran from Cloudflare Pages that I had migrated from GitHub using the Cloudflare Documentation here. Everything in this pipeline had been fine and working. Today was a different story when trying to create a new repo.

## The Error Message

```bash
11:46:50.029 Executing user command: jekyll build
11:46:51.872 /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.19/lib/bundler/runtime.rb:304:in `check_for_activated_spec!': You have already activated i18n 1.14.1, but your Gemfile requires i18n 0.9.5. Prepending `bundle exec` to your command may solve this. (Gem::LoadError)
11:46:51.873  from /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.19/lib/bundler/runtime.rb:25:in `block in setup'
11:46:51.873  from /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.19/lib/bundler/spec_set.rb:165:in `each'
11:46:51.873  from /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.19/lib/bundler/spec_set.rb:165:in `each'
11:46:51.873  from /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.19/lib/bundler/runtime.rb:24:in `map'
11:46:51.874  from /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.19/lib/bundler/runtime.rb:24:in `setup'
11:46:51.874  from /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.19/lib/bundler.rb:162:in `setup'
11:46:51.874  from /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/jekyll-4.3.2/lib/jekyll/plugin_manager.rb:52:in `require_from_bundler'
11:46:51.874  from /opt/buildhome/.asdf/installs/ruby/3.2.2/lib/ruby/gems/3.2.0/gems/jekyll-4.3.2/exe/jekyll:11:in `<top (required)>'
11:46:51.874  from /opt/buildhome/.asdf/installs/ruby/3.2.2/bin/jekyll:25:in `load'
11:46:51.875  from /opt/buildhome/.asdf/installs/ruby/3.2.2/bin/jekyll:25:in `<main>'
11:46:51.879 Failed: Error while executing user command. Exited with error code: 1
11:46:51.889 Failed: build command exited with code: 1
11:46:53.035 Failed: error occurred while running build command
```

I Googled that second line every which way I could. I added webrick, I recreated the Gemfile over and over like a mad man. Finally, I found it... This THREAD showing that the current version of Liquid and the current version of Ruby are broken compatibility wise. Nothing I can do..... Until I found this sneaky setting....

Changing from Version 2 to Version 1 resolved my issues entirely.

Version 1 runs a Ubuntu 20.04 LTS runner with the older Ruby version 2.7.1 - Using this runner I am able to successfully deploy my GitHub Pages projects onto Cloudflare Pages.

Version 2 run s a Ubuntu 22.04 LTS runner with the newer Ruby version 3.2.2 - Unfortunately the upstream creators of Liquid made core code changes between v4 and the new v5. Now many Jekyll gems based on Liquid are broken.
