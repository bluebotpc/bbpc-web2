---
layout: posts
title:  "PiAware - One Month of Ownership"
date:   2021-06-07 08:00:00 -0700
categories: raspi_pi
---
## Summary of My One Month Experience

Over the last month, I have made it up into the top 3,000 PiAware sites out of approximately 24,000 and growing!
On a busy day Raspberry Pi 3B+ runs at about 35%-60% CPU utilization, but can easily spike to 100% for short periods of time during updates.
In the coming weeks, I can see myself upgrading to a Raspberry Pi 4 - I have a strong feeling the 4x compute power & 16x Memory could make this smoother and MAYBE just maybe increase my range.

The antenna I used has a decent range of about 50 nautical miles to the West and to the East. My Western range is handicapped by the 14,000 foot mountains that aren't that far away, and my apartment building interferes with my Eastern range. However going North and South I can see some planes as far as 200 nautical miles. All of this with the DEFAULT configuration. No tweaks at all! **Default SSH Login Info is located lower in this Blog Post under "Control From Anywhere"**

## The Back Story

Early in my relationship with my wife, we would go out back behind the Denver International Airport (KDEN) and we would sit and watch the planes coming into land. We would spend entire afternoons munching on some tacos keeping track of how many planes were lined up to land. Fast forward 7 years and I have found my self living in an area of town with a ton of air traffic.

Every time I was taking a break from my work, I found myself stepping out onto the patio with a pair of cheap binoculars trying to match their N-number while watching a "Big Screen" view on FlightAware's website and listening to the local ATC from LiveATC - My problem was the feed was always delayed a bit, sometimes by a few minutes; which made it difficult sometimes to keep track of the airplanes with the LiveATC feed. So the solution to my issues was to somehow get an Enterprise account on FlightAware and it turns out this was pretty easy for me.

I am absolutely no expert on what all you can do with a PiAware but I found FlightAware's Official Build Guide Here! The big take away for me was all I needed was a Raspberry Pi 3B+ and a few small things off the eBay or Amazon. Luckily I already had a Raspberry Pi 3B+ that I wasn't using so I only had to pick up some small things, here is exactly what I bought...

### The Shopping List

- Raspberry Pi 3B+
- Official FlightAware USB Receiver
- Official 1090MHz Antenna Filter
- 1090MHz Antenna

Once all the parts arrived and I began install, I was able to quickly appreciate how much effort the developers at FlightAware put into making this about as Plug-N-Play as possible. I used the FlightAware provided Raspberry Pi Image called SkyAware 5.0 and was able to connect this to my home wireless network the same as I had done any previous Raspberry Pi.
Then I just followed FlightAware's guide to claim my PiAware which was super easy! All I had to do was wait about 3 minutes after my PiAware booted up for the first time, and then click the link that appeared on my FlightAware dashboard.

### The In-House view

Just having this device streaming data up to FlightAware gives you access to Real-Time data via an Enterprise grade account with them. This allows you to watch flights all across the world, but what if you only want to see what your equipment can see? Well all you need to do is navigate to PiAware's local LAN IP address followed up :8080.

### Control from Anywhere

One of my favorite things about PiAware is that I wouldn't need to open up my port 22. Instead FlightAware has a way for you to securely update, reboot, and reload the required services from your dashboard!

Default SSH Username: ```piaware```
Default SSH Password: ```flightaware```
