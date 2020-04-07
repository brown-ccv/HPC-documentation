# FAQ

## General

### How do I request help?

Most inquiries can be directed to CCV’s support address, `support@ccv.brown.edu`, which will create a support ticket with one of our staff.

### What are the fees for CCV services?

All CCV services are billed quarterly, and rates can be found [here](../accounts-on-oscar/account-types.md) \(requires a Brown authentication to view\). Questions about rates should be directed to `support@ccv.brown.edu`.

### How do I acknowledge CCV in a research publication?

We greatly appreciate acknowledgements in research publications that benefited from the use of CCV services or resources.

## Oscar

### What is Oscar?

Oscar is our primary research computing cluster with several hundred multi-core nodes sharing a high-performance interconnect and file system. Applications can be run interactively or scheduled as batch jobs.

### How do I request an account on Oscar?

To request an account, please fill out a [New User Account Form](http://pccvwebcit.services.brown.edu/secure/account/). All accounts are subject to our [General Terms and Conditions](ccv-user-policies.md).

### How do I run a job on Oscar?

Sample batch scripts are available in your home directory at `~/batch_scripts` and can be run with the `sbatch <jobscript>` command. For more information, visit our manual page on [Batch Jobs](../submitting-jobs/batch.md).

### Can I use Oscar for teaching?

See our page on [Academic Classes](https://ccv.brown.edu/services/consulting/student-accounts/)

### How do I find out when the system is down?

We post updates to our user mailing list, `ccv@listserv.brown.edu` which you are automatically subscribed to when setting up an account with CCV. If you need to be added to the mailing list, please submit a support ticket to `support@ccv.brown.edu`. We also have an announcement mailing list for office hours, workshops and other events relevant to CCV users, `ccv-announce.listserve.brown.edu`.

### How do I run a job array on Oscar?

A job array is a special type of job submission that allows you to submit many related batch jobs with a single command. This makes it easy to do parameter sweeps or other schemes where the submitted jobs are all the same except for a single parameter such as a filename or input variable. Job arrays require special syntax in your job script. Sample batch scripts for job arrays are available in your home directory at `~/batch_scripts` and can be run with the `sbatch <jobscript>` command. For more information, visit our manual page on [Running Jobs](../submitting-jobs/array.md).

### How do I run a MPI job on Oscar?

MPI is a type of programming interface. Programs written with MPI can run on and communicate across multiple nodes. You can run MPI-capable programs by calling `srun --mpi=pmi2 <program>` in your batch script. For more detailed info, visit our manual page on [MPI programs](../submitting-jobs/mpi-jobs.md).

### I have some MPI-enabled source code. How can I compile it on Oscar?

Load an mpi module `module load mpi`. For a list of mpi modules available, `module avail mpi`

### What applications are available on Oscar?

Many scientific and HPC software packages are already installed on Oscar, including python, perl, R, Matlab, Mathematica, and Maple. Use the `module avail` command on Oscar to view the whole list or search for packages. See our manual page on [Software](../software/software.md) to understand how software modules work. Additional packages can be requested by submitting a support ticket to `support@ccv.brown.edu`.

### What compilers are available on Oscar?

By default, the `gcc` compiler is available when you login to Oscar, providing the GNU compiler suite of `gcc` \(C\), `g++` \(C++\), and `gfortran`. We also provide compilers from Intel \(`intel` module\) and the Portland Group \(`pgi` module\). For more information, visit our manual page on [Software](../software/software.md).

### How do I get information about finished jobs?

The `sacct` command will list all of your completed jobs since midnight of the previous day \(as well as running and queued jobs\). You can pick an earlier start date with the `-S` option, e.g. `sacct -S 2012-01-01`.

### How much storage am I using?

The `myquota` command on Oscar will print a summary of your usage on the home, data, and scratch file systems. For more information, see our manual page on [File Systems](../managing-files/filesystem.md).

### My job keeps terminating unexpectedly with a "Killed" message, or without any errors. What happened?

These are symptoms of not requesting enough memory for your job. The default memory allocation is about 3 GB. If your job is resource-intensive, you may need to specifically allocate more. See the [user manual](../submitting-jobs/batch.md#sbatch-command-options) for instructions on requesting memory and other resources.

### How do I request a certain amount of memory per CPU?

Specify the SLURM option `--mem-per-cpu=` in your script.

### How do I link against a BLAS and LAPACK library?

We recommend linking against the Intel Math Kernels Library \(MKL\) which provides both BLAS and LAPACK. The easiest way to do this on Oscar is to include the special environment variable `$MKL` at the end of your link line, e.g. `gcc -o blas-app blas-app.c $MKL`. For more complicated build systems, you may want to consult the [MKL Link Line Advisor](http://software.intel.com/en-us/articles/intel-mkl-link-line-advisor).

## RUNNING JOBS

### How is a job identified?

By a unique JobID, e.g. `13180139`

### Which of my jobs are running/pending?

Use the command `myq`

### How do I check the progress of my running job?

You can look at the output file. The default output file is slurm-%j.out" where %j is the JobID. If you specified and output file using `#SBATCH -o output_filename` and/or an error file `#SBATCH -e error_filename` you can check these files for any output from your job. You can view the contents of a text file using the program `less` , e.g.

```text
less output_filename
```

Use the `spacebar` to move down the file, `b` to move back up the file, and `q` to quit.

### My job is not running how I indented it too. How do I cancel the job?

`scancel <JobID>` where `<JobID>` is the job allocation number, e.g. `13180139`

### How do I save a copy of an interactive session?

You can use `interact -o outfile` to save a copy of the session's output to "outfile"

I've submitted a bunch of jobs. How do I tell which one is which? `myq` will list the running and pending jobs with their JobID and the name of the job. The name of the job is set in the batch script with `#SBATCH -J jobname`. For jobs that are in the queue \(running or pending\) you can use the command `scontrol show job <JobID>` where `<JobID>` is the job allocation number, e.g.`13180139` to give you more detail about what was submitted.

### How do I ask for a haswell node?

Use the `--constraint` \(or `-C`\) option:

```text
#SBATCH --constraint=haswell
```

You can use the `--constraint` option restrict your allocation according to other features too. The `nodes` command provides a list of "features" for each type of node.

### What are the nodes in the "smp" partition?

SMP stands for symmetric multiprocessing. These nodes are meant to be useful with jobs which use a large numbers of CPUs on the same node for **shared memory parallelism**. However, comparing sequentially they can be much slower because their architecture is quite old.

### Why won't my job start?

When your job is pending \(PD\) in the queue, SLURM will display a reason why your job is pending. The table below shows some common reasons for which jobs are kept pending.

| Reason | Meaning |
| :--- | :--- |
| \(None\) | You may see this for a short time when you first submit a job |
| \(QOSGrpCpuLimit\) | All your condo cores are currently in use |
| \(Priority\) | Jobs with higher priority are using the resources |
| \(Resources\) | There are not enough free resources to fulfill your request |
| \(JobHeldUser\) | You have put a hold on the job. The job **will not run** until you lift the hold. |
| \(ReqNodeNotAvail\) | The resources you have requested are not available. Note this normally means you have requested something impossible, e.g. 100 cores on 1 node, or a 24 core sandy bridge node. Double check your batch script for any errors. Your job **will never run** if you are requesting something that does not exist on Oscar. |
| \(PartitionNodeLimit\) | You have asked for more nodes than exist in the partition. For example if you make a typo and have specified -N \(nodes\) but meant -n \(tasks\) and have asked for more than 64 nodes. Your job **will never run**. Double check your batch script. |

### Why is my job taking so long to start? Just waiting in \(Priority\) or \(Resources\)

1. **Overall system busy**: when tens of thousands of jobs are submitted it total by all users, the time it takes SLURM to process these into the system may increase from the normal almost instantly to a half-hour or more. 
2. **Specific resource busy**: if you request very specific resources \(e.g., a specific processor\) you then have to wait for that specific resource to become available while other similar resources may be going unused. 
3. **Specified resource not available**: if you request something that is not or may never be available, your job will simply wait in the queue. E.g., requesting 64 GB of RAM on a 64 GB node will never run because the system needs at least 1 GB for itself so you should reduce your request to less than 64. 

## TRANSFERING FILES

### How do I transfer big files to/from Oscar?

Please use the server **transfer.ccv.brown.edu**

1. From your machine to Oscar:  scp file1.txt userid@transfer.ccv.brown.edu From Oscar to another machine: ssh transfer transfer&gt; scp file1.txt userid@your-machine-name 
2. Alternatively, Oscar has an endpoint for "Globusonline" \([https://www.globus.org](https://www.globus.org)\) that you can use to more effectively transfer files. See our manual page on how to use [Globus Online](../managing-files/filetransfer/using-globus.md) to transfer files.

## XSEDE

### What is XSEDE?

[XSEDE](http://www.xsede.org) is an NSF-funded, nationwide collection of supercomputing systems that are available to researchers through merit-based allocations. It replaces what used to be called the TeraGrid. CCV participates in the Campus Champions program and has a small pool of compute time available for Brown researchers to test out XSEDE resources.

### How do I request access to XSEDE?

If you would like help getting started with XSEDE and obtaining a startup allocation, please contact `support@ccv.brown.edu` with a description of your project and which XSEDE systems you would like to access. We can also assist you in preparing an allocation request for longer-term access to larger resources.

### How do I access XSEDE resources?

See [https://portal.xsede.org/single-sign-on-hub](https://portal.xsede.org/single-sign-on-hub).

## Cloud HPC Options

The use of cloud resources for HPC varies according to your demands and circumstances. Cloud options are changing rapidly both in service providers and various services being offered. For those who have short-term needs that don't demand the highest of computational performance, a cloud option might be appropriate. For others, a local option customized to individual needs may be better. The cost of cloud services also varies quite a bit and includes not only compute time but data transfer charges. Other issues involved licensing, file synchronization, etc.

We are actively investigating a number of options to connect Brown users seamlessly to suitable cloud options. We are collecting such information for publishing on the CIS website as part of research services available. At this point, the best course of action is to request an individual consultation to help address your specific needs. Please send email to support@ccv. brown.edu.

