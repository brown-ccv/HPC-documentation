# Accessing Oscar Filesystem

By default, a Singularity image only have access to a limited set of paths once created. Without any special configurations, your $HOME \(`~/`\) and `/tmp/` \(among a few other system-specific locations\) are accessible from within a container. However, this will not automatically bind your `data/` or `scratch/` directories, and thus they will not be accessible. The easiest method to gain access to these directories is to use the **bind** functionality to mount these volumes to the container on runtime.

## Binding Using Command Line Arguments

Binding is achieved using the --bind or -B argument followed by the `<hostPath>:<containerPath>`

```bash
$ singularity shell -B /gpfs/scratch,/gpfs/data <yourContainer.simg>
```

This will bind `/data` and `/scratch` on from OSCAR's GPFS to `/data` and `/scratch` within the container, respectively. Doing this will allow any existing links you have to your data and scratch directories to function properly.

## Binding Using Environment Variables

An alternative approach is to use the `SINGULARITY_BINDPATH` environment variable which is used as a list of additional bind paths that will be included in any singularity commands you execute, including run and shell. Using the environment variable instead of the command line argument, this would be:

```bash
export SINGULARITY_BINDPATH="/gpfs/scratch,/gpfs/data"
singularity shell <yourContainer.simg>
```

You can add various additional command options to configure the read/write permissions for these mounted volumes. For more information regarding file or path binds, please see the official [Mounting and binding](https://singularity.lbl.gov/docs-mount) documentation from Singularity.

