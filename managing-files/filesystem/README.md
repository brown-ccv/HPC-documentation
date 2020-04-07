---
title: Filesystem
date: '2019-01-31T22:06:44.000Z'
draft: false
project: Oscar
section: Managing files
weight: 0
icon: check
---

# Oscar's Filesystem

CCV uses IBM's General Parallel File System \(GPFS\). Users have a home, data, and scratch space.

**home** `~`

* 20GB of space
* Optimized for many small files
* Nightly backups \(30 days\)
* Quota is per individual user

**data** `~/data`

* Each PI gets 256GB for free
* Optimized for reading large files
* Nightly backups \(30 days\)
* Quota is by group

**scratch** `~/scratch`

* 512GB of space - contact support@ccv.brown.edu increase on a temporary basis
* Optimized for reading/writing large files
* NO BACKUPS
* Purging: files not accessed for 30 days may be deleted
* Quota is per individual user

{% hint style="warning" %}
Files not accessed for 30 days will be deleted from your scratch directory. This is because scratch is high performance space. The fuller scratch is the worse the read/write performance. **Use ~/data for files you need to keep long term.**
{% endhint %}

{% hint style="warning" %}
The scratch purge is on individual files. It is by 'atime' which is when the file was last read. You can use 'find' to find files that are at risk of being purged, e.g. to find files in the current directory that have not been accessed in the last 25 days:

find . -atime +25
{% endhint %}

A good practice is to configure your application to read any initial input data from `~/data` and write all output into `~/scratch`. Then, when the application has finished, move or copy data you would like to save from `~/scratch` to `~/data`.

{% hint style="info" %}
Note: class or temporary accounts may not have a `~/data` directory!
{% endhint %}

To see how much space you have on Oscar you can use the command `myquota`. Below is an example output

```text
                       Block Limits                              |           File Limits              
    Type    Filesystem           Used    Quota   HLIMIT    Grace |    Files    Quota   HLIMIT    Grace
    -------------------------------------------------------------|--------------------------------------
    USR     home               8.401G      20G      30G        - |    61832   524288  1048576        -
    USR     scratch              332G     512G      12T        - |    14523   323539  4194304        -
    FILESET data+apollo        11.05T      20T      24T        - |   459764  4194304  8388608        -
```

{% hint style="warning" %}
You can go over your quota up to the hard limit for a grace period \(14 days\). This grace period is to give you time to manage your files. When the grace period expires you will be unable to write any files until you are back under quota.

There is a quota for space used and for number of files. If you hit the hard limit on **either** of these you will be unable to write any more files until you are back under quota.
{% endhint %}

