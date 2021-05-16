---
layout: post
title: "Finale Examination Project Kick-Off"
categories: ["As A Student", "Hackers-HomeAuto"]
---

### Summary

Everything we have learned gathered into a single project. It's time to show everyone what I've learned the past 2 years! The project is called **Hackers-HomeAuto** (Project name under development😉) and is a DIY Home Automation system.

The hardware is a mixture of Raspberry Pies, Arduinos and other micro-controllers that utilizes a wider range of sensors for home-automation purposes. The Server part of the project is focusing on software written in C# running a .NET environment. As for the nodes that are smaller and mostly battery-powered, are running code written in languages suitable for micro-controllers. I'm planning to write programs for these smaller devices in Lua, C++ and Python/MicroPython. Raspberry Pi Zeros are used when heavier loads like video-surveillance should be implemented. The RPi Zero is based upon a ARMv6 and is there by not compatible with .NET runtime, Python will be used instead with the use of Flask which is a MicroWeb-Framework (communicating through http/https).

The main purpose is to monitor my home and to build statistics on data collected from sensors, making it possible to show statistics on data impacting energy consumption and environment status monitoring.

I'm also trying to make this project as a base template, implementing best practices and concepts that is relevant in the early stages when learning to write software. It should be easy to contribute and expand, tailored to fit any home-automation need.

Could it maybe be used as an assignment and or test to implement something into the project? Or maybe identify a issue and fix that?
This was something I wanted to have as an exercise myself, but couldn't find any good projects.

The project is open sourced and located at github under the repositories:

- [Hackers-HomeAuto.Server](https://github.com/wiseby/Hackers-HomeAuto.Server)
- [Hackers-HomeAuto.Node](https://github.com/wiseby/Hackers-HomeAuto.Node)

At the time of writing this post I'm one week out of four into the assignment schedule with a bit of a head start.

### Technologies used:

**MongoDB**

Decided to use MongoDB for all my data. It's going to be a hole new experience to add in my portfolio!
The Mongo Driver is mature enough and super easy to use, I've heard! Running MongoDB in docker with a simple docker-compose.yml straight from [dockerhub example](https://hub.docker.com/_/mongo). This composition also includes a web-administration tool that makes it easy examining the database with a web-browser.

**.NET 5.0**

.NET 5.0 is the latest version and is listed as the recommended version when starting a new project. It will soon be released as LTS (Long Time Support).
Everything you have learned in .NET Core 3.0 and later are applicable to this version.

**MQTTNet**

To communicate with smaller devices and micro-controllers I needed a lighter transport protocol than HTTP, MQTT fitted perfectly and I found this open-source project [MQTTNet](https://github.com/chkr1011/MQTTnet) which supports both client and server/broker implementations.

**Angular**

The frontend part of the project is built with Angular. By isolating the application inside the web-api it becomes easy to move to a separate repository later, but for simplicity it can live and be served under the api root path. When I decided in what form of user interface I wanted I considered to either build an app with Xamarin or build a web-application. My experience in Angular is far more superior than in Xamarin.Forms so I went with a web-app using Angular, this was so I could focus making my project the best I could on the time I was given, getting up and running with Xamarin again eats time that I don't have!

### MVP Iteration

Keeping everything in the right scope was key to hit the date for having a product ready on time.
For my first iteration, I'm going to implement temperature readings and a frontend to **view and administrate the data**. As simple as it could get!

**TDD**

Test Driven Development was one of those things I wanted to practice. Using the knowledge from our testing course and referencing the book we used, testing would be easy to get started with. Using frameworks as _XUnit_, _FakeItEasy_, _AutoFixture_ and _FluentAssertions_ would make all my tests easy to maintain and cover most of my code. As we where taught, tests are supposed to be part of the documentation. Reading the tests should describe how the system works.

**Github**

I'm hosting all of my code on Github to enforce the open-source values. The projects planning tools is also hosted on Github with Project/Boards that are setup on each Repository respectively. CI (Continuous Integration) pipelines are enabled on the Hackers-HomeAuto.Server project with Github Actions to build and test the application when a merge to master is triggered. This is to maintain the build process as a central part of the application and reduce bugs. It will add more value when others join and contribute.

**Server Focus**

This system comes in two parts on my end. A Server and a Node Project. My intention for this Finale Exam Project is to focus my work on the Server part.
Four weeks is a short time developing something in this size all by myself. My opinion is that the Server project is more than enough to show my capabilities and cover everything needed for the highest grade possible.

**Documentation**

A well documented project can be hard to maintain, but for this project documentation is a big part of the contribution. New developers and curious tinkerers should be able to walk through the documentation to get up and running without any hassle! Step by step instructions should guide you on how to expand it.
On github the README is the most important piece and the first thing that you see, this should be the entry-point to all documentation. There is also a Wiki-tab that I'm going to look deeper into.
