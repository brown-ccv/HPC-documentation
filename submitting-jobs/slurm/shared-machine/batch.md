---
title: Batch
date: '2019-01-31T22:04:57.000Z'
draft: false
project: Oscar
section: Submitting jobs
weight: 0
icon: check
---

# Batch Jobs

## Submitting jobs using batch scripts

To run a batch job on Oscar, you first have to write a script that describes what resources you need and how your program will run. Some example batch scripts are available in your home directory on Oscar, in the directory:

```bash
~/batch_scripts
```

A batch script starts by specifying the `bash` shell as its interpreter with the line:

```bash
#!/bin/bash
```

By default, a batch job will reserve 1 core and 2.8GB of memory per core for your job. You can customize the amount of resources allocated for your job by explicitly requesting them in your batch script with a series of lines starting with `#SBATCH`, e.g.,

```bash
#SBATCH -n 4
#SBATCH --mem=16G
#SBATCH -t 1:00:00
```

The above lines request 4 cores \(`-n`\), 16GB of memory **per node** \(`--mem`\), and one hour of runtime \(`-t`\). After you have described the resources you want allocated for the job, you then give the commands that you want to be executed.

{% hint style="warning" %}
All of the `#SBATCH` instructions in your batch script must appear **before the commands** you want to run.
{% endhint %}

Once you have your batch script, you can submit a batch job to the queue using the `sbatch` command:

```bash
sbatch <jobscript>
```

## Submitting jobs from the command line

As an alternative to requesting resources within your batch script, it is possible to define the resources requested as command-line options to `sbatch`. For example, the command below requests 4 cores \(`-n`\), 16GB of memory **per node** \(`--mem`\), and one hour of runtime \(`-t`\) to run the job defined in the batch script.

```bash
sbatch -n 4 -t 1:00:00 --mem=16G <jobscript>
```

Note that command-line options passed to `sbatch` will override the resources specified in the script, so this is a handy way to reuse an existing batch script when you just want to change a few of the resource values.

## Output from batch jobs

The `sbatch` command will return a number, which is your **Job ID**. You can view the output of your job in the file `slurm-<jobid>.out` in the directory where you invoked the `sbatch` command. For instance, you can view the last 10 lines of output with:

```bash
tail -10 slurm-<jobid>.out
```

Alternatively, you can mention the file names where you want to dump the standard output and errors using the `-o` and `-e` flags.

## sbatch command options

A full description of all of the options for`sbatch` can be found [online ](https://slurm.schedmd.com/sbatch.html)or by using the following command on Oscar:

```bash
$ man sbatch
```

The table below summarizes some of the more useful options for`sbatch` .

| option | purpose |
| :--- | :--- |
| `-J` | Specify the job name that will be displayed when when listing the job |
| `-n` | Number of tasks \(= number of cores, if "--cpus-per-task" or "-c" option is not mentioned\) |
| `-c` | Number of CPUs or cores per task \(on the same node\) |
| `-N` | Number of nodes |
| `-t` | Runtime, as HH:MM:SS |
| `--mem=` | Requested memory per node |
| `-p` | Request a specific partition |
| `-o` | Filename for standard output from the job |
| `-e` | Filename for standard error from the job |
| `-C` | Add a feature constraint \(a tag that describes a type of node\). Note: you can view the available features on Oscar with the `nodes`command. |
| `--mail-type=` | Specify the events that you should be notified of by email: BEGIN, END, FAIL, REQUEUE, and ALL |
| `--mail-user=` | Email ID where you should be notified |

## Passing environment variables to a batch job

When a user log in to Oscar, there are pre-set environment variables such as HOME, which are the user's login environment variables. A user may modify an existing enviornmet variable, or add a new environment variable. So when a user submit a slurm batch job, the user's current environment variables may differ from the user's login environment. By default, a user's current environment variables, instead of the user's login environment variables, are accessible to the user's batch jobs on Oscar.

To modify or add an environment variable, run the following command:

* run the following command in your shell

```bash
export my_variable=my_value
```

* or have the following line in your batch script

```bash
#SBATCH --export=my_variable=my_value
```

After the step above to modify or add an environment variable, your batch job can access the environment variable _my\_variable_ whose value is _my\_value_.

To export more than one environment variables, just list all the name=value pairs separated by a comma:

```bash
#SBATCH --export=my_variable1=my_value1,my_variable2=my_value2,my_variable3=my_value3
```

