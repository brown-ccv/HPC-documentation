# Jupyter

## Installing Jupyter

Use pip or anaconda to [install jupyter notebook](https://jupyter.readthedocs.io/en/latest/install.html).

## Running Jupyter on Oscar

There are a couple of ways to use [Juypter](https://jupyter.org/) Notebooks on Oscar. You can use Jupyter Notebooks in a VNC session or you can submit a batch script to start a Juypter Notebook server. With the batch script method you use a browser on your machine to connect to your Juypter Notebook server on Oscar.

{% hint style="warning" %}
Do not run Jupyter Notebooks on the login nodes.
{% endhint %}

## In a VNC Session

Start a [VNC session](../connecting-to-oscar/oscar/connecting/vnc.md) and open up a terminal in the VNC session . To start a Jupyter notebook, enter

```text
jupyter-notebook
```

This will start the Jupyter notebook server and open up a browser with the lab

{% hint style="info" %}
If you installed Juypter notebook with pip you may need to give the full path:

~/.local/bin/jupyter-notebook
{% endhint %}

## Using a Batch Job

1. Submit a batch script tp start the server.
2. Setup an ssh tunnel to the server.
3. Open a browser to view the lab.
4. Use `scancel` to end the batch job when you are done.

### 1. Submit batch script

Here is an example batch script to start at Juypter notebook server on an Oscar compute node

```text
#!/bin/bash
#SBATCH --nodes 1
#SBATCH -c 6
#SBATCH --time 04:00:00
#SBATCH --mem-per-cpu 3G
#SBATCH --job-name tunnel
#SBATCH --output jupyter-log-%J.txt
## get tunneling info
XDG_RUNTIME_DIR=""
ipnport=$(shuf -i8000-9999 -n1)
ipnip=$(hostname -i)
## print tunneling instructions to jupyter-log-{jobid}.txt
echo -e "
    Copy/Paste this in your local terminal to ssh tunnel with remote
    -----------------------------------------------------------------
    ssh -N -L $ipnport:$ipnip:$ipnport $USER@ssh.ccv.brown.edu
    -----------------------------------------------------------------
    Then open a browser on your local machine to the following address
    ------------------------------------------------------------------
    localhost:$ipnport  (prefix w/ https:// if using password)
    ------------------------------------------------------------------
    "
## start an ipcluster instance and launch jupyter server
~/.local/bin/jupyter-notebook --no-browser --port=$ipnport --ip=$ipnip
```

{% hint style="info" %}
If you installed Juypter notebook with pip you may need to give the full path:

`~/.local/bin/jupyter-notebook --no-browser --port=$ipnport --ip=$ipnip`
{% endhint %}

This script can be found in ~/batch\_scripts. Copy this example and submit this script with

`sbatch jupyter.sh`

Once your batch job is running there will be a file `jupyter-log-`{jobid}`.txt`containing the info you need to connect to your jupyter notebook server on Oscar. To check if your job is running you can use `myq`

The output from `myq` will look something like this:

```text
Jobs for user mhamilton

Running:
ID       NAME    PART.  QOS          CPU  WALLTIME  REMAIN   NODES
7239096  tunnel  batch  pri-mhamilt  6    4:00:00   3:57:33  node1036

Pending:
(none)
```

### 2. Setup an ssh tunnel to the notebook server

In this example the jobID is 7239096. To view the notebook server info, use `cat.` For this example:

`cat jupyter-log-7239096.txt`

Open a terminal on your machine and copy and past the `ssh -N -L ........` line in to a terminal **on your machine**.

```text
 ssh -N -L $ipnport:$ipnip:$ipnport user@ssh.ccv.brown.edu
```

Enter your Oscar password. Note it will appear that nothing has happened.

### 3. Open a browser to view the notebook

Open a browser on your local machine to the address given in `cat jupyter-log-{jobid}.txt.`

```text
localhost:9349  (prefix w/ https:// if using password)
```

The notebook will ask for a token. Copy the token from `jupyter-log-{jobid}.txt.` Then your notebook will start.

{% hint style="warning" %}
Remember to `scancel {jobid}` when you are done with your notebook session
{% endhint %}

