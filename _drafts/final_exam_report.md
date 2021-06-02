---
layout: post
title: "System-Developer .Net Thesis"
categories: ["As A Student"]
---

### Summary

Hackers-HomeAuto, a simple, light weight home automation system for everyday use.

It's not that classic system that dims the light with voice commands, or starts the coffee machine 15 minutes before your alarm clock rings.
It's also not a cloud platform, It's supposed to run locally on your home network isolated from the outside world.
It's more like a home health system, reading the status of your home. If the system had a voice it would be possible to ask something like "Hello Home. How are you feeling today?" and the answer would be "I'm feeling fine. Nothing out of the ordinary to report" or something like that.

The main purpose of this project is to monitor my home and to build statistics on data collected from sensors, making it possible to show statistics on data impacting energy consumption and environment status monitoring. Storing history so that statistics can be visualized over long time period's. How has the temperature relations advanced over the past five years? That is a question that will be answered with this system.

**Not A Cloud Service**

As I mentioned, this system is not intended to run on the cloud. It's supposed to run on a server in your own home. No external party that handles your data.
It will run on any server that supports the dotnet runtime specified in the documentations.

The server I always think of when hosting something like this is the Raspberry Pi Single Board Computer. It's affordable for everyone.

The hardware is a mixture of Raspberry Pies, Arduinos and other micro-controllers that utilizes a wider range of sensors for home-automation purposes. The Server part of the project is focusing on software written in C# running a .NET environment. As for the nodes that are smaller and mostly battery-powered, are running code written in languages suitable for micro-controllers. I'm planning to write programs for these smaller devices in Lua, C++ and Python/MicroPython. Raspberry Pi Zeros are used when heavier loads like video-surveillance should be implemented. The RPi Zero is based upon a ARMv6 and is there by not compatible with .NET runtime, Python will be used instead with the use of Flask which is a MicroWeb-Framework (communicating through http/https).

### OSS - Open Source Software

I have always dreamed of having a popular github repository. I have seen many other repositories with beautifully built documentations. It seems to me that these repos tend to work much better than others that lacks structure.

This repository will be a base template, implementing best practices and concepts that is relevant in the early stages when learning to write software. It should be easy to contribute and expand, tailored to fit any home-automation need.

The project is open sourced and located at github under the repositories:

- [Hackers-HomeAuto.Server](https://github.com/wiseby/Hackers-HomeAuto.Server)
- [Hackers-HomeAuto.Node](https://github.com/wiseby/Hackers-HomeAuto.Node)

### Technologies used:

**MongoDB**

Decided to use MongoDB for all my data. It's going to be a hole new experience to add in my portfolio!
The Mongo Driver is mature enough and super easy to use, I've heard! Running MongoDB in docker with a simple docker-compose.yml straight from [dockerhub example](https://hub.docker.com/_/mongo). This composition also includes a web-administration tool that makes it easy examining the database with a web-browser.

**.NET 5.0**

.NET 5.0 is the latest version and is listed as the recommended version when starting a new project. It will soon be released as LTS (Long Time Support).
Everything you have learned in .NET Core 3.0 and later are applicable to this version.

**MQTTNet**

To communicate with smaller devices and micro-controllers I needed a lighter transport protocol than HTTP, MQTT fitted perfectly and I found this open-source project [MQTTNet](https://github.com/chkr1011/MQTTnet) which supports both client and server/broker implementations.

**HTML, Javascript/Typescript, Angular**

The frontend part of the project is built with Angular. By isolating the application inside the web-api it becomes easy to move to a separate repository later, but for simplicity it can live and be served under the api root path. When I decided in what form of user interface I wanted I considered to either build an app with Xamarin or build a web-application. My experience in Angular is far more superior than in Xamarin.Forms so I went with a web-app using Angular, this was so I could focus making my project the best I could on the time I was given, getting up and running with Xamarin again eats time that I don't have!

Drawing some basic charts with [chart.js](https://www.npmjs.com/package/chart.js). Chart.js is very potent and could produce all charts for the needs of presenting the data.

When it was time to style the webapp I made the decision of using a CSS framework. [Bulma](https://bulma.io/) was used and I could focus on other things than CSS.

### MVP Iteration

Keeping everything in the right scope was key to hit the date for having a product ready on time.
For my first iteration, I'm was to implement temperature readings and a frontend to **view and administrate the data**. As simple as it could get!

Building a foundation for a system that should live through many iterations is not an easy task. 

**The process of system functionality:**

- Reading Sensor 
- Publishing Data
- Server Intercepting Data
- Client Fetching Data from Api
- Visual Presentation of Data

### Planning and Execution

**TDD**

Test Driven Development was one of those things I wanted to practice. Using the knowledge from our testing course and referencing the book we used, testing would be easy to get started with. Using frameworks as _XUnit_, _FakeItEasy_, _AutoFixture_ and _FluentAssertions_ would make all my tests easy to maintain and cover most of my code. As we where taught, tests are supposed to be part of the documentation. Reading the tests should describe how the system works. 

The Mqtt-Server part was developed explicitly with TDD because I knew exactly what kind of behavior I wanted. With the other parts of the code I skipped tests when time was running out. When I want to build tests I want them to be solid and have a purpose. Until I figured out why I need a test there is no point writing one. 

**Github**

I'm hosting all of my code on Github to enforce the open-source values. The projects planning tools is also hosted on Github with Project/Boards that are setup on each Repository respectively. CI (Continuous Integration) pipelines are enabled on the Hackers-HomeAuto.Server project with Github Actions to build and test the application when a merge to main is triggered. This is to maintain the build process as a central part of the application and reduce bugs. It will add more value when others join and contribute.

Github Project Kanban style board:

![Github Kanban Board](/assets/images/GithubProject.png "Github Project Kanban")

When working in iterations (Scrumish) there are some features missing on Github, but I found _MileStones_. As an example I set up a Milestone for the deadline of the assignment.

![Github MileStone](/assets/images/GithubMilestone.png "Github MileStone")

You don't set up a deadline with this feature but it's a clear goal and you can link Issues to it so that a progressbar appears. It's always nice to have some kind of visual marker on progress. It pushes you to go further!

**Generic Data**

A red thread in this project has been that the data from all IoT devices should be in a generic format. JSON format with flat simple key/values. 
A IoT device could be equipped with a bunch of sensors and they would be represented with a key and value for each. It's up to the client to map these values and set there definitions. This makes the nodes stupid and there only job is to gather data from sensor and sending them to the server.

**Server Focus**

This system comes in two parts on my end. A Server and a Node Project. My intention for this Finale Exam Project is to focus my work on the Server part.
Four weeks is a short time developing something in this size all by myself. My opinion is that the Server project is more than enough to show my capabilities and cover everything needed for the highest grade possible.

**Documentation**

A well documented project can be hard to maintain, but for this project documentation is a big part of the contribution. New developers and curious tinkerers should be able to walk through the documentation to get up and running without any hassle! Step by step instructions should guide you on how to expand it.
On github the README is the most important piece and the first thing that you see, this should be the entry-point to all documentation. There is also a Wiki-tab that I'm going to look deeper into.

Projects front door:

![Projects README](/assets/images/RepoDocumentations.png "Projects README")

**Common Workflows**

Sometimes when there is a problem that is hard to solve I have practiced a number of methods. Pseudo-Code and my favorite FlowCharts.
I also started using Sequence-diagrams. They offer a bigger picture and describes a specific process in a system. 
This is an example for how I figured out how to initialize a Node with Rest-Api behavior.

![Node Init Sequence Diagram](/assets/images/Node_Init_Connect_Success.png "Node Init Sequence Diagram")

You can relate to it if you ever have configured a Wifi extender/hotspot.

**The hard parts**

The hardest part is getting everything up and running with the right architecture in place.
It's like bootstrap phase, when everything is in place, things would get much clearer when working on a new feature.

- Load configuration
- Setup Dependency Injection with Autofac
- Setup logging with Serilog
- Mapping Configuration for AutoMapper

A lot of these dependencies had seamless integration to Asp.Net application with extension libraries available as nuget-packages.
This has taken some time to get right but is now working as it should. 

You better get used to reading documentation because you are not going to write all code yourself, you are going to use other peoples code. My bet is that it comes with a handbook, if it has a handbook, it's probably something that is supposed to be used by others. 

Sometimes it gets hard focusing on single issues, one thing leads to another and all of a sudden you find yourself far away from the starting line.  
It's all about having the proper conditions when solving a problem, are you missing anything, you have to take a few steps back and make the foundation ready to build that new shiny feature!

Discovering parts that is missing and evaluating on the most important steps to take and when to take a shortcut is also something that comes up frequently.

Struggling with the usual data structure to be sent from my API. I got my hands dirty and started investigating if there was a standard for this kind of thing, and yes there was. There was something called [JSON:API Specification](https://jsonapi.org/) which covered all of my questions. It was a bit overwhelming and a lot to take in, but ended up using the more strict specs that where described as a "Must".

I often find myself magically trapped in reading documentation! I'm trying my hardest to stick with things I already know, but it's hard, wouldn't you want to implement all the new exciting technologies you read about right know!

The data collections could be huge when it's gathered to show statistics. Restricting clients publications to server should be limited some how. Maybe with a default filter. One fix could be to configure a nodes definitions to store how often a reading should be persisted into the database, all latest temperature readings already has a place inside a node object, so live updates should be supported this way even if I decide to persist let's say one reading every hour?

Plans doesn't always end up as you thought. I had to abandon a bunch of interesting ideas and technologies.

- Mediator
- Vertical Slicing
- SignalR
- Dynamic Forms
- Frontend Testing
- End To End Testing

**Features in coming iterations could be:**

- SignalR could be nice so that the UI could be updated when states change in backend. (notifications, live updates on readings, etc).
- Adding Microsoft.Extensions.Hosting to MqttServer project as with [this](https://dev.to/krusty93/net-core-5-0-console-app-configuration-trick-and-tips-c1j) articles content would be something to look into later.
- Implement a [MQTT Client](https://www.npmjs.com/package/mqtt) in the WebApp. Easy debugging and a admin-tool.
- Following [JSON:API Specifications](https://jsonapi.org/) and integrating a [serializer extension](https://github.com/codecutout/JsonApiSerializer).
- Guides on publishing to a production server (Raspberry Pie).
- Extend documentations with a Wiki
- Expand Node IoT unit library with more variations of sensors.
- Improve test coverage
- Improve UI with more options on how to visualize data. Selecting different sensors to compare etc.

I could go on and on but in the end I'm going to run this system and implement features as I need it. It's like User Acceptance Testing but in a scenario where I have all teh roles.

**Final Thoughts**

I should have worked with a wire-frame to design my UI and pinpoint all my API needs before I got started. I'm not very good at creating user-friendly interfaces, but this system was going to be used by me and I figured that I'll work on improvements on iterations to come. 

There are so much code out there! Using brilliant tools and libraries that other developers have created makes it easy for me to focus on what really matters!

In the end, If no one uses your code, there where no reason to write it in the first place!
I don't know if any one else will use it, but I will definitely make this work for me! 

**Until next post. Make a contribution to the OpenSource community!**
