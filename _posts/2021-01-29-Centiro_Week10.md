---
layout: post
title: "Centiro Internship Week Ten"
categories: [The Internship]
---

Mondays starts with planning.
Good practice to talk about the weeks events and reflect on what happened previous week and the progress. Updating the Azure Board,
some work-items need more time and transfers between sprints. The backlog consists of user-stories created by our team before we got this mission, and some of them are a little bit obscure.
We tend to ignore them, and created our own stories that where relevant to requirements from the team.

#### How far have we come?

As of this week we are putting much of the pieces together. Moving over to implement the new api in our client application. Changing the code in that part of the project was fairly simple and that must be a sign of code written the right way. Some methods needed some refactoring because it took to long figuring out what it did, most of the time the method did more then one thing (remember Single Responsibility Principle!).

The mock part of the client needs some mayor refurbishing now that we have changed much of the public interfaces. This is a issue with low priority.
When someone else takes over the project or it needs refactoring and feature upgrades it would be necessary having this mock upp to date. Faster development when running the environment locally. But this has fallbacks, every change to the production api will have to reflect on the mock server. Maybe less detailed data should be generated to only satisfy the edge cases? Smarter auto-generating methods should be developed that doesn't break over time. I really hope I get the time to attend this issue.

#### Any obstacles in our way?

Problem with data constraints not being what was promised. Remember the column that was separated by ':' and '@'? Sometimes the names included '@'. This should not be allowed! The users we have been provided has a lack of data to fill every part of the application and that makes it hard to test. For next week our Microsoft AD accounts will be activated and filled with the data needed for the application (fingers crossed!).

#### Reverser Proxy

Too much code is written in the dotnet portion of our client application. All we need is to proxy the request/response. Consulted my colleague and discussed [Microsofts Reversed Proxy](https://microsoft.github.io/reverse-proxy/articles/direct-proxying.html) library. This is going to remove 60 - 80% of the code we written in that project by adding a extension method to our startup file. Making this a high priority work-item that hopefully will be started next week.

This week I also made a order of two [RPi Zero W:s][1], a [RPi Pico][2] (Raspberry Pies first microcontroller!!!) and a longer [camera cable][3] for my 3D-printer. It's time to prove some concepts I have been thinking off lately. Hopefully it will arrive early next week.

Also decided what my Final Examination project should be. New article series coming soon!

[1]: https://www.electrokit.com/produkt/raspberry-pi-zero-w-with-header-unsoldered/
[2]: https://www.electrokit.com/produkt/raspberry-pi-pico/
[3]: https://www.electrokit.com/produkt/flexkabel-for-raspberry-pi-kamera-610mm/

**Until Next week. Take care and code creatively!**
