---
layout: post
title: "Finale Examination Project"
categories: ["As A Student"]
---

### Summary

Everything we have learned gathered into a single project. It's time to show everyone what I've learned the past 2 years! The project is called **Hackers-HomeAuto** (Project name under development😉) and is a DIY Home Automation system.

The hardware is a mixture of Raspberry Pies, Arduinos and other micro-controllers that utilizes a wider range of sensors for home-automation purposes. The Server part of the project is focusing on software written in C# running a .NET environment. As for the nodes that are smaller and mostly battery-powered, are running code written in languages suitable for micro-controllers. I'm planning to write programs for these smaller devices in Lua, C++ and Python/MicroPython. Raspberry Pi Zeros are used when heavier loads like video-surveillance should be implemented. The RPi Zero is based upon a ARMv6 and is there by not compatible with dotnet runtime, Python will be used instead with the use of Flask which is a MicroWeb-Framework (communicating through http/https).

The main purpose is to monitor my home and to build statistics on data collected from sensors, making it possible to show statistics on data impacting energy consumption and environment status monitoring.

I'm also trying to make this project as a base template, implementing best practices and concepts that is relevant in the early stages when learning to write software. It should be easy to contribute and expand, tailored to fit any home-automation need.

Could it maybe be used as an assignment and or test to implement something into the project? Or maybe identify a issue and fix that?
This was something I wanted to have as an exercise myself, but couldn't find any good projects.

The project is open sourced and located at github under the repositories:

- [Hackers-HomeAuto.Server](https://github.com/wiseby/Hackers-HomeAuto.Server)
- [Hackers-HomeAuto.Node](https://github.com/wiseby/Hackers-HomeAuto.Node)

At the time of writing this post I'm one week out of four into the assignment schedule with a bit of a head start.

### Technologies used:

- **MongoDB**

  Decided to use MongoDB for all my data. It's going to be a hole new experience to add in my portfolio!
  The Mongo Driver is mature enough and super easy to use, I've heard! Running MongoDB in docker with a simple docker-compose.yml straight from [dockerhub example](https://hub.docker.com/_/mongo). This composition also includes a web-administration tool that makes it easy examining the database with a web-browser.

- **.NET 5.0**

- **MQTTNet**

- **Angular**

  The frontend part of the project is built with Angular. By isolating the application inside the web-api it becomes easy to move to a separate repository later, but for simplicity it can live and be served under the api root path. When I decided in what form of user interface I wanted I considered to either build an app with Xamarin or build a web-application. My

- **Python**

- **ESP-01**
  - Lua
  - C++
  - MicroPython

### MVP Iteration

Keeping everything in the right scope was key to hit the date for having a product ready on time.

- **TDD**
- **Github**
- **Server Focus**
- **Documentation**
