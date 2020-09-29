---
layout: post
title: SBC(Single Board Computer) server setup
---

So server, server, server, what to do with my buzzing server in the hallway?
I was cleaning upp my network equipment and decided it was time to get rid of the homemade server Ive used for many years.  I figured that for my needs I only need a singleboard computer. 

What i want to run on my server:

* Web Site (Have nooo idea if anyone visits it)
* Testing some webservice (ID server, RESTful apis, etc)
* SSH PassForward to other servers.

So after a fair bit of searching in drawers, closets, boxes I finally found one of my raspberries. Fired it up and YES!! it was equipped with a Raspbian installation. The only thing I needed to do was configure the network and find my ssh key so I could connect. Searched my secret notebook for credentials connecting and found it though it was over a tear I used it.

Now I had everything in hardware I needed to get started. I've connected my pie to my computer with a Ethernet cable. I changed the adapter settings for my laptops Ethernet with the following command:

```
sudo ip addr add 192.168.1.1/24 dev enp2s0
```

This command reconfigures my ethernet device (enp2s0). I was in luck because my raspberry was configured the same (if the pi was configured with another adress let's say 192.168.2.1 it wouldn't work) this is the default adresses used so it's always a good idea to start there.

When this was done my internet connection was lost (my one and only resource for knowledge!!!). This was because my wlan adapter was setup using the same subnet.
Piece a cake! I connected to the raspberry over ssh with my rsa key and password (always protect your keys with passphrases!) and reconfigured the pi to use another subnet *192.168.2.0*. Rebooted and changed my laptops adapter to match the pies. Now the conflict was gone and I could browse the internet while configuring/tinkering with the pie (one browser for every terminal 😉).

Now I wanted to reach the internet to fix the system with the latest updates available but I had no internet connection!? Im only connecting to my pi over ssh and on my local network. The internet connection is not shared over my ssh connection. Forgot to make a connection to the wifi on my raspberry, made the necessary changes to my *wpa_supplicant.conf* and successfully connected to my home wifi. But there was still no internet connection on my pi! 

After som digging the final touch was the ip route:

`ip route list` Before:
```
default via 192.168.2.1 dev eth0
```
After:
```
default via 192.168.1.1 dev wlan0 
```
Command to accomplish this:
```
sudo ip route change default via 192.168.1.1 dev wlan0
```
Where *192.168.1.1* is your target network for internet and *wlan0* is your adapter.

Mission Success!

Let's see what this baby can do!
