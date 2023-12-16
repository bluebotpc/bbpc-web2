---
layout: posts
title:  "Setting the Timezone on your Raspberry Pi 4"
date:   2021-03-24 08:00:00 -0700
categories: raspi_pi
---
Hello everyone! In this post I will be walking you through how to update the timezone on your newly imaged Raspberry Pi. While this guide is specifically aimed at Raspberry Pi users, these commands will work in both the Ubuntu Desktop GUI and Ubuntu Server CLI as well as on many other Debian based Operating Systems. If you prefer a YouTube tutorial, check out mine below!

{% include video id="mHVodqxJGbU" provider="youtube" %}

First we want to see what our system time is, we can do this with...

```timedatectl``

The output above is what you typically get after a clean installation of RaspberryPi OS or Ubuntu Server 20.04. You can see your local system time as well as Universal Time, the default Timezone.
Now to get a list of all our available options, we want to run...

```timedatectl list-timezones```

The list of time-zones is pretty long. Just hit space bar a couple of times to see the full list. If you found your entry and want to quit out of the menu on screen, just hit "q".

Then we will take note of which timezone we would like to use! Now to set the timezone we will want to use elevated privileges...

```sudo timedatectl set-timezone America/Denver```

Now that we have selected America/Denver the original timedatectl command will generate the output below... We can see we have selected Mountain Standard selected.
