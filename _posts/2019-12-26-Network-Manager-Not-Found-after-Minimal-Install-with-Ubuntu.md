---
layout: post
title:  "Network Manager Not Found after Minimal Install with Ubuntu"
date:   2019-12-26 
categories: Troubleshoot
---

I got an old laptop from my, non blood related, auntie, Asus EeePC with good old Atom CPU and 1 GB of ram. I may or may not upgrade the ram to 4 GB and the drive, currently SATA, to SSD. To get the most out of it, would have no other choice but to go lean, super lean. I went with Lubuntu Minimal Install and nothing else. The installation was pretty straight forward, the main problem comes when I could not connect to the internet… How am I going to laugh at Patriotic American bashing at the Declaration of Independence!?

The ethonet connection and wireless connection were there, but network-manager was not found. Thankfully, ifconfig is here to save the day.

Enter ifconfig on the terminal to see which network connections are available.
Enter sudo ifconfig <cxn_name> up to open the connection.
Then enter sudo dhclient <cxn_name> to kick off the protocol.
If you want to connect via wifi, you would
Otherwise, check your connection by pinging yahoo or google.
To simplify your life in the future, download network-manager-gnome (network-manager should come with it) by sudo apt-get install network-manager-gnome
Run Network Manager by entering sudo service network-manager restart and sudo service networking start
Enter nm-applet to start the Network Manager
I’d also suggest you to download sudo apt-get install software-properties-common for other goodies, e.g. I downloaded midori
Now have fun with the internet!

Reference:

https://askubuntu.com/questions/422928/how-to-reinstall-network-manager-without-internet-access
https://askubuntu.com/questions/652401/i-accidentally-deleted-the-network-manager-and-dont-have-access-to-internet-any
