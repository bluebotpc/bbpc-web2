---
layout: posts
title:  "Matt's Desktop Build in 2022"
date:   2022-06-24 08:00:00 -0700
categories: technology
---
The Razer Blade 2019 Advanced (RZ09-02887) was originally announced by Razer on January 6th 2019 in their official blog post here. The Mercury edition with the RTX 2070 Max-Q and 512GB Samsung SSD was priced at a whopping $2,649.99 USD. This crazy little laptop was rocking a beautiful 15 inch 144Hz IPS display and a pretty dang powerful 6 Core/12 Thread Intel Core i7-8750H. For myself and many others, the true appeal to the Mercury Edition was how it looked great in a boardroom. No more unprofessional glowing green logo on the back, you could finally blend in with all the other Apple Macbooks' in the room.

Now I was lucky to get this device for much less than that crazy MSRP. A co-worker of mine sold it to me in January 2020 for $1,500 due to intermittent audio quality issues coming from the left speaker. At the time, I did not have a laptop at all and my desktop PC that I used for gaming was pretty under powered. So I was more than excited to not only have a laptop that I could take from the house and work but also play Forza Horizon 4 at Ultra Settings and still get 100 fps.

## More Recent Backstory

Something everyone who is interested in a Razer laptop needs to understand is that these things run hot. Heat and dust are the two big enemies of electrical components so just keep that in mind. In my experience with separate 2 Razer laptops in my household, it was common for us to see temperatures over 85*C on the CPU as reported from HWMonitor when playing intensive games like Farming Simulator 2022 and Microsoft Flight Simulator 2020. That 85*C could be seen even when the fans were at 100% (5200RPM) and elevated on a laptop tray with a larger cooling fan.

The battle to keep my laptop cool even escalated to the point of replacing the thermal paste and thermal pads inside the device with some higher quality material I picked up from MicroCenter. It was only 3 weeks later the chipset overheated and let out the magic blue smoke. She's dead Jim.

## New Parts List Rational

CPU: AMD Ryzen 5 5600 - At $150 this was the cheapest but current generation Ryzen 5 MicroCenter had in-stock. It has 6 Cores/12 Threads so it shouldn't be a downgrade from my Intel i7, but more importantly 35MB of Layer 3 cache!  That is 35MBs of data that is on the CPU die and is shared between all 12 compute threads.

To put that 35MB of L3 cache into prospective, my massive dual-socket 40 thread server only has 25MB of L3 cache per CPU. This means the CPU can keep more memory closer it the compute modules which can reduce latency in many workloads.

Motherboard: ASRock B550 Pro4 - $135, This motherboard seemed to hit the sweet spot. Its not too cheap, not too expensive. I didn't feel comfortable spending less than $120 on an AMD motherboard because for some reason the AMD lineups have always been neglected. Even the Bill of Materials (BOM) is cheaper, typically due to cutting corners on cooling and power delivery. This board has some really solid VRM and chipset cooling!

Memory: G.Skill 16GB DDR4-3200 - $60, cheap and it fits. I don't care at all about RGB lights. Perfect!

Power Supply: EVGA SuperNOVA 650GT - $70 and from a reputable manufacturer. Its also 80 Plus Gold rated and the modular feature was honestly just a bonus. Great, add it to the cart.

Graphics Card: EVGA RTX3050 - $340, while my mindset is a bit dated, I figure you can +1 to the generation and then step down 1 model and get similar performance. So with that mind set a RTX2070 +1 Generation would be the RTX3070, then step down 1 model and you'd get the RTX3060. But wait... this is an 3050 instead. Well I figured my 2070 Max-Q being a mobile card couldn't possibly be performing at the same level as a true full-sized 2070. Especially knowing the thermal limits of my laptop. Gamble, but I'll gladly risk it.

Case: Thermaltake V100 - $50, The current trend in the custom PC building community is to have massive tempered glass side panels and a slew of RGB everything. I can get down with a decent sized window to allow me to look into my neat little computer, but the amount of glass cases come with these days is crazy. Nothing I've said so far is about this Thermaltake V100 case though! Its pretty basic, but I did not come across any sharp edges and there was plenty of room to route power cables behind the motherboard.
Overall, for $50 its a good case. Lacking in IO but who really cases at this price? My favorite part was the nice thumbscrews on the side panels.

## Reusable Parts List

As for re-usable parts I was really down to just 2 items that I could keep. Both being M.2 NVMe Storage Disks. Both being Samsung as well. The only notable device was the 1TB Samsung 970 EVO that already had a copy of Windows 10 Home installed onto it. I was a bit worried that I would be prompted for an activation key, but that was not the case. Both my M.2 drives were plug-n-play which was awesome.

## Build Process and Post Build Notes

Everything went smooth and according to plan. I used the AMD Wraith cooler for the CPU and so far have not ran into any cooling related issues but this will in-fact be my first upgrade. Something everyone should note is that for the CPU cooling fan to run at the speeds I expected I did have to change the fan profile which was rather hidden in the BIOS.

The dual M.2 drives saved me from needing to ran any SATA power cables from the EVGA modular power supply and I was very much impressed with the quality of the interfaces and power cables themselves. I would totally buy this power supply again!

The case, while very cheap also blew my expectations out of the water. Thermaltake used to have a super budget case that was a bit disappointing. However this time around, even thought I knew it was a gamble, they have really hit a home run at $50.

- The motherboard area already had all the applicable ATX standoffs installed.
- There was sufficient room for power cable routing.
- The side panels didn't feel crazy flimsy. Neither did the overall chassis.

Airflow does seem to be a weak point but so far its non-impactful and can be resolved by some cheap $15 fans being added.

### Future Content?

You may have noticed that in the **Build Process and Post Build Notes** section above I did not actually talk about the EVGA RTX 3050 graphics card and how well it met my expectations. Instead I plan on talking about that in another blog post dedicated to GPU benchmarking.

It that has been written, you can find it here!
