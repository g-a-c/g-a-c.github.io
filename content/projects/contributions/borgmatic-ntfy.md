---
title: "Added `ntfy.sh` support to Borgmatic"
date: 2022-06-08T22:00:00.000Z
link: "https://projects.torsion.org/borgmatic-collective/borgmatic/pulls/543"
image: "/img/borgmatic.png"
description: "Allows Borgmatic users to receive push notifications via `ntfy.sh`"
featured: true
tags:
  - Python
fact: "Receive Borgmatic backup status via push notifications"
weight: 100
sitemap:
    priority : 0.8
---

As a "homelab" Borgmatic user, I found the available options for push notifications a little limiting. Having become aware of [`ntfy.sh`](https://ntfy.sh) which offers both a cloud-hosted and self-hosted version, this seemed a good fit into Borgmatic to allow custom push notifications to be sent. So I set about creating a pull request for the Borgmatic project to implement this.

This PR followed all the project guidelines, including writing basic unit tests, caters for privacy-conscious self-hosted Ntfy users just as easily as the cloud-hosted version, and comes with [full documentation](https://torsion.org/borgmatic/docs/how-to/monitor-your-backups/#ntfy-hook)
