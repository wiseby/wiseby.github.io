---
title: Unifi Controller on RaspberryPi
category: [Ubiquiti]
---

**Installing Unifi Controller using the following guide:**

[PiMyLife](https://pimylifeup.com/rasberry-pi-unifi/)

There is also a Official guide by Ubiquity that I found later, guide [here](https://help.ui.com/hc/en-us/articles/220066768-UniFi-How-to-Install-and-Update-via-APT-on-Debian-or-Ubuntu)

I Skipped some steps. Short version is this:

Update and prepare system with tools needed to download and install:

```bash
sudo apt-get update && sudo apt-get install ca-certificates apt-transport-https
```

Add repository to apt.list:

```bash
echo 'deb https://www.ui.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/100-ubnt-unifi.list
```

Add repository GPG Key:

```bash
sudo wget -O /etc/apt/trusted.gpg.d/unifi-repo.gpg https://dl.ui.com/unifi/unifi-repo.gpg
```

Finally, Update and install the Controller Software:

```bash
sudo apt-get update && sudo apt-get install unifi -y
```

**There are some issues with the arguments to mongodb**

I found this [link](https://community.ui.com/questions/Unifi-controller-on-Ubuntu-18-04/93b00b88-7542-40ba-bb0b-a80a84415e1d)

did the following:

renamed /usr/bin/mongod to /usr/bin/mongod.bin

```
cd /usr/bin
sudo mv mongod mongod.bin
```

created new mongod file and added following content to new mongod file:

```
sudo nano mongod
```

```
#!/bin/bash
cleaned_args=$(echo $* | sed -e 's/--nohttpinterface//')
exec /usr/bin/mongod.bin ${cleaned_args}
```

This script made mongodb start with arguments supported by the version on my system.

restarted unifi.service:

```
sudo systemctl restart unifi.service
```

and the controller started successfully!

The controller interface should now be accessable on your network by visiting host address of the device you installed the controller on.
I installed it on a Raspberry Pi that sits on my main network panel and could be reached at port 8443. If you installed it on your desktop/laptop 
you could visit the address *http://localhost:8443*.

The first time you do this there are some initial setup steps to make like setting up the root user, connect devices, create networks etc.

Later I tried to adopt my AP which is a [UAP-AC-LR](https://dl.ubnt.com/qsg/UAP-AC-LR/).
But it didn't find any devices. 
I SSH:ed into the AP and issued the command:

```
set-inform http://ip-of-controller:8080/inform
```

It only needed a little flirting to get excited and join the team 😉

In the future I'm going to extend my network with more products from Ubiquiti. First in is a edgeRouter so I can throw away my shitty all-in-one router I got from my ISP.

**Stay tuned for a review!**