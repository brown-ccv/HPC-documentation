# About Oscar



Welcome to the CCV Oscar User Manual. Oscar is Brown University's supercomputer.

This user manual assumes you already have an Oscar account. If you do not have an Oscar account, you can request one by filling and submitting a [new user account form](https://brown.co1.qualtrics.com/jfe/form/SV_0GtBE8kWJpmeG4B).

{% hint style="info" %}
Anyone with a Brown account can get a free, exploratory account on Oscar.
{% endhint %}

Individuals external to Brown can get access to Oscar by having a sponsored Brown account. Please work with your department to get sponsored Brown accounts for any external collaborators.

If you publish research that benefited from the use of CCV services or resources, we would greatly appreciate an acknowledgment that states:

> This research \[Part of this research\] was conducted using \[computational/visualization resources and services at the Center for Computation and Visualization, Brown University.

## Important Notices

{% hint style="warning" %}
**Do not run computations or simulations on the login nodes**, because they are shared with other users. You can use the login nodes to compile your code, manage files, and launch jobs on the compute nodes.
{% endhint %}

{% hint style="warning" %}
**Large numbers of jobs submitted to Slurm on Oscar can cause problems.** If you are going to submit tens of thousands of jobs please bundle your work into fewer jobs. CCV staff can help you with this. Please email support@ccv.brown.edu with any questions
{% endhint %}

{% hint style="info" %}
**Oscar is a multi-node system**. If your code is serial or threaded then using multiple nodes will not make your code go faster. Restrict your job to running on one node with`#SBATCH -N 1`. Efficient use of resources helps everyone on Oscar. CCV staff can help you determine the best way to run your job. support@ccv.brown.edu
{% endhint %}

{% hint style="warning" %}
Files not accessed for 30 days will be deleted from your scratch directory. This is because scratch is high performance space. The fuller scratch is the worse the read/write performance. Use ~/data for files you need to keep long term.
{% endhint %}

