# Setting Job Submission Settings

We have provided templates for you to use for job submission settings. These templates are in`/gpfs/runtime/opt/forge/19.1.2/templates`

Click `Run and debug a program` to open the following menu

![](../../.gitbook/assets/screen-shot-2019-08-05-at-3.20.08-pm.png)

Click `Configure` next to **Submit to Queue** and enter `/gpfs/runtime/opt/forge/19.1.2/templates/slurm-ccv.qtf` as the Submission template file

{% hint style="info" %}
`slurm-ccv-qtf` lets you specify the total number of tasks. The number of tasks may not be equal for each node. This option will be the shortest time in the queue, but may not give you consistent run times.

`slurm-ccv-mpi.qtf` is for MPI jobs where you want to specify number of nodes and tasks per node

`slurm-ccv-threaded.qtf` is for threaded \(single node\) jobs
{% endhint %}

![](../../.gitbook/assets/screen-shot-2019-08-05-at-3.22.32-pm.png)

