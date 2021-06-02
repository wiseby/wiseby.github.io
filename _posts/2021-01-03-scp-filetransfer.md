---
layout: post
title: "Secure Copy File-transfer with SSH"
category: [Linux, Deployment]
---

SSH is a wonderful thing and I use it all the time working on servers in my home.
With ssh configuration setup for my user it's very easy connecting to whatever server I want.

Easy as making pancakes!

In my case I wanted to deploy a dotnet webapi build to my server.

The easiest way of transfer files over network is probably with the tool scp.
scp stands for Secure Copy and uses ssh protocol.

**From manual page of scp:**

> scp copies files between hosts on a network. It uses ssh(1) for data transfer, and uses the same authentication and provides the same security as ssh(1). scp will ask for passwords or passphrases if they are needed for authentication.
>
> File names may contain a user and host specification to indicate that the file is to be copied to/from that host. Local file names can be made explicit using absolute or relative path-names to avoid scp
> treating file names containing ‘:’ as host specifiers. Copies between two remote hosts are also permitted.

The following command copies a project folder recursively to a remote destination with rsa encryption key (always use keys for validation! No root login!):

```
scp -r -i [path_to_rsa_key] files_to_transfer [user@host]:[destination]
```

It's also possible to use ssh.conf profiles using the **-F** flag:

```
scp -r -F [shh_profile] files_to_transfer [user@host]:[destination]
```

It will pass the profile to the ssh call when establishing the connection and you will be prompted for the rsa_key passphrase.

It's also possible transfer a file from a remote host to the client machine (the machine you are running the command from).

```
scp -r -F [shh_profile] [user@remote]:[path/to/transfer/copy] path/to/local/destination/
```

At this point I'm doing all steps for deployment manually to get a better understanding over the process.
In the future I'll move over to a more automated approach. Ansible is a interesting software that I want to get deeper into.
