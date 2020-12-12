---
title: Unifi Controller on RaspberryPi
category: [ubiquiti]
---

###Installing Unifi Controller using the following guide:

https://pimylifeup.com/rasberry-pi-unifi/

###There are some issues with the arguments to mongodb

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

restarted unifi.service:

```
sudo systemctl restart unifi.service
```

and the controller started successfully!

Later i tried to adopt my AP wich is (name of device here!!!)
But it didn'y find any devices. 
I SSH:ed into the AP because it was accessable to the network correctly and issued the command:

```
set-inform http://ip-of-controller:8080/inform
```