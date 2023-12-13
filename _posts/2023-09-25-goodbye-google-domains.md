---
layout: posts
title:  "Goodbye Google Domains"
date:   2023-09-25 08:30:00 -0700
categories: technology
---
Google Domains was the first Registrar I had ever used. They had an easy to use API, near market pricing, and an overall "clean" user experience that you would expect from a Google product. However on September 7th 2023 Squarespace and Google announced that the acquisition was completed and you can no longer purchase a domain via Google.

This article from The Verge was released on June 16th and was where I originally heard the news. I do not exactly have any problems with Squarespace as a company but I do not intend on using their services. This means I would need to migrate my 5 personally owned Domains elsewhere.

## Two for Cloudflare

I moved my two business domains over to Cloudflare. I use their "Pages" platform to an extent and I also enjoy utilizing their Zero-Trust Tunnels application for my Raspberry Pi projects.

To be completely honest, when you utilize the Free Tier of Cloudflare CDN, you are provided two authoritative name-servers to point your domain too. Owns, and Bethany. I figured that if I purchased a domain/performed a transfer I would gain access to a higher quality "pool" of authoritative name-servers. I also cannot seem to point my domain name servers to another vendor. That is a conversation for another day.

Either way, putting my mild disappointment aside the experience has been perfectly acceptable.

## PorkBun

PorkBun has really funny piggy branding. I heard a bunch of good things about them on the internet. Sometimes I purposely ignore the advise of the internet but for some reason I took the bait.

I am not an entirely huge fan of their broad TLD advertising. I guess they are in the business of selling domains, but come on man. Who wants to buy some of these "dot camera" or "dot sales"  I mean really!

However they a decent user experience, affordable pricing for the quality TLDs like .com and .net. They also have an API that can interacted with via Python. They also have some great documentation for utilizing their platform. If they continue to keep renewal pricing reasonable and below $13.00 I will continue to utilize them.

## Conclusion

If I were to have the opportunity to go back and migrate again, I would put all of my domains inside the PorkBun basket. I would continue to utilize Cloudflare but by the way of custom authoritative name servers. This would prevent me from being locked to Cloudflare like I currently feel.
