---
title: Cuda Compiling
date: '2019-01-31T22:03:45.000Z'
draft: false
project: Oscar
section: GPU Computing
weight: 0
icon: check
---

# Compiling CUDA

## Compiling with CUDA

To compile a CUDA program on Oscar, first load the CUDA [module](https://github.com/brown-ccv/HPC-documentation/tree/274acf2ee119a42697ed887d0deb64f3f06d57c1/doc/software/README.md) with:

```text
$ module load cuda
```

The CUDA compiler is called `nvcc`, and for compiling a simple CUDA program it uses syntax similar to `gcc`:

```text
$ nvcc -o program source.cu
```



