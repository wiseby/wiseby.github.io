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

**Update 28/2 2021**

Made a system update and installed Raspberry Pi Os. Unifi installs openjdk-9-jre but openjdk-8-jre is needed.

```bash
sudo apt install openjdk-8-jre
```

Finally, Update and install the Controller Software:

```bash
sudo apt-get update && sudo apt-get install unifi -y
```

**There are some issues with the arguments to mongodb**
**Not needed the last time I installed on Raspberry Pi Os version 10 (Buster) this issue could have been fixed by ubiquity**

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

Don't forget to open ports on the controller server:

| Protocol  | Port | Description |
|----|------------|-------------------------------------------------------------|
|UDP |	3478      |	Port used for STUN.                                         |
|UDP |	5514      |	Port used for remote syslog capture.                        |
|TCP |	8080      |	Port used for device and controller communication.          |
|TCP |	8443      |	Port used for controller GUI/API as seen in a web browser   |
|TCP |	8880      |	Port used for HTTP portal redirection.                      |
|TCP |	8843      |	Port used for HTTPS portal redirection.                     |
|TCP |	6789      |	Port used for UniFi mobile speed test.                      |
|TCP |	27117     |	Port used for local-bound database communication.           |
|UDP |	5656-5699 |	Ports used by AP-EDU broadcasting.                          |
|UDP |	10001     |	Port used for device discovery                              |
|UDP |	1900      |	Port used for "Make controller discoverable on L2 network" in controller settings. |

Later I tried to adopt my AP which is a [UAP-AC-LR](https://dl.ubnt.com/qsg/UAP-AC-LR/).
But it didn't find any devices. 
I SSH:ed into the AP and issued the command:

```
set-inform http://ip-of-controller:8080/inform
```

It only needed a little flirting to get excited and join the team 😉

In the future I'm going to extend my network with more products from Ubiquiti. First in is a edgeRouter so I can throw away my shitty all-in-one router I got from my ISP.

**Stay tuned for a review!**