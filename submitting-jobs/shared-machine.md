---
title: Shared Machine
date: '2019-01-31T22:04:43.000Z'
draft: false
project: Oscar
section: Submitting jobs
weight: 0
icon: check
---

# Running Jobs

Oscar is a shared machine used by hundreds of users at once. User requests are called _**jobs**_. A job is the combination of the resource requested and the program you want to run on the compute nodes of the Oscar cluster. On Oscar, [_**Slurm**_](https://slurm.schedmd.com) is used to schedule and manage jobs.

Jobs can be run on Oscar in two different ways:

* _**Interactive** **jobs**_ allow the user to interact with programs \(e.g., by entering input manually, using a GUI\) while they are running. However, if your connection to the system is interrupted, the job will abort. Small jobs with short run times or jobs that require the use of a GUI are best-suited for running interactively.
* _**Batch** **jobs**_ allows you to submit a script that tells the cluster

  how to run your program. Your program can run for long periods of

  time in the background, so you don't need to be connected to Oscar.

  The output of your program is continuously written to an output file

  that you can view both during and after your program runs.

Jobs are scheduled to run on the cluster according to your account priority and the resources you request \(e.g. cores, memory and runtime\). In general, the fewer resources you request, the less time your job will spend waiting in the queue.

{% hint style="warning" %}
Please do not run CPU-intense or long-running programs directly on the login nodes! The login nodes are shared by many users, and you will interrupt other users' work.
{% endhint %}

