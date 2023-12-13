---
layout: posts
title:  "How To Change The Hostname of a Raspberry Pi"
date:   2022-01-10 08:00:00 -0700
categories: raspi_pi
---
Hello Everyone! If you prefer video formats, please go ahead and give the YouTube video above a quick watch, but if you prefer reading a "white paper" style document I'll jump right into the meat and potatoes below!

While you do not need to set a hostname, they make it easier to identify individual devices on a network. Also, if you are hosting a web server that supports HTTPS, the hostname must match the SSL certificate that is being used or else it will give up an error!

Using a One-Liner in Command Line (CLI)

First we want to check our hostname so we can verify if we actually made any changes, we can do this with the command...

```hostname```

Now for the one-liner

```sudo hostnamectl set-hostname <new hostname>```

and then once again we can run "hostname" to see our changes. For this to officially take effect we need to reboot our device. All three are applicable, choose whatever you like best!

```sudo reboot```
```sudo shutdown -r```
```sudo shutdown -r now```

Using Nano Text Editor

If you would prefer to use the Nano Text Editor, you can access your hostname file using the following command...

```sudo nano /etc/hostname```

Once you have replaced the text with your desired hostname, CTRL+S to save and CTRL+X to exit from Nano and now you can go ahead and reboot, just as you would had you used the CLI One-Liner.

```sudo shutdown -r now```
