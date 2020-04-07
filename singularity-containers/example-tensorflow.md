---
description: >-
  The following is a brief example of building a tensorflow container from a
  DockerHub recipe, and using via the batch command to run a tensorflow project
  without loading any specific modules.
---

# Example - Tensorflow

## Getting the Container Built

First, I go to the official dockerHub Tensorflow page, and decide on which release I am interested in. For this example, I will use the latest python3 deployment. Following the instructions provided in the [Building Images](building-images.md) section:

```text
singularity build <finalImageName>.simg docker://<dockerHubURL>
```

becomes

```text
singularity build tf-py3.simg docker://tensorflow/tensorflow:1.14.0
```

Once entering the command, singularity will begin to compile the container. During the build process, the .singularity directory is used as a temporary cache location. Be aware of this is if you are nearing or at the hard quota limit in your home directory.

```text
[mk100@login003 ~]$ singularity build tf-py3.simg docker://tensorflow/tensorflow:latest-py3
Docker image path: index.docker.io/tensorflow/tensorflow:latest-py3
Cache folder set to /gpfs_home/mk100/.singularity/docker
[6/6] |===================================| 100.0% 
Importing: base Singularity environment
Exploding layer: sha256:7b722c1070cdf5188f1f9e43b8413157f8dfb2b4fe84db3c03cb492379a42fcc.tar.gz
Exploding layer: sha256:5fbf74db61f1459176d8647ba8f53f8e6cf933a2e56f73f0e8da81213117b7e9.tar.gz
Exploding layer: sha256:ed41cb72e5c918bdbd78e68f02930a3f1cf1d6079402b0a5b19de8508e67b766.tar.gz
Exploding layer: sha256:7ea47a67709ebea8efed59fbda703dbd00a0d2cae7e2808959744bfa30bfc0e9.tar.gz
Exploding layer: sha256:38e64f576f172feb568fa37796b3f563d0e60a2ba24b1eac2fad31df27214dc5.tar.gz
Exploding layer: sha256:ccae7f1b5fc083f600889513fd8b1d7601bc2923f1ae68f9d2bf66bb090832f9.tar.gz
Exploding layer: sha256:101128cef006ac70fa8be20e4a37ee7e63f24f873e26b44a013fe454894abc8e.tar.gz
Exploding layer: sha256:823f589d99e57b951ef7b273171950b53d68d0bc04eb822f30350057006b59a0.tar.gz
Exploding layer: sha256:602fd2bed0f1c6c68a6c0fb5aec0a864b0fe8858d5a854c4288782373d569599.tar.gz
Exploding layer: sha256:1313b3c833db39b4bf83b56b436cbcd245cfc485c50a300793d5d09c7df210e1.tar.gz
Exploding layer: sha256:51b06a4999c72e68d37588051e489e7864d9a166e3cdd9cfd4e0df9efff476f1.tar.gz
WARNING: Building container as an unprivileged user. If you run this container as root
WARNING: it may be missing some functionality.
Building Singularity image...
Singularity container built: tf-py3.simg
Cleaning up...
```

Once built, you will have a new file in your current directory named tf-py3.simg.

## Running Our Tensorflow Container

Now that we have our tensorflow container, we can run it either interactively \(interactive slurm job using [singularity shell](https://singularity.lbl.gov/docs-shell)\) or as a batch job through the existing slurm sbatch command. I will demonstrate a simple sbatch script which will submit a job to launch the container and execute a python script which requires tensorflow.

The sbatch script seen below

```bash
#!/bin/bash
#SBATCH -J myTestSingularity
#SBATCH --ntasks=1
#SBATCH --ntasks-per-node=1
#SBATCH --time=1:00:00
#SBATCH --mem=14GB
#SBATCH --partition=batch

# Print key runtime properties for records
echo Master process running on `hostname`
echo Directory is `pwd`
echo Starting execution at `date`
echo Current PATH is $PATH

# Launch singulairty container and execute python command to run tf_NN.py
singularity exec $HOME/simgTest/tensorflowPy3.simg python $HOME/simgTest/tf_NN.py
```

Notice for previous workflows \(non-singularity based\), we would have loaded python3 and tensorflow, then had our sbatch script run `python3 myProgram`. Now, instead you run the `singularity exec` command with the desired singularity image \(containing tensorflow\), and provide the corresponding `python myProgram` as a command argument.

See below attached the sample batch script, and tf\_NN.py tensorflow python code to run as this demo.

{% file src="../.gitbook/assets/tf\_nn.py" caption="Tensorflow Sample Python Code" %}

{% file src="../.gitbook/assets/singularity\_sbatch\_tf3.sh" caption="Sample Batch Script" %}

