---
title: "Bugfixes for OPNsense/FRR"
date: 2021-10-30T12:00:00.000Z
link: "https://github.com/opnsense/plugins/pull/2633"
image: "/img/opnsense_logo-zilver_grijs.png"
description: "Improved the configuration of the FRR plugin for OPNsense"
featured: true
tags:
  - PHP
  - Jinja2
  - BGP
  - routing
  - FreeBSD
  - OPNsense
fact: "Improve FRR configuration in OPNsense appliances"
weight: 100
sitemap: 
    priority : 0.8
---

As a "homelab" user, I was interested in joining [DN42](https://dn42.eu/) using an [OPNsense](https://opnsense.org) firewall in order to educate myself more on BGP and associated networking protocols, but I ran into problems with the project out of the box with the included [`frr`](https://frrouting.org/) package and the way the PHP web UI configured the daemon on the backend.

I raised some issues ([#2602](https://github.com/opnsense/plugins/pull/2602), [#2604](https://github.com/opnsense/plugins/pull/2604), [#2606](https://github.com/opnsense/plugins/pull/2606), [#2623](https://github.com/opnsense/plugins/pull/2623)) with the project containing my findings on these three issues. And by working through the issue on my local appliance I was able to put together a set of Pull Requests which were ultimately superseded/consolidated into [#2633](https://github.com/opnsense/plugins/pull/2633). Once this was approved by the OPNsense developers (with positive feedback in our collaboration via Pull Request comments) this was merged into the OPNsense project for version 21.7.5 and will hopefully set other users up to be in a good position out of the box for their own usage.
