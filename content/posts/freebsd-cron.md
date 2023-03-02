---
title:  "FreeBSD `root` crontab entries not firing...?"
date:   2023-03-02 21:23:11 +0100
draft: false
tags:
  - freebsd
  - security
  - troubleshooting
---
I recently set up an Oracle Cloud Infrastructure "Ampere" ARM instance and decided to do something unusual and install FreeBSD.

I did this via Terraform, through an official [module](https://github.com/amperecomputing/terraform-oci-ampere-a1) in the [Ampere Computing](https://github.com/amperecomputing) organisation, with a few custom changes to allow different types of traffic (HTTPS, NTP, and so on).

After it was set up, I found that my `root` crontab jobs for backups were not firing, for no obvious reason (some jobs were still logged in `/var/log/cron` but not my `crontab` jobs; this should have been a clue but I didn't appreciate this different...). Googling turned up some historical known issues:

- different environment for running `crontab` commands, e.g.
  - different `PATH` variable
  - different `SHELL` variable
- invalid `crontab` format (as it is slightly different from a normal system `crontab` file)
- missing trailing newline in the `crontab` file
- incorrect permissions on scripts being run

After verifying all of these were correct and banging my head against it for a while, I noticed something in the log files after all...

```plain
Feb 23 16:00:00 ampere-a1-freebsd-13-01 /usr/sbin/cron[63442]: (operator) CMD (/usr/libexec/save-entropy)
Feb 23 16:00:00 ampere-a1-freebsd-13-01 /usr/sbin/cron[63443]: (root) CMD (newsyslog)
Feb 23 16:00:00 ampere-a1-freebsd-13-01 /usr/sbin/cron[63444]: (root) CMD (/usr/libexec/atrun)
Feb 23 16:00:00 ampere-a1-freebsd-13-01 /usr/sbin/cron[63439]: (root) USER (account unavailable)
```

That last message looks a little off. A user is unavailable? Well that can't be anything to do with `root`, right? The account must be available as it just ran two commands at the same time as that message and I'm `sudo`-logged in as `root` right now to troubleshoot this, because `root` is the only account that _can_ read the `cron` logfile. So if there's one account that I'm 100% confident _is_ available on this system (apart from my user account that I `SSH`ed in with) then it's `root`.

Then all of a sudden, a penny dropped. Since I have `PermitRootLogin prohibit-password` set on this instance (it has a public IP address after all), I also took the extra step of "locking" the `root` account. According to the [manpage](https://man.freebsd.org/cgi/man.cgi?pw#USER_LOCKING):

```plain
USER LOCKING
     The pw utility supports a simple password locking mechanism for users; it
     works by prepending the string `*LOCKED*' to the beginning of the pass-
     word field in master.passwd to prevent successful authentication.

     The lock and unlock commands take a user name or uid of the account to
     lock or unlock, respectively.  The -V, -C, and -q options as described
     above are accepted by these commands.
```

Something that doesn't seem to be mentioned anywhere that I could see it (or at least in the `pw` manpage or the `crontab` manpage) is that when `root` is locked with `pw lock root` this will cause user `crontab` jobs to NOT run, while system `crontab` jobs set to run as `root` will run just fine.

So I unlocked the account and next `cron` run:

```plain
Mar  2 21:00:00 ampere-a1-freebsd-13-01 cron[48836]: (root) CMD (newsyslog)
Mar  2 21:00:00 ampere-a1-freebsd-13-01 cron[48838]: (operator) CMD (/usr/libexec/save-entropy)
Mar  2 21:00:00 ampere-a1-freebsd-13-01 cron[48839]: (root) CMD (/usr/libexec/atrun)
Mar  2 21:00:00 ampere-a1-freebsd-13-01 cron[48840]: (root) CMD (/root/test.sh)
```

My test script now appears to run fine, just fine.
