---
title: "About this website"
date: 2025-08-05T07:21:13Z
sitemap:
  priority : 1.0

outputs:
- html
---
This site is intentionally bare, as I'm no designer. But what it _is_, is demonstrative of the techniques I've learned.
Every change to it is committed to Git, first and foremost, before a pull request gets opened. GitHub Actions builds it
and deploys it to a staging setup so that I can preview the site in a safe way. Once I'm happy that it looks like I want
it to, I can merge the pull request and have it deployed to the correct location automatically.

I may not know a lot about HTML, CSS and suchlike. But with the wide array of modern static site tools, I don't need to!

What I can do is write well-formed Markdown and use the toolchain available to me to make turning that into a functional
website quick, simple, and automated as much as possible.

Technologies used:

- [Hugo](https://gohugo.io) static site generator
  - [Hextra](https://imfing.github.io/hextra/) theme
- [GitHub](https://github.com)
  - [GitHub Actions](https://docs.github.com/en/actions) for CI/CD purposes
- [OctoDNS](https://github.com/octodns/octodns) for configuring DNS records
- [Mailcow](https://mailcow.email) for email services on this domain
