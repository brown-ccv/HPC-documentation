# Job Arrays

A job array is a collection of jobs that all run the same program, but on different values of a parameter. It is very useful for running parameter sweeps, since you don't have to write a separate batch script for each parameter setting.

To use a job array, add the option:

```text
#SBATCH --array=<range>
```

in your batch script. The range can be a comma separated list of integers, along with ranges separated by a dash. For example:

```text
1-20
1-10,12,14,16-20
```

A job will be submitted for _each_ value in the range. The values in the range will be substituted for the variable `$SLURM_ARRAY_TASK_ID` in the remainder of the script. Here is an example of a script for running a serial Matlab script on 16 different parameters by submitting 16 different jobs as an array:

```bash
#!/bin/bash
#SBATCH -J MATLAB
#SBATCH -t 1:00:00
#SBATCH --array=1-16

# Use '%A' for array-job ID, '%J' for job ID and '%a' for task ID
#SBATCH -e arrayjob-%a.err
#SBATCH -o arrayjob-%a.out

echo "Starting job $SLURM_ARRAY_TASK_ID on $HOSTNAME"
matlab -r "MyMatlabFunction($SLURM_ARRAY_TASK_ID); quit;"
```

You can then submit the multiple jobs using a single `sbatch` command:

```text
$ sbatch <jobscript>
```

For more info: [https://slurm.schedmd.com/job\_array.html](https://slurm.schedmd.com/job_array.html)

