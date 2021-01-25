---
layout: post
title:  "Internship Week Nine"
categories: [The Internship]
---

This was going to be a week with a mixture of vacation, board-meetings and code-reviews.
No day was the other like and it flew by with an incredible pase. 

Me and Johan focused on different parts of the application where I worked more with the frontend implementing the new API and Johan made further development and improvements on the backend. More confusion was added when exploring the depth of the database and additional attributes/references, no consistency in relationships at all!

We learned that different collections have there weaknesses and strengths, when to use the other according to situation. 
Right now we are trying to make everything work, later we need to make some refactoring so operations are more efficient.
The goal of refactoring is to make the code more readable, efficient and testable.
I figured out that when you have the result that you want you could later refactor it and see if the result stay's the same.

One thing that I want to fix is the part of the client application that serves the angular application and works as a facade. This means that it handles all request/responses made from the client. The facade then makes new requests to the destined API packages data as query params and body. The best solution would be to use the controller as a proxy, forwarding the requests and responses, the only thing that needs to be added are the base url, Accept header and a Bearer Token.

An API works great as a adapter where the complexity of the database is hidden behind a user friendly interface.
When designing a API you should ask yourself how you want to use rather then how the implementation is going to be.
Some changes along the way made the API straight forward to use.

Our mentor/team-member checked in and wanted to see how everything was going. He reviewed some code and was pleased with our progress. He had some feedback and guided us on how to make the code better, and this was great. We learned a lot and we where able to correct those mistakes without problems.

Today we are going to have a demo having a partially completed application on both back-frontend. 