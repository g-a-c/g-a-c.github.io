---
title:  "De-Googling my life"
date:   2025-04-19 21:53:11 +0100
draft: false
tags:
  - google
  - monopolies
  - bigtech
  - 
---
With the state of....well, everything in 2025 in the land of the free, I decided it would be a good time to try and become less dependent on big tech companies.
There are a lot of features of Google I use heavily, and some I wouldn't really miss. This doc attempts to outline some of my experiences. If I ever figure out how to get this better integrated with Mastodon, I'd appreciate replies...

# Google Mail

This is a **big** one. I've been a Google Mail user since it was invite-only (2004?) and I have made the mistake which I made slowly over time of always using my **`@gmail.com`** address. Whomp whomp. If I had at least used my own domain from the beginning then migrating away would have been significantly easier. But instead I _used to_ use my own domain, then started trying Google Mail, then using it a little more, then before you know it it's been my main email address for a little over 20 years.

## Mailcow

Mailcow appeals for a few reasons, such as email, contacts and calendar in one place, like Exchange. It also provides ActiveSync, like Exchange. This should give me push email on iOS in the standard Mail app (which isn't possible with IMAP as far as I could see, perhaps even missing at a protocol level?). It also provides a very easily configured setup, which I was able to run on a small Hetzner VPS for testing.

Unfortunately at some point, my mail has stopped syncing entirely, even when I manually refresh it. All the folders have also vanished. But Contacts and Calendar still sync as they should so this doesn't appear to be a network connection or password issue.

### Pros

- relatively easily configured
- comes with a Docker Compose file
- simple backups

### Cons

- for some reason, mail has stopped syncing, and I haven't yet found the right place to look to find out _why_
- also some issues with syncing Reminders, I deleted them from my phone but they're still in Mailcow's webmail (SOGo)

# Google Drive

I prefer my file sync to be more of a "virtual file system" because I have files that I never really access and don't see the point syncing these around with Syncthing. So I'm happy with

## Nextcloud

I used Nextcloud All-in-One to try to replace Google Drive, and it works pretty well. THe VFS support appears solid on both my Windows desktop and macOS laptop, where only files I use get synced (saving space) and the entire library can be backed up centrally from my NAS where Nextcloud is hosted

### Pros

- AIO Docker installation is _fairly_ easy

### Cons

- I also tried this with Contacts and Calendar functionality
  - Contacts don't sync to iOS properly (I have ~130 Nextcloud contacts, and about ~115 of them sync to iOS. No idea why)
  - No way to add recurring reminders from the web
 
# Google Photos

## Immich

Immich seems like a really good replacement. The only feature missing (for me) is the ability to sync deletes. With Google Photos you can mass-delete photos from the web (convenient) and then sync those deletes to your iOS phone to clear up the phone storage. Immich doesn't appear to offer this. Other than that, it's VERY feature-complete at this point, was pretty easy to configure, and has a solid third-party tool for importing from a Google Takeout archive. Nice.

Only two bugs I found so far

- (iPhone) if you delete all the local photos on an iPhone, then the background upload in Immich stops working because there are no longer any local photo albums. They all become deselected, and then when you take a new photo, the "Recents" album gets recreated but is no longer synced
- (iPhone) I sometimes have an issue where the timeline view is blurred until I open/close a picture in full screen view. I've never seen this on the web, it may be iOS app specific.
