---
description: >-
  This page is designed to give a brief introduction to how to build a
  singularity image through the various methods available.
---

# Building Images

For more information regarding building a singularity container, the [Building a Container](https://singularity.lbl.gov/docs-build-container) documentation is excellent and I would recommend giving it a look.

## From SingularityHub

You can use the `build` command to download a container from Singularity Hub.

```text
$ singularity build <finalImageName>.simg shub://<singularityHubURL>
```

The first argument \(`<finalImageName>.simg`\) specifies a path and name for your container. The second argument \(`shub://<singularityHubURL>`\) gives the Singularity Hub URI from which to download.

{% hint style="info" %}
Note, you do not actually use the `<>` when entering your path/name or url.
{% endhint %}

## From DockerHub

If you already have a desired docker container that you would like to build as a singularity image for use on OSCAR, you can build directly from dockerHub using the build command:

```text
$ singularity build <finalImageName>.simg docker://<dockerHubURL>
```

This will pull the docker image from DockerHub and build it as a singularity image locally.

