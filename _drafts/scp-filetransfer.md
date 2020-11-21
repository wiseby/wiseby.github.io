---
layout: post
title: "Secure Copy Filetransfer with SSH"
category: []
---

SSH is a wonderful thing and I use it all the time working on servers in my home.
With ssh configuration setup for my user it's very easy connecting to whatever server I want.

Easy as making pancakes!






The easiest way of transfering files over network is probably with the tool scp.
scp stands for Secure Copy and uses ssh protocol.

The following command copies a project folder recursivly to a destination server with rsa encrytion key (always use keys for validation! No root login!):
```
scp -r -i [path_to_rsa_key] file_to_tranfer [user@host]:destination
```