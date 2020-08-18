---
layout: post
title: "My First Post!"
date: 2020-08-18 14:07:17 +0200
---
This is awesome! Creating a webpage under 30min (including reading documentation)! I heard alot about Jekyll but never tried it, so here we go!

**Here I can put:**
* All thoughts for you all to see.
* Probably alot of solutions to problems I've had.
* Code snippets (OMG! soo much code! MarkDown makes it a blast!) 
* I think it's going to be alot of serverside managment content to (We'll see).

I'm dedicating this page for software development and for it to be internationaly available and written in english (vill ni läsa andra artiklar på mitt modersmål går det bra [här]({{site.web_site}})).

Okej! Okej! Let's make a code snippet!

```csharp
var pizzas = new List<string> {
    "vesuvio", 
    "margerita", 
    "calzone", 
    "batman(yes it's a pizza!)"
    };

for(int i = 0; i < pizzas.Count; i++) 
{
    Console.WriteLine(pizzas[i]);
}
```

**Look at that!** Beatifull!

How didi I make this possible? Followed the steps in this [guide](https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll). Had some trouble with dependencies so i stumbled into this site [StackOverflow](https://stackoverflow.com/questions/9725679/an-error-occurred-while-installing-nokogiri-1-5-2) (never happend before, am i right!?) 

Installed missing packages, because everyone runs a linux machine!?
```shell
sudo apt install liblzma-dev zlib1g-dev
```

And everything worked as a sharm.

Rather short post but it's a start. Now I need to work on my profile page for this awesome site!

Take care now, bye bye then!