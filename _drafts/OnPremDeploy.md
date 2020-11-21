---
layout: post
title: "OnPrem Deployment with Azure Pipelines"
category: [Azure, Linux]
---

## Deploying with Azure Pipelines over SSH

So pipelines you say? Great it is, you say? Let's do it!

Pipelines is one of the great things when using the wonders of Azure DevOps platform.
This is Microsofts answer to CI/CD. Host your code on a number of different code Repositories like GitHub, BitBucketetc.
DevOps also have there own repository integrated in the platform. 

Today I'm going to show you how I managed to setup a pipeline for a Python Flask application to my homeserver over SSH.

It's a fairly basic pipeline only running ssh tasks but could in the future be extended doing lots of cool stuff like linting, packaging and building.
