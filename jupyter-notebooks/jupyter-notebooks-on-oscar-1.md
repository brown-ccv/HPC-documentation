# Jupyter Notebooks on Oscar

## Installing Jupyter Notebook

The anaconda/3-5.2.0 module provides jupyter-notebook. Users can also use pip or anaconda to [install jupyter notebook](https://jupyter.readthedocs.io/en/latest/install.html).

## Running Juypter Notebook on Oscar

There are a couple of ways to use [Juypter](https://jupyter.org/) Notebookon Oscar. You can run Jupyter Notebook

* in a VNC session 
* using a batch job
* in an interactive session

  With the batch job or interactive session method, you use a browser on your machine to connect to your Juypter Lab server on Oscar.

{% hint style="warning" %}
Do not run jupyter notebook on login nodes.
{% endhint %}

## In a VNC Session

Start a [VNC session](../connecting-to-oscar/vnc.md), and open up a terminal in the VNC session . To start a jupyter notebook, enter

```text
jupyter-notebook
```

This will start the Jupyter notebook/lab server and open up a browser with the notebook/lab

{% hint style="info" %}
If you installed Juypter notebook/lab with pip you may need to give the full path:

`~/.local/bin/jupyter-notebook`
{% endhint %}

## Using a Batch Job

1. submit an ssh tunnel to the server.
2. Setup an ssh tunnel to the server.
3. Open a browser to view the notebook.
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
module load anaconda/3-5.2.0
jupyter-notebook --no-browser --port=$ipnport --ip=$ipnip
```

{% hint style="info" %}
If you installed Juypter notebook/lab with pip you may need to give the full path:

`~/.local/bin/jupyter-notebook --no-browser --port-$ipnport --ip=$ipnip`
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
Remember to `scancel {jobid}` when you are done with your notebook session.
{% endhint %}

## In an Interactive Session

1. Start jupyter lab in an interactive job
2. Setup an ssh tunnel to the server.
3. Open a browser to view the notebook.
4. Use `scancel` to end the batch job when you are done.

### 1.Start jupter lab in in interactive job

Start a [Interactive job](../submitting-jobs/slurm/shared-machine/interact.md) and then in your interactive seesion enter

```text
unset XDG_RUNTIME_DIR
module load anaconda/3-5.2.0
ipnport=$(shuf -i8000-9999 -n1)
echo $ipnport
ipnip=$(hostname -i)
echo $ipnip
jupyter-notebook --no-browser --port=$ipnport --ip=$ipnip
```

Output like below indicates that Jupyter Lab starts:

> $ jupyter-notebook --no-browser --port=$ipnport --ip=$ipnip
>
> \[I 13:35:25.948 NotebookApp\] JupyterLab beta preview extension loaded from /gpfs/runtime/opt/anaconda/3-5.2.0/lib/python3.6/site-packages/jupyterlab
>
> \[I 13:35:25.948 NotebookApp\] JupyterLab application directory is /gpfs/runtime/opt/anaconda/3-5.2.0/share/jupyter/lab
>
> \[I 13:35:25.975 NotebookApp\] Serving notebooks from local directory: /gpfs\_home/yliu385
>
> \[I 13:35:25.975 NotebookApp\] 0 active kernels
>
> \[I 13:35:25.975 NotebookApp\] The Jupyter Notebook is running at:
>
> \[I 13:35:25.975 NotebookApp\] [http://172.20.207.61:8855/?\*\*token=c58d7877cfcf1547dd8e6153123568f58dc6d5ce3f4c9d98\*\*](http://172.20.207.61:8855/?**token=c58d7877cfcf1547dd8e6153123568f58dc6d5ce3f4c9d98**)
>
> \[I 13:35:25.975 NotebookApp\] Use Control-C to stop this server and shut down all kernels \(twice to skip confirmation\).
>
> \[C 13:35:25.994 NotebookApp\]
>
> ```text
> Copy/paste this URL into your browser when you connect for the first time,
>
> to login with a token:
>
>     http://172.20.207.61:8855/?token=c58d7877cfcf1547dd8e6153123568f58dc6d5ce3f4c9d98&token=c58d7877cfcf1547dd8e6153123568f58dc6d5ce3f4c9d98
> ```

### 2. Setup an ssh tunnel to the server

Open a terminal on your machine and tenter the following line in a terminal **on your machine**. You need replace $ipnip and $ipnport with the values from the two `echo` commands in the previous step.

```text
 ssh -N -L $ipnport:$ipnip:$ipnport user@ssh.ccv.brown.edu
```

Enter your Oscar password. Note it will appear that nothing has happened.

### 3. Open a browser to view the notebook

Open a browser on your local machine to the address:

```text
localhost:$ipnport  (prefix w/ https:// if using password)
```

Again, you need to replace `$ipnport` with the value from the first `echo` command in Step 1. The notebook will ask for a token. You can copy the token from the ouput of Step 2.

### 4. Press 'Ctl+C' twice to kill your Jupyter Lab server

Once you finish and no longer need the Jupyter Lab server, you can kill the server by pressing 'Ctl+C' twice in your interactive session.

