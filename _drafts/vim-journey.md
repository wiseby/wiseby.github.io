---
layout: post
title: "My Vim Journey"
categories: ["Editor"]
---

### Creating windows and files

Opwn a new file in split to current horizontal `:new` 
Open a new file in split vertically `:vnew`

### Commands and Macros

`:!dotnet build` runs a command with a !

Create a command `:command Build :w | !dotnet build`
This creates a command that saves the current file and builds the dotnet project.
The pipe/bar is used to seperate and chain multiple commands.
If the command already exists you can append ! to override it (:command!)

### Multiple windows

Move around windows with Ctrl - ww

### Multi-Tasking

Use Ctrl-z to put halt the program to background. Do anything else and then return to vim with the `fg` command.
