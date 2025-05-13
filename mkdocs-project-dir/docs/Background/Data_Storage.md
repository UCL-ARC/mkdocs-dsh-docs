---
title: Data Storage
categories:
 - User Guide
 - Background
layout: docs
---

# Data Storage

Our clusters have local [parallel filesystems](Parallel_Filesystems.md) consisting of 
your home where you can write data. They may also have local storage on the compute node
that can be used during your job.

## On-cluster storage

### Home

Every user has a home directory. This is the directory you are in when you first log in.

- Location: `/home/<username>`
- May also be referred to as: `~`, `$HOME`.

Many programs will write hidden config files in here, with names beginning with `.` (eg `.config`,
`.cache`). You can see these with `ls -al`.


