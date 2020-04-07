# MPI Jobs

Resources from the web on getting started with MPI:

* [https://computing.llnl.gov/tutorials/mpi](https://computing.llnl.gov/tutorials/mpi)
* [http://mpitutorial.com](http://mpitutorial.com/)
* [http://www.math-cs.gordon.edu/courses/cps343/presentations/Intro\_to\_MPI.pdf](http://www.math-cs.gordon.edu/courses/cps343/presentations/Intro_to_MPI.pdf)

MPI is a standard that dictates the semantics and features of "message passing". There are different implementations of MPI. Those installed on Oscar are

* MVAPICH2
* OpenMPI

We recommend using MVAPICH2 as it is integrated with the SLURM scheduler and optimized for the Infiniband network.

## MPI modules on Oscar

The MPI module is called "mpi". The different implementations \(mvapich2, openmpi, different base compilers\) are in the form of versions of the module "mpi". This is to make sure that no two implementations can be loaded simultaneously, which is a common source of errors and confusion.

```text
$ module avail mpi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ name: mpi*/* ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
mpi/cave_mvapich2_2.3b_gcc    mpi/openmpi_1.10.7_gcc
mpi/cave_mvapich2_2.3b_intel  mpi/openmpi_1.8.3_gcc
mpi/mvapich2-2.3a_gcc         mpi/openmpi_2.0.3_gcc
mpi/mvapich2-2.3a_intel       mpi/openmpi_2.0.3_intel
mpi/mvapich2-2.3a_pgi         mpi/openmpi_2.0.3_pgi
mpi/mvapich2-2.3b_gcc
```

You can just use "`module load mpi`" to load the default version which is `mpi/mvapich2-2.3a_gcc`. This is the recommended version.

The module naming format is

```text
mpi/<implementation>-<version>_<base compiler>
```

### `srun` instead of `mpirun`

**Use `srun --mpi=pmi2` to run MPI programs.** All MPI implementations listed above except `openmpi_1.8.3_gcc` and `openmpi_1.10.7_gcc` are built with SLURM support. Hence, the programs need to be run using SLURM's `srun` command, except if you are using the above mentioned legacy versions.

The `--mpi=pmi2` flag is also required to match the configuration with which MPI is installed on Oscar.

## Running MPI programs - Interactive

To run an MPI program interactively, first create an allocation from the login nodes using the `salloc` command:

```text
$ salloc -N <# nodes> -n <# MPI tasks> -p <partition> -t <minutes>
```

For example, to request 4 cores to run 4 tasks \(MPI processes\):

```text
$ salloc -n 4
```

Once the allocation is fulfilled, you can run MPI programs with the `srun` command:

```text
$ srun --mpi=pmi2 ./my-mpi-program ...
```

When you are finished running MPI commands, you can release the allocation by exiting the shell:

```text
$ exit
```

Also, if you only need to run a single MPI program, you can skip the `salloc` command and specify the resources in a single `srun`command:

```text
$ srun -N <# nodes> -n <# MPI tasks> -p <partition> -t <minutes> --mpi=pmi2 ./my-mpi-program
```

This will create the allocation, run the MPI program, and release the allocation.

**Note: It is not possible to run MPI programs on compute nodes by using the `interact` command.**

`salloc` documentation: [https://slurm.schedmd.com/salloc.html](https://slurm.schedmd.com/salloc.html)

`srun` documentation: [https://slurm.schedmd.com/srun.html](https://slurm.schedmd.com/srun.html)

## Running MPI programs - Batch Jobs

Here is a sample batch script to run an MPI program:

```bash
#!/bin/bash

# Request an hour of runtime:
#SBATCH --time=1:00:00

# Use 2 nodes with 8 tasks each, for 16 MPI tasks:
#SBATCH --nodes=2
#SBATCH --tasks-per-node=8

# Specify a job name:
#SBATCH -J MyMPIJob

# Specify an output file
#SBATCH -o MyMPIJob-%j.out
#SBATCH -e MyMPIJob-%j.err

# Load required modules
module load mpi

srun --mpi=pmi2 MyMPIProgram
```

## Hybrid MPI+OpenMP

If your program has multi-threading capability using OpenMP, you can have several cores attached with a single MPI task using the `--cpus-per-task` or `-c` option with `sbatch` or `salloc`. The environment variable `OMP_NUM_THREADS` governs the number of threads that will be used.

```bash
#!/bin/bash

# Use 2 nodes with 2 tasks each (4 MPI tasks)
# And allocate 4 CPUs to each task for multi-threading
#SBATCH --nodes=2
#SBATCH --tasks-per-node=2
#SBATCH --cpus-per-task=4

# Load required modules
module load mpi

export OMP_NUM_THREADS=4
srun --mpi=pmi2 ./MyMPIProgram
```

The above batch script will launch 4 MPI tasks - 2 on each node - and allocate 4 CPUs for each task \(total 16 cores for the job\). Setting `OMP_NUM_THREADS` governs the number of threads to be used, although this can also be set in the program.

## Performance Scaling

The maximum theoretical speedup that can be achieved by a parallel program is governed by the proportion of sequential part in the program \(Amdahl's law\). Moreover, as the number of MPI processes increases, the communication overhead increases i.e. the amount of time spent in sending and receiving messages among the processes increases. For more than a certain number of processes, this increase starts dominating over the decrease in computational run time. This results in the overall program slowing down instead of speeding up as number of processes are increased.

**Hence, MPI programs \(or any parallel program\) do not run faster as the number of processes are increased beyond a certain point.**

If you intend to carry out a lot of runs for a program, the correct approach would be to find out the optimum number of processes which will result in the least run time or a reasonably less run time. Start with a small number of processes like 2 or 4 and first verify the correctness of the results by comparing them with the sequential runs. Then increase the number of processes gradually to find the optimum number beyond which the run time flattens out or starts increasing.

