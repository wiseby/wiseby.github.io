---
layout: post
title: "Finale Examination Project Week Two"
categories: ["As A Student", "Hackers-HomeAuto"]
---

Leaving the tests for Message interceptor for now.
Mqtt Server works as intended for first iteration. I'm really happy how it turned out, clean and simple!
Waiting to try it out with a live node next weekend. It would be nice to have the whole chain when doing a demo for the presentation.

The hardest part is getting everything up and running with the right architecture in place.

- Load configuration
- Setup Dependency Injection with Autofac
- Setup logging with Serilog
- Mapping Configuration for AutoMapper

A lot of these dependencies had seamless integration to ASP.Net application with extension libraries available as nuget-packages.
This has taken some time to get right but is now working as it should.

In the starting phase as I'm in right now, it gets hard focusing on single issues, one thing leads to another and all of a sudden you find yourself far away from the starting line. I call this the Bootstrap phase, when everything is in place, things would get much clearer when working on a new feature.
Discovering parts that is missing and evaluating on the most important steps to take and when to take a shortcut is also something that comes up frequently.

Struggling with the usual data structure to be sent from my API. I got my hands dirty and started investigating if there was a standard for this kind of thing, and yes there was. There was something called [JSON:API Specification](https://jsonapi.org/) which covered all of my questions. It was a bit overwhelming and a lot to take in, but ended up using the more strict specs that where described as a "Must".

I often find myself magically trapped in reading documentation! I'm trying my hardest to stick with things I already know, but it's hard, wouldn't you want to implement all the new exciting technologies you read about right know!

The data collections could be huge when it's gathered to show statistics. Restricting clients publications to server should be limited some how. Maybe with a default filter. One fix could be to configure a nodes definitions to store how often a reading should be persisted into the database, all latest temperature readings already has a place inside a node object, so live updates should be supported this way even if I decide to persist let's say one reading every hour?

Decided to skip MediatR, maybe implement it later. Simple Repositories injected in controllers does the trick for me this time. Jamie Bogard gets his part when using AutoMapper😉.
Creating Generic Repositories for api and for mqtt messages.
To use repositories? or not use repositories? that is the question! Final decisions where made and ended up creating some generic interfaces for repositories that could be consumed for different parts of my project. This way I could make a second version of my repositories with another kind of database (don't know yet if MongDb was the right choice, works good this far).

Drawing some basic charts with [chart.js](https://www.npmjs.com/package/chart.js). Managed by the end of the week to produce a basic chart using Angular library (ng2-charts)[https://www.npmjs.com/package/ng2-charts]. My needs is to make linear charts to see relations between different temperature readings. A really versatile tool for data presentation! It had a ton of customizations that could be tweaked. Check them all out [here](https://www.chartjs.org/docs/latest/samples/animations/progressive-line.html).

**Features in coming iterations could be:**

- SignalR could be nice so that the UI could be updated when states change in backend. (notifications, live updates on readings, etc).
- Adding Microsoft.Extensions.Hosting to MqttServer project as with [this](https://dev.to/krusty93/net-core-5-0-console-app-configuration-trick-and-tips-c1j) articles content would be something to loo into later, created a new task in my project-board.
- Implement a [MQTT Client](https://www.npmjs.com/package/mqtt) in the WebApp. Easy debugging and a admin-tool.
- Following [JSON:API Specifications](https://jsonapi.org/) and integrating a [serializer extension](https://github.com/codecutout/JsonApiSerializer).

**Final Thoughts**

I should have worked with a wire-frame to design my UI and pinpoint all my API needs before I got started.

Before I finish this projects first iteration, I would want to test publishing and add steps to deploy the application. It's maybe not possible to accomplish this til friday next week. I also want to test publishing a package through Github, that is up to date with master build by creating and publishing a artifact from action/pipeline.

There are so much code out there! Using brilliant tools and libraries that other developers have created makes it easy for me to focus on what really matters!
Together we create a new future.

**Until next post. Make a contribution to the OpenSource community!**
