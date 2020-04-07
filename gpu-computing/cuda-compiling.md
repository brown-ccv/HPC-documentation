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

The CUDA compiler is called `nvcc`, and for compiling a simple CUDA program it uses syntax simlar to `gcc`:

```text
$ nvcc -o program source.cu
```

### Optimizations for Fermi

The Oscar GPU nodes feature NVIDIA M2050 cards with the Fermi architecture, which supports CUDA's "compute capability" 2.0. To fully utilize the hardware optimizations available in this architecture, add the `-arch=sm_20` flag to your compile line:

```text
$ nvcc -arch=sm_20 -o program source.cu
```

This means that the resulting executable will not be backwards-compatible with earlier GPU architectures, but this should not be a problem since CCV nodes only use the M2050.

### Memory caching

The Fermi architecture has two levels of memory cache similar to the L1 and L2 caches of a CPU. The 768KB L2 cache is shared by all multiprocessors, while the L1 cache by default uses only 16KB of the available 64KB shared memory on each multiprocessor.

You can increase the amount of L1 cache to 48KB at compile time by adding the flags `-Xptxas -dlcm=ca` to your compile line:

```text
$ nvcc -Xptxas -dlcm=ca -o program source.cu
```

If your kernel primarily accesses global memory and uses less than 16KB of shared memory, you may see a benefit by increasing the L1 cache size.

If your kernel has a simple memory access pattern, you may have better results by explicitly caching global memory into shared memory from within your kernel. You can turn off the L1 cache using the flags `–Xptxas –dlcm=cg`.

