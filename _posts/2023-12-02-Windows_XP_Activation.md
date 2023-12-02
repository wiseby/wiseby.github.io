---
layout: post
title: "Activating Windows XP"
categories: ["Retro Gaming"]
---

A couple of months ago I installed Windows XP on my very old PC with components from 2008. My goal was to play my old favorite games from that era. 

When I sat down today to play Red Alert 2, I got the reminder to activate Windows, but I didn't have any valid product keys. I did some googling and I wanted to tell you what method I used to successfully activate it.

I activated the product by using a software called Universal MS Key Toolkit (UMSKT). It's opensource and available on [github](https://github.com/UMSKT/UMSKT). I simply ran the program to generate a activation key and entered it, but this was not all. The activation wanted me to go online to verify the authenticity of the product-key and for obvious reasons this computer should never be connected to the internet. My option was then to select the "activate over telephone support". 

![Activate over telephone service](/assets/images/activate_xp_telephone.png "Activate over telephone service")

The UMSKT program got you covered. Run it with the following command and use your _Installation ID_ displayed on the next screen.

`umskt -i <Installation ID>`

Enter this as your verification number and BOOM! You should now have an activated version of Windows XP.

I later got the Anti-Piracy base destroyed when starting up a game in Red Alert 2 so that was a huge disappointment when I already spent so much time to play a simple game. I even have the original game on disc! How I will solve that is a topic for another post.

_More retro-gaming will follow!_