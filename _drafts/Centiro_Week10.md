---
layout: post
title:  "Internship Week Ten"
categories: [The Internship]
---

Mondays starts with planning. 
Good practice to talk about the weeks events and reflect on what happened previous week and the progress. Updating the Azure Board, 
some work-items need more time and transfers between sprints. The backlog consists of user-stories created by our team before we got the job, and some of them are a little bit obscure.
We tend to ignore them, and created our own stories that where relevant to requirements from the team.

How far have we come?
As of this week we are putting much of the pieces together. Moving over to implement the new api in our client application. Changing the code in that part of the project was fairly simple and that must be a sign of code written the right way. Some methods needed some refactoring because it took to long figuring out what it did, most of the time the method did more then one thing (remember Single Responsibility Principle!).


What is the delays?


Any problems we need to address?

Problem with data constraints not being what was promised. Remember the column that was separated by ':' and '@'? Sometimes the names included '@'. This should not be allowed!


Implement Direct Proxy with YARP

Too much code is written in the dotnet portion of our client application. All we need is to proxy the request/response. Consulted my colleague and discussed [Microsofts Reversed Proxy](https://microsoft.github.io/reverse-proxy/articles/direct-proxying.html) library. This is going to remove 60 - 80% of the code we written in that project by adding a extension method to our startup file.