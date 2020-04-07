# Arm Forge

[Arm Forge](https://www.arm.com/products/development-tools/server-and-hpc/forge) is available on Oscar. There are two products, DDT \(debugger\) and MAP \(performance reports\).

We recommend you use the Arm Forge remote client to launch your debugging jobs on Oscar. The first time you set up Arm Forge you will need to configure the client with the following steps:

1. Download the [arm forge remote client](https://developer.arm.com/tools-and-software/server-and-hpc/arm-architecture-tools/downloads/download-arm-forge) on your machine.
2. [Configuring Remote Launch from the client](configuring-remote-launch.md)
3. [Set up Job Submission Settings](setting-job-submission-settings.md)

{% hint style="info" %}
Compile your code with `-g` so you can see the source code in your debugging session
{% endhint %}

**Arm DDT**

Arm DDT is a powerful graphical debugger suitable for many different development environments, including:

* Single process and multithreaded software.
* OpenMP.
* Parallel \(MPI\) software.

## Arm MAP

Arm MAP is a parallel profiler that shows you which lines of code took the most time to run, and why. Arm MAP does not require any complicated configuration, and you do not need to have experience with profiling tools to use it.

Arm MAP supports:

* MPI, OpenMP and single-threaded programs.
* Small data files. All data is aggregated on the cluster and only a few megabytes written to disk, regardless of the size or duration of the run.
* Sophisticated source code view, enabling you to analyze performance across individual functions.
* Both interactive and batch modes for gathering profile data.
* A rich set of metrics, that show memory usage, floating-point calculations and MPI usage across processes, including:
  * Percentage of vectorized instructions, including AVX extensions, used in each part of the code.
  * Time spent in memory operations, and how it varies over time and processes, to verify if there are any cache bottlenecks.
  * A visual overview across aggregated processes and cores that highlights any regions of imbalance in the code.

