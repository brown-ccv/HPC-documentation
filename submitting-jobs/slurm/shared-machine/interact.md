---
title: Interact
date: '2019-01-31T22:04:53.000Z'
draft: false
project: Oscar
section: Submitting jobs
weight: 0
icon: check
---

# Interactive Jobs

To start an interactive session for running serial or threaded programs on an Oscar compute node, simply run the command `interact` from the login node:

```bash
interact
```

By default, this will create an interactive session that reserves 1 core and 4GB of memory for a period of 30 minutes. You can change the resources reserved for the session from these default limits by modifying the interact command:

```text
usage: interact [-n cores] [-t walltime] [-m memory] [-q queue]
                [-o outfile] [-X] [-f featurelist] [-h hostname] [-g ngpus]

Starts an interactive job by wrapping the SLURM 'salloc' and 'srun' commands.

options:
  -n cores        (default: 1)
  -t walltime     as hh:mm:ss (default: 30:00)
  -m memory       as #[k|m|g] (default: 4g)
  -q queue        (default: 'batch')
  -o outfile      save a copy of the sessions output to outfile (default: off)
  -X              enable X forwarding (default: no)
  -f featurelist  CCV-defined node features (e.g., 'e5-2600'),
                  combined with '&' and '|' (default: none)
  -h hostname     only run on the specific node 'hostname'
                  (default: none, use any available node)
  -a account     user SLURM accounting account name
```

For example, the command

```bash
$ interact -n 20 -t 01:00:00 -m 10g
```

requests an interactive session with 20 cores and 10 GB of memory \(per node\) for a period of 1 hour.

{% hint style="info" %}
**Keeping Interactive Jobs Alive:**

If you loose connectivity to your login node, you loose access to your interactive job. To mitigate this issue you can use `screen` to keep your connection alive. For more information on using `screen` on the login nodes, see the [software section](../../../connecting-to-oscar/connecting/ssh/screen.md)
{% endhint %}

