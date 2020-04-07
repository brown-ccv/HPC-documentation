---
title: Account Limits
date: '2019-01-31 22:01:46 +0000'
project: Oscar
section: Accounts
icon: check
---

# Partitions

{% hint style="info" %}
The number and size of jobs allowed on Oscar vary with both partition and type of user account. You can email support@ccv.brown.edu if you need advice on which partitions to use
{% endhint %}

The following partitions are available to all Oscar users:

| Name | Purpose |
| :--- | :--- |
| batch | general purpose computing |
| debug | short wait time, short run time partition for debugging |
| gpu | GPU nodes |
| gpu-debug | short wait time, short run time partition for gpu debugging |
| bigmem | large memory nodes |
| smp | older large memory nodes |

{% hint style="info" %}
For current rates and limits see [https://ccv.brown.edu/services/rates/](https://ccv.brown.edu/services/rates/)
{% endhint %}

## batch partition

* General purpose computing
* Priority is determined by account type \(from highest

  to lowest: condo, premium, exploratory\)

Condo limits apply to the group \(i.e., they reflect the sum of all users on the condo\). Condo users can check the limits on their condo with the command `condos`.

{% hint style="warning" %}
There is no limit on the time for condo jobs, but users should be aware that planned maintenance on the machine may occur \(one month’s notice is given prior to any planned maintenance\).
{% endhint %}

## debug partition

* Short wait time, short run time access for debugging
* All users have the same limits and priority on the debug partition

## gpu partition

* For GPU-based jobs
* Premium users get higher priority and more resources than free users on the GPU partition
* Condo users submit to the gpu partition with normal or priority access \(if they have a priority account in addition to their condo\)

## gpu-debug partition

* Short wait time, short run time gpu access for debugging
* All users have the same limits and priority on the gpu-debug partition

## bigmem

* For jobs requiring large amounts of memory
* Premium users get higher priority and more resources than free users on the bibmem partition
* Condo users submit to the bigmem partition with normal or priority access \(if they have a priority account in addition to their condo\)

## smp partition

* For jobs requiring large amounts of memory
* Premium users get higher priority and more resources than free users on the SMP partition
* Condo users submit to the SMP partition with normal or priority access \(if they have a priority account in addition to their condo\)

