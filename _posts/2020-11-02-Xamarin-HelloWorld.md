---
layout: post
title: "Cross-Platform development with Xamarin Forms"
category: [.Net, 'As A Student']
---

Hello again! Long time now see.

It's time for another post and this time we will be talking about Xamarin.
Xamarin is one more tool from Microsoft enabling us to make cross-platform applikations mainly 
focusing on mobile devices as iOS and Android but also desktop applications in form of UWP (Universal Windows Platform).

For the last couple of weeks (about 6-7 in the time of writing) I have been attending a 
course that's part of my education program. This course is delivered by a company named [MissMess](www.missmess.se).
The course was made so that we had a better understanding of what it takes to produce a product with the tools provided by Microsoft.

With Xamarin Development comes Visual Studio 2019 and all its DevKit Packages relating to Xamarin. 
Its quit a environment to develope apps. I'm used to install a sdk and start typing. 
Microsoft have put alot of effort making it as easy as possible to get started, and with all the right tools I was ready to start coding!
The installation went smooth and I was up and running with a template after maybe 15 minutes.

I made the first mistake wondering if this was possible to accomplish on a linux machine (Tried building it from source with no luck!). 
But unfortunatly there was no binaries available and no plans for it in the future to maintain so many different distributions of linux. 
There will probably be some workaround in the future.
The community around this is huge so I hold my fingers crossed!

So what are my thoughts about the subject? I was amazed! I never belived that I would do a mobile app, but now when I got a taste for it, 
I would probably not turn down a job as a app-developer. There is something special about making software you can hold in your hand.

Xamarin Forms was to me very natural to use because I can write programs with my favourite language C#. 
I can also use many of the packages I'm familiar with that are built upon NetStandard.

### Building the UI

XAML (Xtendable Application Markup Language) was also alot simpler to use than HTML, alot more restriktive when it comes to design but easier to get going fast.
There is this great thing called HotReload in Visual Studio when writing XAML to design the app. 
This enables you to debug the application and make changes to the design and automatically reload the interface on the device/emulator your running.
This makes it super easy testing out all the elements to get the correct design, look and feel with instant feedback. 
This is great if it worked all the time!
I had quite some struggle with this functionality because it's tech that allways in motion, 
features are added bugs is fixed and new concepts are introduced.
I dont know if I could blame my hardware but sometimes the emulator stoped working and wouln't respond to hotreload.
It's recommended to have extra RAM and a processor with virtualization support to run the emulator smoothly and to compile your application fast.
Most of the time I was just sitting there waiting for the app to build and run to see what outcome my code would end up with.
One time I even had to delete and reinstall my emulator.

Steps to fix some issues not related to code:

* Clean Solution
* Rebuild Application
* Update Packages
* Start removing XAML elements

I figured out that it was simpler building the application one step at a time. As our teacher told as all about the "Walking Skeleton" 
witch in this case was the simple sketch on a piece of paper that later became our XAML. Fill the UI with dummy data without any thougt of backend stuff.
I could then focus on how each element should be designed.

### Using the MVVM Pattern

To follow some of the best practicies for making Xamarin Applications the MVVM pattern was introduced. 
With the Model Binding capabilities that Xamarin Forms provide makes this pattern obvious to use. 
I'm getting more and more confertable with the SOLID principles and one thats particularly close to me is the Dependancy Inversion Principle and the idea of 'Loose Coupling, High Cohesion'.
With MVVM we can take some of the responsibility focused at backend operations to a class that has no idea how to represent itself in the UI.

The biggest problem when using Xamarin is the step of debugging. It's a pain in the ass pointing directly at the problem. Most often this is in the CodeBehind-file or ViewModel.
When I was in need of some debugging I often made a button with a command so I could break and check the state of my program witch was a little tedious at times.
By moving as much code not relatied to the view we can now build robust tests to catch these bugs without running the app at all. You can even use TDD (if your into that kind of stuff).

### Native Features

For my own sideproject I was intrested in making a application that took advantage of hardware, such as camera and storage (these gadget we all have are packed with alot of magic for those who didn't know! ;)). 

Xamarin comes with alot of goodies when you start up a new project. Xamarin.Essentials are all the extra stuff you would need to interact with platform specific features. In my case I needed a preview of the package to use the MediaPicker class to browse device gallery and take photo/video with camera.

There are tons of other features you could use like:

* Accelerometer
* Clipboard
* File Picker
* Geolocation
* Flashlight
* ......
* ...

Too just mention a few

Another package I used was the sqlite-net-pcl so I could run a local sqlite database to store information. This combined with a REST-service would make it possible to have the application running both off/online.
 
### Conclusion. What have I learned?

* Practicing events
* New patterns including MVVM, Command
* Write code once, run on multiple devices
* Start small (KISS)

We were using Xamarin Forms 4.8 and not long after or even during the course Xamarin 5 was released. In the near future there will be some changes in the .Net world.
The big project of unifying .Net with .Net 5 (under this umbrella we have .Net Core, .Net Framework, Xamarin, Mono) will be a big step and I'm sooo exited, unfortunatly Project MAUI is not to be released together with .Net 5 but probably towards .Net 6.
What I heard is that CLI tools will be available when developing Apps so I have more freedom using witchever IDE pleases me best (VS Code FTW!).

The things I have been struggeling the most is the design/UI part. It was the same when we had our WebDev course. 
The education-program aims at backen development but in my eyes there is alot of UI elements and design aspects.
Maybe we should discuss and rename the hole program. My suggestion "FullStack .Net Development"? 
It feels like we are only scratching the surface of popular technologies.

All in all this was a realy fun course and it made me eagerd to find out more about this wonderfull product.
Maybe I publish my own app in the near future!

Thats all fokes. 

Feeling lucky? Why not try [Xamarin](https://docs.microsoft.com/en-us/xamarin/get-started/) today?!

Next post coming soon!