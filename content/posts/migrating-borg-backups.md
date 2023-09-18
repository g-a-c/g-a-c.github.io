---
title:  "Migrating Borg backups"
date:   2023-02-02 23:00:00 +0000
draft: false
tags:
  - backups
  - borg
---

I wanted to migrate some backups from [rsync.net](https://rsync.net/borg.html) to [BorgBase](https://borgbase.com) in such a way that they were separate repositories, and to compress on ingestion.

This didn't seem to be a built-in command so I hacked it together in `bash`. The `OLD_REPO` and `NEW_REPO` need to be valid repository addresses, if encryption was used then `BORG_PASSPHRASE` needs to be set and the new repository needs to be configured.

I'll probably never need to do this again, but here we go.

```shell
#!/bin/bash

for archive in $(borg list --json ${OLD_REPO} | jq -r '.[].archives[].name'); do
    ARCHIVE_JSON=$(borg list --json --prefix ${archive} ${OLD_REPO})
    NAME=$(echo ${ARCHIVE_JSON} | jq -r '.[].archives[0].name')
    TIMESTAMP=$(echo ${ARCHIVE_JSON} | jq -r '.[].archives[0].time')
    SIZE=$(borg info ${OLD_REPO}::${NAME} --json | jq -r '.archives[0].stats.original_size')

    borg export-tar ${OLD_REPO}::${NAME} - | pv -s ${SIZE} | borg import-tar --compression auto,zstd,22 --timestamp ${TIMESTAMP} ${NEW_REPO}::${NAME} -
done
```
