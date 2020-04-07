---
description: >-
  There are three main ways to run a Singularity image on OSCAR. As an
  interactive shell, using the exec command, or building a runscript and using
  the run command.
---

# Running Images

The most likely usage of your singularity environment will be via utilizing either [singularity exec](https://singularity.lbl.gov/docs-exec) or [singularity run](https://singularity.lbl.gov/docs-run). These can be directly executed via a batch script or through an interactive job in place of your traditional execution scripts. For more information about the methods of running a singularity image, the [Singularity quickstart](https://singularity.lbl.gov/quickstart) guide is pretty handy.

{% hint style="info" %}
Treat the running of a singularity container like any other executable or codebase on OSCAR. **Do not run singularity containers directly on the login nodes**. Instead, they should be run either via an interactive or batch job, or via the terminal within a VNC session.
{% endhint %}

## Singularity Shell

This will launch an interactive shell within a singularity instance based on the designated image. This should be used when you are testing/debugging the image or intend to use it via the interact/VNC methods.

```text
$ singularity shell <imagePath>
```

This method is only applicable when working with an interact slurm job, or via the terminal within a VNC session.

## Singularity Execute Instructions

The next method is to launch the image with a defined set of instructions. This will launch the singularity image, and execute whatever commands are defined by the user.

```text
$ singularity exec <imagePath> <commands>
```

Here, the commands can range from running a script, loading modules, or piping multiple instructions together. To see an example of this process, see the [Example - Tensorflow](example-tensorflow.md) section where we execute a script to run within the singularity image.

## Run Image Instructions

The last method we will go over here is via singularities run command, which will execute a series of instructions provided to the image in the form of a runscript. This script will automatically execute if the image is either launch using the run command, or if the singularity image is directly executed.

```text
$ singularity run <imagePath>
```

or

```text
./<imagePath>
```

In both cases, we are executing the container’s “runscript” \(the executable `/singularity` at the root of the image\).

{% hint style="info" %}
For more information about singularity run and the associated runscript, we recommend the run documentation using `singularity run help` or visiting the [singularity run](https://singularity.lbl.gov/docs-run) documentation.
{% endhint %}

