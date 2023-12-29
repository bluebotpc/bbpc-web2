---
layout: posts
title:  "Ad-Blocking on the Go using Pi-Hole and Pi-VPN in the Cloud"
date:   2022-01-26 08:00:00 -0700
categories: technology
---
{% include video id="RJ2zoA9Y0Tk" provider="youtube" %}

I do not think that I am alone when I say that I hate advertisements. I actually think that my distaste for advertisements is the major reason that I do not watch any form of traditional television whether that be from a cable company or even the free local channels that are streamed over the air. Getting away from traditional television, I also hate seeing advertisements on the internet as well. Between Google AdSense tracking you everywhere you go, and other advertising partners putting trackers on top of trackers in every single web page and mobile application is a major turnoff.

That is why I think we are extremely lucky that the developers over at Pi-Hole and AdGuard are some great folks and we should all be buying them a coffee. These guys allow us to block ads by the way of DNS filtering and I have found this to be very effective. So I present you the video above and the write up below. I hope between the two resources I can help guide you on how to deploy your very own Pi-Hole and Pi-VPN instance that will give you the ability to live a mildly ad-free life and maybe even help secure and anonymize some of your online browsing habits.

## Process Overview

Before we start, you will need a Domain Name registered through a Domain Registrar. I suggest Google Domains because they have a massive and extremely responsive DNS infrastructure that is feature rich.

- Deploy your Cloud Virtual Machine
- Create DNS Records with your Domain Registrar
- Prepare the Virtual Machine environment
- Deploy Pi-Hole & Pi-VPN applications
- Secure Pi-Hole with HTTPS/SSL using CertBot by Let's Encrypt
- Secure the Virtual Machine with a firewall using UFW
- Configure Unbound to lightly anonymize DNS requests

Most of this guide is going to be done in the Command Line Interface (CLI) so it is best that you choose an Operating System you are comfortable with. When it comes to most users, likely yourself included, your choice of Linux OS does not really matter. At the most basic level they all do the same thing and typically even very similarly. With that being said, I am choosing to deploy a Ubuntu Sever 20.04 LTS which is based on Debian.

## Staging your Environment

I have deployed my Ubuntu Server 20.04 LTS virtual machine and I am going to take the IPv4 and IPv6 records provided by Linode to create DNS records with my Domain Registrar, Google Domains.

Once I have created my A Record for the IPv4 address and an AAAA Record for my IPv6 address I am going to wait approximately 15 minutes for my virtual machine to finish provisioning and my DNS record to propagate around the globe.
After this small waiting period, you should now be able to connect to your virtual machine using the domain name via SSH. PuTTY is the most popular SSH application but I will be using MobaXterm Professional.
Once you get connected, the very first thing we will need to do is patch updates, set our timezone to help keep track of logs, and set our hostname to match our DNS records to allow a fully functional SSL certificates to be issued. The commands below will do just this!

```bash
sudo apt update && sudo apt upgrade -y
sudo hostnamectl set-hostname <yourHostname>
sudo timedatectl set-timezone <yourTimezone>
```

Check out my other post Setting the Timezone on a Raspberry Pi 4 to find the full list of time-zones.

Now that we have done most of our preliminary setup, we need to add our hostname to our loop-back address in the Operating Systems host file. We will use the preinstalled and simple to use NANO text editor.

sudo nano /etc/hosts

Add your hostname to the loopback address

CTRL+S to save then CTRL+X to exit and we are ready to reboot our VM. Either of the syntax below will do.

```bash
sudo shutdown -r
sudo reboot
```

## The Pi-Hole Deployment

You are more than welcome to install Pi-Hole using the default web server package lighttpd (Pronounced Lighty) but some folks like myself prefer Apache2 because it is easier to setup metrics monitoring. These are all the packages you will need to install before Pi-Hole for it to work as expected.

```bash
sudo apt install apache2 php php-sqlite3 libapache2-mod-php -y
```

Now we can proceed with the Pi-Hole installation using their one-liner. While I have this one listed, please be sure you get the one-line installer straight from the source GitHub here!

```bash
curl -sSL https://install.pi-hole.net | bash
```

Now before you browse to your Pi-Hole admin portal you will need to update some permissions on your VM. We need to add the www-data user access to the group pihole. Once that is completed we can restart the apache2.service for those changes to take effect.

```bash
sudo usermod -a -G pihole www-data
sudo service apache2 restart
```

During the Pi-Hole one-line installer you were provided a password for the Pi-Hole admin panel, you can change this to whatever you like using this command. Just follow the prompt on-screen.

```pihole -a -p```

## Securing our Pi-Hole Admin Portal with HTTPS/SSL

We will be requesting a free SSL Certificate from Let's Encrypt using the CertBot application. While you can get certbot from the APT package manager, I recommend using the Snapcraft package manager.
Once we have the CertBot snap package installed we can use the syntax you see below to automatically configure your Apache2 installation. Just follow the on-screen instructions.

```bash
sudo apt remove certbot -y
sudo snap install --classic certbot
sudo certbot --apache
```

At this point, you have successfully secured your Pi-Hole admin interface with HTTPS/SSL. At this point I would urge you to go and access this new web interface and get familiar with what all you can do inside it. Now that you have taken a peak inside your Pi-Hole admin interface I would advise that you add some of these Ad-Lists to your Pi-Hole, but everyone's blocking needs are a bit different.

The Big Block Collection by The Firebog

## Unbound - A Recursive DNS Resolver

Instead of using an upstream DNS resolver such as Google, CloudFlare, Lumen, or Comcast we would like to have the ability to resolve our own DNS records. This will provide a basic level of anonymization since we will not be sending out DNS queries to the likes of Google or our local ISP.

To do this, we are going to install Unbound and point our Pi-Hole towards itself for DNS resolution. I am going to tell you to simply read the Official Pi-Hole Documentation on how to setup Unbound. This document is literally copy paste-able and explains everything better than I possibly could.

Loop-back for DNS in Pi-Hole Settings

## Let's Deploy Pi-VPN

While Pi-Hole can block ads by filtering DNS queries the goal of this guide/document is to help you setup a cloud VPN endpoint so that you can have your data flow between your device and this virtual machine inside an encrypted VPN tunnel. No longer will you be browsing the internet from your device, but instead you will be browsing from your Virtual Machine. Lets get started with the one-liner installer.
As always, check the source for the most up to date process!

```curl -L https://install.pivpn.io | bash```

During the installation, you will first be asked to setup a non-root user account to hold the Pi-VPN certificates for your users/connections. I named my user vpn-user for ease of use.
I would recommend you select Wireguard as the VPN protocol. Also during this installation, be sure to select local Pi-Hole for DNS resolution. You should now have completed the installation of Pi-VPN. Yes, that is it. Now we need to generate a certificate for our device.

You can learn a ton about the proper syntax by just typing pivpn

```bash
root@vpn:~$ pivpn
::: Control all PiVPN specific functions!
:::
::: Usage: pivpn <command> [option]
:::
::: Commands:
:::    -a, add              Create a client conf profile
:::    -c, clients          List any connected clients to the server
:::    -d, debug            Start a debugging session if having trouble
:::    -l, list             List all clients
:::   -qr, qrcode           Show the qrcode of a client for use with the mobile app
:::    -r, remove           Remove a client
:::  -off, off              Disable a user
:::   -on, on               Enable a user
:::    -h, help             Show this help dialog
:::    -u, uninstall        Uninstall pivpn from your system!
:::   -up, update           Updates PiVPN Scripts
:::   -bk, backup           Backup VPN configs and user profiles
pidmin@vpn:~$
```

Now that we have seen the available syntax we can create a new certificate for our device.

```pivpn add name <deviceCertificateName>```

Now we need to display the qr code so that we can connect our mobile device from inside the Wireguard Application available on the Google Play Store and the Apple App Store

### Pi-VPN on a Non-Mobile Device

If you are trying to connect to your laptop or desktop to your Pi-VPN server you will need one of those generated certificates but how?! You can't just pickup and scan a QR code with the Windows Wireguard application. Earlier in this guide I mentioned that you can use PuTTY for SSH access your VM but I use MobaXterm because it has a built in SCP File Manager. This allows you to upload and download files with ease right from the application.
During the Pi-VPN one-line installer you had to create a user account to hold the configs. Now we will create a password for that account so we can SSH into it, then we will access it and download the configs we would like.
From the root user we will do the following command and follow the on-screen instructions.

```sudo passwd vpn-user```

Now we will connect via SSH to our vpn-user

```ssh vpn-user@<ourIPAddress>```
```cd ./.configs```

Now we are inside the Pi-VPN config folder we should use MobaXterm to download our target certificate.

### UFW - Uncomplicated Firewall - The Elusive Firewall Configuration

Now we need to setup an application layer firewall. Yes, you have secured your Pi-Hole web interface with HTTPS/SSL but you still have a computer connected directly to the public internet with no real security. We can change this a bit! We will now configure and deploy UFW to do our best to protect our machine. I'd advise you do further research than just this document to secure your virtual machine even further.

The following configuration below will start by setting up the defaults for UFW, then we will allow SSH so that we can continue to manage our machine with Command Line. We will also allow HTTP and HTTPS so that our web interface will continue to work. Then we will allow port 53 via the TCP and UDP protocol so that the machine can route DNS requests. Finally we will allow incoming traffic from the Wireguard interface to exit our VM on the ethernet0 interface so that we can use the VM as our VPN endpoint.

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw allow 53/tcp
sudo ufw allow 53/udp
sudo ufw route allow in on wg0 out on eth0 from 10.6.0.0/24
sudo ufw enable
sudo ufw status verbose
```

## Finalizing Our Deployment

If you have made it this far in the guide, you have done some great things!
You have....

1. Created a virtual machine in the cloud
1. Deployed public DNS records
1. Updated and patched a Linux virtual machine using the CLI via SSH
1. Installed and secured an Apache web server with an HTTPS/SSL certificate
1. Installed and configured a DNS filtering application
1. Installed and configured a VPN server
1. Connected clients to a self-hosted VPN server
1. Deployed an application layer firewall
1. It is time to reboot your virtual machine one last time and essentially, set it and forget it! Thank you for reading!

### Great Resource Documents - Supporting Information

[Official Linode Guide - Securing Web Traffic Using Certbot with Apache on Debian 10 and 9](https://www.linode.com/docs/guides/enabling-https-using-certbot-with-apache-on-debian/)
[Official Pi-Hole Documentation - Unbound on Pi-Hole](https://docs.pi-hole.net/guides/dns/unbound/)
[Pi-Hole Community Forums - Pi-Hole with an Apache2 deployment](https://discourse.pi-hole.net/t/installing-pi-hole-on-existing-apache-server/43968)
[List of Ad-lists for Pi-Hole - Firebog](https://firebog.net/)
[CloudFlare - What is DNS](https://www.cloudflare.com/learning/dns/what-is-dns/)
