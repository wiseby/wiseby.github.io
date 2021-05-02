---
layout: post
title: "Centiro Internship Week Twenty-One"
categories: [The Internship]
---

**The Monday Feeling**

Talked a bit about how much time we got left on our internship, not even a month left, and that includes the last week of presentations for the class.
Need to wrap this up soon if we should have something to handover.

The energy was at a decent level for this week to turn out as a success. Didn't have much of a clue on what the week was to bring us.

**What Happened?**

No new features implemented more than some enhancements for already existing ones. The focus was on hiding things depending on role for users. I took on the task to refactor the ClientApp. I had done some reading and researching on how to build bigger enterprise Angular apps. My conclusion was to develop features with container components according to the following articles:

- [6 Tips & Practices by Tomas Trajan](https://medium.com/@tomastrajan/6-best-practices-pro-tips-for-angular-cli-better-developer-experience-7b328bc9db81)
- [Slides by Loiane Groner](https://slides.com/loiane/10-angular-tips-modules-vscode-and-best-practices)
- [Best practices for a clean and performant Angular application by Vamsi Vempati](https://www.freecodecamp.org/news/best-practices-for-a-clean-and-performant-angular-application-288e7b39eb6f/)

My biggest problem was all services injected to most of the components. This made the app very messy. The idea behind following the practices in these articles is to make as many components as dumb as possible.

I've dug a hole. That's the answer to why I need to do so much refactoring. My knowledge has grown and I understand now how things can get complicated when the architecture is wrong. So I need to do something about that now! I want it to be easy adding new features in the future that doesn't lead to unwanted behaviors and side effects.

Many hours later the new architecture was in place and the process to make components dumber could start.

It is my intension to be proud of what I produce and a commitment to this line of work I have chosen.

Read some about state too. State in a frontend application is a real headache! I think of state as my kids without leash in a candy store! Eating everything and turning into sugar-rushed monsters! That is a topic for another day.

There are big changes in the workplace. Management is shaking all Centiro around to make place to grow. This results in new sectors and DM:s to manage them.

**Final Thoughts**

I've learned so much this week, as it comes to frontend development.

Soon I get payed doing this!

Next week we are following up on the architecture part and I could probably show you some code from my own private projects.

**Until Next Week. Get a haircut!**
