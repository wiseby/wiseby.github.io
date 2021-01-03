---
layout: post
title: "Secure Copy Filetransfer with SSH"
category: [Linux, Deployment]
---

SSH is a wonderful thing and I use it all the time working on servers in my home.
With ssh configuration setup for my user it's very easy connecting to whatever server I want.

Easy as making pancakes!

In my case I wanted to deploy a dotnet webapi build to my server.


The easiest way of transfering files over network is probably with the tool scp.
scp stands for Secure Copy and uses ssh protocol.

**From manual page of scp:**

> scp copies files between hosts on a network.  It uses ssh(1) for data transfer, and uses the same authentication and provides the same security as ssh(1).  scp will ask for passwords or passphrases if they are needed for authentication.
> 
> File names may contain a user and host specification to indicate that the file is to be copied to/from that host.  Local file names can be made explicit using absolute or relative pathnames to avoid scp 
> treating file names containing ‘:’ as host specifiers.  Copies between two remote hosts are also permitted.

The following command copies a project folder recursivly to a remote destination with rsa encrytion key (always use keys for validation! No root login!):
```
scp -r -i [path_to_rsa_key] files_to_tranfer [user@host]:[destination]
```

It's also possible to use ssh.conf profiles using the **-F** flag:
```
scp -r -F [shh_profile] files_to_tranfer [user@host]:[destination]
```
It will pass the profile to the ssh call when establishing the connection and you will be promted for the rsa_key passphrase.

It's also possible transfering a file from a remote host to the client machine (the machine you are running the command from).

```
scp -r -F [shh_profile] [user@remote]:[path/to/transfer/copy] path/to/local/destination/
```

