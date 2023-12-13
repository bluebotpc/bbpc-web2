---
layout: posts
title:  "Using A Raspberry Pi Zero To Host a VPN Server"
date:   2021-11-13 08:00:00 -0700
categories: raspi_pi
---
**Techies that are here for the meat and potatoes, please go to the next section! :)** Thanks to countless YouTubers' and a handful of VPN Providers such as NordVPN, Private Internet Access (PIA), or Someone Else, having a VPN for personal use is all the rage these days. Now we must answer the question, what does VPN stand for? What does a VPN do? Why would I host my own VPN?

A VPN or Virtual Private Network consists of at least two distinct parts. First is a device known as a Server. This server hosts a service for the second device, known as a Client. Together they are part of a Client/Server environment which is a core concept of modern networking.

A VPN allows a user to access a network and its localized resources from just about anywhere. If you work remotely or work from home, you may connect to a VPN so that you can access internal resources such as a networked storage drive or maybe an in-office application server. A consumer however uses a VPN in a slightly different manner; Let me explain...

As an American citizen sitting in your house, you may be using a VPN Provider to access Netflix content that is region restricted. For example, The Office is no longer visible in the United States but if you turn on your VPN and connect to a Canadian Server, tada! You can watch The Office. But how does that work???

When you connect to a VPN, your device (the client) creates a secured connection known as a handshake with a server. This handshake is an agreement to let each other know that if you suspect someone or something is sniffing the data to terminate the connection immediately. Another part of this handshake is potentially an agreement on an encryption algorithm, but the details on how encryption are a whole separate rabbit hole not meant for this document.

This handshake your client and the VPN server creates also establishes whats known as a Tunnel. If you are a techie interested in networking, this is known as a Layer 2 Tunneling Protocol or L2TP for short. Now what does a Layer 2 Tunneling Protocol do? Well you may want to familiarize yourself with the OSI Model (Open Systems Interconnection Model) Understanding the OSI model is fundamental to learning how networks function. That is for another day.

Again I am asking, What does a Layer 2 Protocol do? Well this uses your local network to well...bypass your local network. By creating this encrypted tunnel your data stays inside where others cannot see what travels inside the tunnel. Keep in mind, while the network cannot see what is inside this Tunnel it can at least see that the Tunnel is there.

Anyways, this Tunnel forwards 100% of your data to the VPN Server. From there your data then reaches out to the rest of the World Wide Web. I bring this up so that you can keep in mind that by using a VPN Provider you are putting your trust in their hands. Trust that they will keep your information private, and trust that they are not the ones sniffing your traffic.

Trust that they will keep your information private

So Why Would I Host My Own VPN Server? How Can That Benefit Me?

By hosting your own VPN server, you can get yourself access to your home network from anywhere you might be. One of the ways I leverage hosting my own VPN server is that I also host Pi-Hole. Pi-Hole allows me to have ad-blocking at the network level for my entire home network. Thanks to Pi VPN it also allows me to have ad-blocking on my mobile phone! I'll have a separate write up on Pi-Hole at a later date.

## The Pi Zero Setup Process

If you already know what a VPN is then this is where we start! For the rest of this document we will be examining the performance of a Raspberry Pi Zero acting as a Wireguard VPN Server running a clean installation of the 32bit Raspberry Pi OS straight from Raspberry Pi Imager v2.6 - Wireguard VPN will be used via the Pi VPN package. To speedtest the Raspberry Pi we will be using speedtest-cli which can be installed with

```sudo apt install speedtest-cli```

If you look to the image to the right, we can see that my network is capable of moving at least 800 megabit (Mbps) up and down. This is great as it exceeds the 802.11n wireless network interface found on the Pi Zero which is only theoretically capable of moving 600 megabit (Mbps) in either direction.

Providing wireless to this little wireless computer is a Ubiquity UniFi AC-AP-Pro broadcasting on 802.11b/g/n on the 2.4GHz band which is what the Pi Zero needs on top of broadcasting an 802.11ac network on the 5GHz band. However the Pi Zero is not able to leverage 802.11ac.

A few more notable specs of the Raspberry Pi Zero is that it is running a Broadcom BCM2835 at 1GHz with 512MB of on-board memory. It's highly likely the phone or device you are reading this on has 8x or more on-board memory.

## Determining The Baseline

Okay, we know the Raspberry Pi has the technical ability to push 600Mbps of data, so we will need a baseline of what the Pi does in the real world. The Raspberry Pi sat on my desk about 4 feet from the Wireless AP it was connecting too getting power from a Samsung wall adapter so I suspect that power delivery will not be impacting its ability to operate smoothly.

| **Ping** | **Upload** | **Download** |
| 25.3ms   | 28.8 Mbps  | 6.7 Mbps  |
| 15.0ms   | 29.6 Mbps  | 14.5 Mbps |
| 14.3ms   | 23.8 Mbps  | 14.6 Mbps |
| 17.7ms   | 26.1 Mbps  | 15.0 Mbps |

Examining the information above we should be expecting on average 27 Mbps upload and only 12.7 Mbps download.

Pi Zero - Idle

The next important part of our Pi Zero VPN Server testing is the CPU utilization. If the device gets stuck at 100% usage we are inevitably going to experience increased latency while browsing the web, and this latency will severely impact the usability of the platform. Lucky for us, htop is a CLI utility baked into the Raspabian OS as well as many other distros such as Ubuntu or Linux Mint. So now lets go ahead and look at the Load Average.... Over the last minute prior to the screenshot we were averaging 20% utilization. Over the last five minutes, 24% utilization. Finally over the last 15 minutes, only 16%.

Something important to know is that the screenshot above was taken while the Pi Zero was totally idle besides the single SSH session needed to obtain this information.

## Load Testing

To load test this Pi Zero my plan is to start with a single client device and stream a YouTube video at 1080p. If the server remains stable I will add another device with a second 1080p YouTube stream. I intend on adding one device at a time until 4 devices are connected, all the while checking for stability in-between client additions. I suspect, that is a single Raspberry Pi Zero can host four simultaneous 1080p video streams it just might be an acceptable experience. I mean at the end of the day I just want to know what a $7 USD from MicroCenter can do.

### Device One

The first device connected was my wife's Razer Blade 15 and of course we had to run the speedtest you see above. If you compare these numbers to the baseline, the latency has improved! I think that is crazy since the Raspberry Pi has not moved and the network environment has not changed a bit. Now, the upload and download speeds being only 8.6 Mbps and 7.8 Mbps respectively is acceptable. Its not great but keep in mind your network is as slow as your slowest link. Considering we are trying to put a 1GHz ARM processor in the way I find these speeds to be okay. Especially if we are just trying to stream a video. Now we will start a 1080p YouTube stream on the first device.

### Device Two

As expected, the Pi Zero was handling this workload rather well, so I suspect it is time to connect a second client. The second device was my personal phone. Once connected I fired up an Episode of THE WAN SHOW that was about 2 hours long and the quality automatically set for 1080p HD. This is great news! Some time past and my phone was able to successfully maintain the YouTube stream. This is when I got curious and broke the scientific protocol I had been carefully following up to this point. I decided to try and download a Ubuntu Desktop ISO onto the first connected client. Oh man! This was super slow to initiate the download. I figured it would fail but to my surprise after about 5 minutes it actually started to trickle along. This image below is from htop with both YouTube streams AND the Ubuntu ISO download.

### Device Three

Now that I have gotten this interesting screenshot and the Pi Zero was stable, I added a third device. I bugged the wife for her cell phone and got her connected. I asked her to listen to some YouTube with the quality turned all the way up to 1080p while she did homework. Now with this third device, YouTube automatically selected 720p but that was outside the scope of what I wanted to test. We had to go into advanced and set the quality to 1080p. That is okay, the Pi Zero handled this fine with about 1.5 seconds of buffering right at the beginning. We will revisit her and ask about her experience a little later.... However I continued to watch htop and while the CPU utilization was high it remained stable. At this point I am amazed at what this little thing can do!

### Device Four

The Pi Zero was stable at three devices, so now we need to add yet another device. Into the old phone box I go, looking for my wife's old Samsung S9. Exactly the same protocol as earlier, pick an episode of The WAN Show and force the quality to 1080p. This time, the Galaxy S9 auto selected 480p. In my experience this the client understanding that the network might be degraded and unable to push the full stream. This time it buffered for about 6 to 7 seconds but for almost 20 minutes ran that video perfectly fine. This is great news. I'm starting to suspect that the Pi Zero might be a valid home VPN endpoint for those edge case users that want a super cheap was to access their home network...

#### Can We Break It

By no means am I an expert in load testing network components let alone anything for that matter. But what I do know how to do it download things. Client 1 has a 2GB ISO queued up and ready to download. Client 2 has 5 applications that could be updated. Client 3 has 12 applications available for download, and Client 4 has 26 applications available for updates. I am going to start all 4 download streams at the same time.

I think the answer is yes, we can "break it" but no how you would suspect. Since we had no quality of service in place nor did we have any traffic shaping the ISO download took priority. None of the other applications could update from the Google Play Store while that other stream was running. Now this is where it gets a bit interesting. Even after I cancelled the ISO download and disconnected from the VPN, the other clients continued to experience issues where there was no throughput. After disconnecting and reconnecting to VPN on each client we were able to get data throughput again. All the while we can keep in mind that the Pi Zero never got stuck at 100% utilization and the software was stable enough it never crashed. So I would say, yes we can cause impact to others but no we cannot break it per say.

## Conclusion

Yes, a Raspberry Pi Zero could reasonably host a small scale VPN server for one or two clients as long as the WAN uplinks for those clients is rather speedy. We must keep in mind that your speeds are limited to your slowest interface in the data path. So even if we could push 10 Mbps upload and 20 Mbps download from the server, if we are traveling with a 5 Mbps up/down connection we would likely see speeds much less than 5 Mbps which would be borderline acceptable for only a single device. Which brings me to the statement, your mileage may vary. But overall YES you could potentially deploy a Raspberry Pi Zero at Grandma's house in Canada and stream Netflix from her house while living in the United States.

Wait, where did that last sentence come from? Maybe the countries are wrong but I saw a forum post on The Level1Tech Forums asking about Raspberry Pi Zero VPN performance which was the spark that lit the fire for this testing.

Thank you for reading, please feel free to reach out and provide any constructive criticism.
