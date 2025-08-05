---
title: "Improvements to Microsoft Azure troubleshooting documentation"
date: 2020-07-16T18:00:00.000Z
link: "https://github.com/MicrosoftDocs/azure-docs/pull/59157"
image: "/img/borgmatic.png"
description: "Usability improvements"
featured: true
tags:
  - troubleshooting
  - cloud
  - azure
  - front-door
fact: "Receive Borgmatic backup status via push notifications"
weight: 100
sitemap:
    priority : 0.8
---

At a previous company I was working with deploying Spring Boot web applications into an Azure environment, making use of:

- Azure Kubernetes Service
  - including the Azure Managed Ingress Controller
- Azure Front Door
  - providing blue/green rollouts

We were having reproducible issues with HTTP requests failing and it was unclear why. After diagnosis with Azure support
staff, we found that although we had disabled all of the WAF functionality that Front Door offered, there was a further
series of compliance checks which were undocumented and unable to be disabled. We then found that one area of our code
had a bug and was not setting a `Content-Length` header that Front Door was then (correctly) rejecting. The notable part
of the troubleshooting section is that these checks occur even if the WAF is disabled, meaning that customers who may
have come to rely on de-facto (buggy) HTTP behaviour may have been unaware that working behaviour from other
platforms/reverse proxies may correctly be broken on Front Door. [This pull request](https://github.com/MicrosoftDocs/azure-docs/pull/59157)
provides a new section in the troubleshooting documentation to make customers explicitly aware of why this message
would be returned, how to diagnose it, and (most importantly) that these checks cannot be worked around within the Front
Door platform.
