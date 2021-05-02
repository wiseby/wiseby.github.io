---
layout: post
title: "Centiro Internship Week Seven"
categories: [The Internship]
---

First Monday 2021! Rallying the team and gets up to speed on what everyone has been up to for the holidays.

Had the time to think over the situation of how work is being done at Centiro.
As a intern I have no supervision which I would prefer when I'm not sure how things should be done. I really hope that someone tells me if I'm doing something wrong, or should work in a different way.

One teammate should have helped us to get a project up and running in the beginning of november but it's not done yet.
Just before the holidays he tells us to get started on the backend when we get back, but there's no working project to get started on.
Everything seems a little uncertain to me. We are expected to make magic happen out of thin air!
It seems that there is still problems with starting up a new WebAPI project with git. The idea was from the start to build a separate WebAPI project moving away from TFS replacing it with GIT.
Hopefully this would be possible next week or we had to add another version of the old API in the existing codebase.

Read some documentation about .Net Configurations from [Microsoft Docs](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-5.0).
Started to watch a course at PluralSight on Azure CLI and how we could get azure secrets into ASP.NET applications.
Trying to understand how and where to store application secrets/settings.

Found this to store settings when running programs on the local machine:

```
dotnet user-secrets init    // Initializes and adds secret to project
dotnet user-secrets set "secret key" "secret value"     // Adds a secret to project
```

The default builder took care of the rest!

Started working more with Visual Studio Pro and how to move around fetching SourceCode from TFS Repositories.
Finally got a API built and run successfully! Now we could review some code trying to figure out how to build our API in a modern way using Vertical Slicing.
This involved research about mediator pattern, adapter pattern and SqlBuilder, Dapper, etc.

This Vertical Slicing feels really nice to my ears. The problem writing code today is the obsession to make everything so generic and complex.
It's so easy getting lost in the code yet alone for class inheritance. With this method we could write feature specific code in one place where the flow was easy to follow.
This method is maybe not suitable for more complex operations but for CQRS operations this was truly the right way to go.

Summary of the week.
Documentation reading and dissecting source code. Ending this week with more knowledge and confidence completing my tasks!
Next week will be more code productive.

**Music tip of the week, Ola Englunds Solo Album 'Master Of The Universe'! Writing code with Ola makes my day!**
