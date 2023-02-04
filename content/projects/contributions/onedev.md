---
title: "OneDev usability improvements"
date: 2023-01-21T18:00:00.000Z
link: "https://code.onedev.io/~pulls?query=submitted+by+me"
image: "/img/borgmatic.png"
description: "Usability improvements"
featured: true
tags:
  - usability
  - a11y
fact: "Receive Borgmatic backup status via push notifications"
weight: 100
sitemap: 
    priority : 0.8
---

I wanted to experiment with an alternative to [Gitea](https://gitea.io) for self-hosted Git repositories (mainly configuration backups which contain passwords and do not support password obfuscation or encryption) and came across [OneDev](https://onedev.io). After deploying it, I found a couple of low-hanging fruit items. One was a [simple documentation change](https://code.onedev.io/onedev/server/~pulls/53) to replace a dead link with the correct one, the second one [improves usability and accessibility](https://code.onedev.io/onedev/server/~pulls/54) with password managers by implementing correct [`autocomplete`](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete) behaviour. This allows a password manager (in my case, [1Password](https://1password.com)) to automatically detect and fill 2FA codes during the login process.

Neither were complex changes, however they did require some familiarity with the modular nature of how a Java project is structured, and knowledge of how and where to find definitive advice on W3C specifications.
