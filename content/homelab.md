---
title: "About my homelab"
date: 2025-08-05T07:21:13Z
sitemap:
  priority : 1.0

outputs:
- html
---
Like a lot of people in my field, I have a [homelab](https://readthemanual.co.uk/what-is-a-homelab/). This runs a load
of services that I use personally including:

- [Traefik](https://traefik.io) as a reverse proxy for all services
- [OpenCloud](https://opencloud.eu) for file synchronisation
- [Immich](https://immich.app) for self-hosted photo storage
- [Forgejo](https://forgejo.org) for self-hosted Git repositories
- [Unifi](https://www.ui.com) for controlling my home switches and access points
- [OPNsense](https://opnsense.org) as my firewall

I don't use this so much currently for proving out work stuff, but it comes in very useful for testing and experimenting.
Pretty much everything is Docker-based for portability (I've rebuilt the host multiple times) with persistent storage on
a [ZFS](https://openzfs.org) array.

My favourite thing about working in the technology sector is that there's always cool new stuff to get to grips with,
and being able to try things out at home often feeds into my tool choices at work. Where there's something with more
features, or more reliability, that gives me something that can have a genuine impact.
