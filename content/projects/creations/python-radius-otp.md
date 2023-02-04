---
title: Super-basic testing-only RADIUS server (Python)
date: 2018-02-07T15:00:28.528Z
link: https://registry.terraform.io/providers/g-a-c/device42/latest
image: /img/Terraform_VerticalLogo_Color_RGB.png
description:
  - A super-basic RADIUS implementation with Python, using one-time passwords
tags:
  - Python
  - RADIUS
  - authentication
  - security
featured: true
fact: 
---

As part of my work for [Barracuda Networks](https://www.barracuda.com) on the [CloudGen Firewall](https://www.barracuda.com/products/network-security/cloudgen-firewall), there were some authentication scenarios which were previously difficult to test easily due to setup time and complexity. The simple solution was to write some quick and dirty Python to implement the most basic form of the RADIUS protocol, including the `State` attribute in order to correctly pair two `Access-Request` packets.

The code is very simple, but required some understanding of the [RADIUS protocol](https://tools.ietf.org/html/rfc5080) and its challenge->response nature.

- [Source Code](https://github.com/g-a-c/python-radius)
