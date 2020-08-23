---
layout: post
title: Intellisense on Solutions
---

So I just started a new project [PiCarDash][1], created a PoC with some basic elements. Later I wanted to make it more robust and easier to build on. I started to refactoring and made some classes and folder to make a solid structure for the application.
Suddenly the Intellisence stopped working, figured that I would try without it for a while, but after just 5min I realised how much it was helping me before (how could you live without auto-completion!). I was constantly making typos which lead to build errors, and that was very time-consuming. 

I thought about the changes that I made preciously, ran *dotnet restore* and fixed my reference errors but still no intellisence (renamed some files and namespaces when refactoring). I started recognizing this issue from a project not long ago.

```
parent --
         +-- src -- 
         |   +-- project
         |       +-- Main.cs
         |       +-- Program.cs
         |       +-- project.csproj <-- Made changes for reference errors
         |   +-- ...
         +-- docs
         |    +-- ...
         +-- parent.sln <-- My mistake is in here
```

When I open up a project I always open the parent with the solution file in VS Code.
That makes intellisense look at the projects listed in that file. In my case I forgot to change the referencing project paths when I refactored. I also ran the project seperatly (the .csproj file in child project) and thus was not getting errors from solution file.

These tiny mistakes are things that make me wanna scream out loud and when I figure it out I laugh silently and think for myself that I'm the stupidest human alive!

I would like to send my gratitudes to all contributors for the [VS Code Extension][2] :pray: . Your contributions have made me a less frustrated programmer!


[1]: https://github.com/wiseby/PiCarDash
[2]: https://github.com/OmniSharp/omnisharp-vscode/graphs/contributors