---
layout: post
title:  "Internship Week Eleven"
categories: [The Internship]
---

Working alone this week when my classmate woke up with fever this morning.

Started to implement Direct Proxy on the client app. Worked great and could remove all controllers and services.

Made some changes in the api where endpoint urls where a bit funny looking. Noticed how easy it was changing code with the architecture we used.

Getting better and better at breaking tasks apart. It helps me focus and if I notice other things in the code that needs fixing I simply create a new work-item for it to come back for later. 

#### There are more collections than Lists!

Working on how to use different collections in the term of relations in objects.
Used LookUp collection and Dictionary. Got some feedback about the use of LINQ foreach extension method and why it's a poor choice to iterate through large datasets. The official language constructs using the foreach has a much better performance impact. My mentor told me to read this [article](https://twitter.com/korifey_ad/status/1141257997886337024) that explained the problem with LINQ:s foreach extension vs foreach statements.

#### Pagination

Pagination is one of the topics of the week. The result set for a view is so huge that there is a good idea to limit the response to the client. This enables the backend to take chunks of the result according to a pagination object (pageSize, currentPage, search criteria, etc) and filter/limit the result set. A fun part implementing and utilizing some new SQL Server methods that I was unfamiliar with.

One thing that I learned during the Database course is the performance of queries. I really need to investigate how the queries can be improved with the help of Query Execution Planner. Thankfully our teacher in that course had it all covered 😃

#### Code Reviews

This week I'm in need for a stand in code reviewer when I'm making Pull Requests.
It would be nice having a developer who has experience in angular to add productive feedback for once. Sent out a request for reviewers to the project and got a developer from india to take on the mission. He is part of Centiros frontend team that does much of the web-applications and design system stuff.
Hopefully he will give me the feedback I deserve! 

#### GIT

Starting to get a hang of how to use git more efficiently, now I'm learning the flow on how to proceed working on features when there is a pending PR. Simply make a new branch on the one waiting for approval and when it is merged to main, rebase the one your on onto main.

This weekend activity is to make a simple project for my latest purchase, the Raspberry Pi Pico!

**Until next time! Stay frosty!(because it's -20 degrees Celsius! Put your Raggsockar* on!)**

**(swedish for thicker knitted socks)*