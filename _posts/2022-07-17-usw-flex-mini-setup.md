---
title: More Devices from Ubiquiti
categories: [Ubiquiti]
---

Yes it's time for an upgrade. Making my TV and Playstation 4 wired and pulled a cable under the lawn for high speed connectivity for the guest house.

Also managed to configure my EdgeRouter to work with my unify controller

Had some trouble when adapting the USW-Flex-Mini. Its a small simple switch that lacks ssh capabilities. How do we make it adapt to the controller? It's easy, reading the docs tells us that we can hold the reset button (located underneath, accessible with a small pin, I always use a classic paper-clip) for 10 seconds. The status-LED should start to blink white-blue-green. This put's it in adoption-mode, sending out the inform command to the controller.

After configuring the USW-Flex-Mini I had some issues yet again with adopting a AccessPoint (UAP-AC-LR) connected to it.
Listing all devices on my network I found the IP-address of the new AP and connected to it with ssh.

When logged in you could execute the command 'info' to get basic information like the one below:

```sh
NameOfDevice-BZ.5.43.52# info

Model:       UAP-AC-LR
Version:     5.43.52.12774
MAC Address: ------------
IP Address:  ------------
Hostname:    NameOfDevice
Uptime:      3335 seconds

Status:      Server Rejected (http://unifi:8080/inform)
NameOfDevice-BZ.5.43.52#
```

I got the status **'Server Rejected'**.

Restoring Device to default using the syswrapper:

```sh
ssh <user>@<ip-address-to-device>
Enter password:
BusyBox v1.25.1 () built-in shell (ash)


  ___ ___      .__________.__
 |   |   |____ |__\_  ____/__|
 |   |   /    \|  ||  __) |  |   (c) 2010-2021
 |   |  |   |  \  ||  \   |  |   Ubiquiti Networks, Inc.
 |______|___|  /__||__/   |__|
            |_/                  https://www.ui.com/

      Welcome to UniFi UAP-AC-LR!

NameOfDevice-BZ.5.43.52# syswrapper.sh restore-default
```

This made the device visible in the controller without any more actions.

_Ubiquiti is the one product I've used that just works when it's setup correctly, happy networking!_
