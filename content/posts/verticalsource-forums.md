---
title:  "Vertical Scope and online forums"
date:   2025-07-28 22:35:11 +0100
draft: false
tags:
  - forums
  - data brokers
  - mergers
---
I recently became aware of a company called Vertical Scope, who (via their Fora sub-brand) appear to have taken over a number of forums, including
some I had dormant accounts on since before this company took over. Since I'm trying to clean my digital house, I decided to pop them a privacy
request to see what data they held on me.

I started with a simple request:

> Hello,
> This is a written request for all data you hold on me linked with this email address (me@gmail.com) and any sub-address (for example me+ANYTEXTHERE@gmail.com)
>
> Regards, me

And received a slightly disappointing but not unexpected reply

> Please provide the URL(s) of the forum(s) you are registered with.

I enquired whether they had a list of the "hundreds" of forums they own instead of having to list every forum I have an account on _just in case_ they own it.

They do not. **Or so they claimed...**

Turns out that the [Fora webpage](https://fora.com/communities/) has a list of all communities, in a [nicely consumable JSON file](https://api.tls-c1-c.fora.com/foraweb/communities?rank=all). So since they couldn't tell me what forums they own, I decided to find out and tell the privacy team what forums they own...

## Required tools

- `curl`
- `jq`

## Steps

* Get the JSON file from above, and store it:

  ```shell
  curl "https://api.tls-c1-c.fora.com/foraweb/communities?rank=all" > all_forums.json
  ```

- Get a list of domain names that you have accounts on.

  - In my case, I use `1Password` and have the `op` CLI utility installed. If you use `1Password` then this should work, otherwise you'll have to figure this part out yourself
  - This `1Password` command prints anything in the "Login" category, dumps the title (human-readable) and the first URL (which is usually the primary one, most of my logins only have one URL, some have more but the primary one is usually the "main" URL, secondary URLs might be for APIs, documentation, etc)

  ```shell
  op item list --categories login --format=json | jq -r '[.[] | {"title": .title, "username": .additional_information, "primary_url": .urls[0].href}]' > my_accounts.json
  ```

- Read in the list of Fora forum URLs, and find any matching `1Password` entries

  ```shell
  for domainName in $(jq < all_forums.json -r '.[].WebDomainName'); do jq <my_accounts.json --arg domain "${domainName#www.}" '.[] | select(.primary_url != null) | select(.primary_url | contains($domain))'; done
  ```

  - this script strips the `www.` prefix from the domain to match, in case I have it stored in `1Password` without it. Since this still leaves the rest of the domain, it matches `1Password` entries _with_ or _without_ the prefix
