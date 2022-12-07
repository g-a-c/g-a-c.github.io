---
title: Device42 Terraform provider
date: 2020-01-07T15:00:28.528Z
link: https://registry.terraform.io/providers/g-a-c/device42/latest
image: /img/Terraform_VerticalLogo_Color_RGB.png
description: A simple Terraform provider for retrieving passwords from Device42
tags:
  - Terraform
  - DevOps
  - Go
featured: true
fact: 
---

As part of working for a company who used [Device42](https://www.device42.com) for their configuration management, it became apparent that a useful feature would be able to retrieve passwords from Device42 via Infrastructure-as-Code. Our IaC tool of choice at the time was Terraform, but there was no public provider for this, so I created one.

Unfortunately I left this company shortly after completing this work, and there is no public Device42 instance against which to continue designing/testing, so this never got any support for other resource types, although it is something I would like to go back to in order to flesh this out a little.

However as part of this work, I did integrate Sonar Cloud for quality assessments and a CI/CD pipeline for signing/releasing the provider to the Terraform Registry so that as improvements come, they will be released.