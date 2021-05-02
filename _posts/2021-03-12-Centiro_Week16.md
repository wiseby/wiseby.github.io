---
layout: post
title: "Centiro Internship Week Sixteen"
categories: [The Internship]
---

Worked most part of the week on the Client. Refactoring to use modules with _separation of concern_ in mind. This made the code much easier to read.

Got some correction to make proper use of REST methods. GET should be used when querying results and fetching data, It should also leave the resource unchanged.
The filtering and pagination where going to be added as query-parameters in the url.

Routing using urls to make it possible to open app in a second tab and sharing urls to others was also a very common workflow.
Many things starts to work automatically when we enabled navigation through the url. Moving between pages using built in features by the browser (Go Back, open in new tab, etc) brought bonus features like history, memory on scroll content. It reminds me how much work a web-browser does.

When it was time for our weekly demo, the question was raised whether pagination would impact performance for larger datasets. Logging in to the system with an account that had lots of data, the size of the response didn't get much bigger than 2 MB. This was no problem and the response time was quit low. We considered to make pagination and related functions in the client (but what happens if someone else makes a implementation to the api?).

There have been some bug searching and refactoring made to the backend.
Every time I look at the code and need to make changes, I make it a little cleaner and easier to read. It's a very good habit revisiting code to see if you could understand it in a reasonable amount of time. If not, you probably need to make some refactoring.

We also had trouble making check ins when previous builds in pipelines failed at the beginning of the week.
Communication when builds fail in pipelines are not that good. Who takes responsibility? I ended up contacting my mentor on how to address the issue.

### Exam Progression

**Making a mock of my api**

I'm going for a _API first_ approach when developing this project, designing the interface for the system is the key to make this project succeed.
After all this is intended to be a open-source base system anyone can make a fork of to make a more personal touch to. [JsonServer](https://www.npmjs.com/package/jsonserver) was used for the client app to mock an api. Here I could quickly set up my idea of how the interface to the backend would look like, focusing on what was needed for the different views of the app.

**The goal for my project**

The problem I would like to solve with this project is statistics and monitoring my home. Sure, switching things on/off, adjusting lights, reading motion, etc is cool but not the most important thing to me. I would like to measure room temperature and energy consumption of my home. This is so I could make my home more energy efficient. Gathering data to be processed by AI perhaps?

**Until next time! Take care now, bye bye then!**
