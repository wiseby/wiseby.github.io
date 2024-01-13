---
layout: post
title: "How to test/debug apis with fiddler"
categories: ["Fiddler"]
---

You can use Fiddler Classic to proxy your requests using the address "ipv4.fiddler". An example for a node Express Server: `https://ipv4.fiddler:3000/api/example`. It will redirect it to localhost after intercepting the request. By using the host "ipv4.fiddler" you bypass the proxy for "localhost", this is hardcoded in many of the modern HTTP stacks today.