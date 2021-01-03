---
title: Unifi Controller on RaspberryPi
category: [Ubiquiti]
---

**Installing Unifi Controller using the following guide:**

[PiMyLife](https://pimylifeup.com/rasberry-pi-unifi/)

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

Later i tried to adopt my AP wich is a [UAP-AC-LR](https://dl.ubnt.com/qsg/UAP-AC-LR/).
But it didn't find any devices. 
I SSH:ed into the AP and issued the command:

```
set-inform http://ip-of-controller:8080/inform
```

In the future I'm going to extend my network with more products from Ubiquiti. First in is a edgeRouter so I can throw away my shitty all-in-one router I got from my ISP.

**Stay tuned for a review!**