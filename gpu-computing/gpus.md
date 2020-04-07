# GPUs on Oscar

{% hint style="info" %}
To view the various GPUs available on Oscar, use the command

`nodes gpu`
{% endhint %}

## Interactive Use

To start an [interactive](../submitting-jobs/interact.md) session on a GPU node, use the `interact` command and specify the `gpu` partition. You also need to specify the requested number of GPUs using the `-g` option:

```text
$ interact -q gpu -g
```

To start an interactive session on a particular GPU type \(v100, QuadroRTX, 1080ti, p100 etc\) use the feature `-f` option:

```text
interact -q gpu -f v100
```

## GPU Batch Job

For production runs, please submit a [batch job](../submitting-jobs/batch.md) to the `gpu` partition. E.g. for using 1 GPU:

```text
$ sbatch -p gpu --gres=gpu:1 <jobscript>
```

This can also be mentioned inside the batch script:

```text
#SBATCH -p gpu --gres=gpu:1
```

You can view the status of the `gpu` partition with:

```text
$ allq gpu
```

Sample batch script for CUDA program:

```text
~/batch_scripts/cuda.sh
```

## Getting started with GPUs

While you can program GPUs directly with CUDA, a language and runtime library from NVIDIA, this can be daunting for programmers who do not have experience with C or with the details of computer architecture.

You may find the easiest way to tap the computation power of GPUs is to link your existing CPU program against numerical libraries that target the GPU:

* [CUBLAS](https://developer.nvidia.com/cublas) is a drop-in replacement for BLAS libraries that runs BLAS routines on the GPU instead of the CPU.
* [CULA](http://www.culatools.com) is a similar library for LAPACK routines.
* [CUFFT](https://developer.nvidia.com/cufft), [CUSPARSE](https://developer.nvidia.com/cusparse), and [CURAND](https://developer.nvidia.com/curand) provide FFT, sparse matrix, and random number generation routines that run on the GPU.
* [MAGMA](http://icl.cs.utk.edu/magma) combines custom GPU kernels, CUBLAS, and a CPU BLAS library to use both the GPU and CPU to simultaneously use both the GPU and CPU; it is available in the 'magma' module on Oscar.
* Matlab has a [GPUArray](https://www.mathworks.com/help/distcomp/gpuarray.html) feature, available through the Parallel Computing Toolkit, for creating arrays on the GPU and operating on them with many built-in Matlab functions. The PCT toolkit is licensed by CIS and is available to any Matlab session running on Oscar or workstations on the Brown campus network.
* [PyCUDA](http://documen.tician.de/pycuda/) is an interface to CUDA from Python. It also has a [GPUArray](http://documen.tician.de/pycuda/array.html) feature and is available in the `cuda` module on Oscar.

## OpenACC

OpenACC is a portable, directive-based parallel programming construct. You can parallelize loops and code segments simply by inserting directives - which are ignored as comments if OpenACC is not enabled while compiling. It works on CPUs as well as GPUs. We have the PGI compiler suite installed on Oscar which has support for compiling OpenACC directives. To get you started with OpenACC:

* [Introduction to OpenACC Online Course](https://developer.nvidia.com/intro-to-openacc-course-2016)
* [PGI Accelerator Compilers with OpenACC Directives](https://www.pgroup.com/resources/accel.htm)
* [Getting Started with OpenACC](https://devblogs.nvidia.com/parallelforall/getting-started-openacc)
* [Running OpenACC Programs on NVIDIA and AMD GPUs](https://www.pgroup.com/lit/presentations/ieee_webinar_dec2013_slides.pdf)

### MATLAB

[GPU Programming in Matlab](http://www.mathworks.com/company/newsletters/articles/gpu-programming-in-matlab.html)

## NVLink Enabled GPU Nodes

NVLink enables GPUs to pool memory over high speed links \(25 G/s\). This will increase performance of your application code.

Nodes `gpu[1210,1211,1212]`have 4 fully connected NVLink \(SXM2\) V100 GPUs.

To submit interactive job to NVLink Enabled GPU nodes:

```text
interact -q gpu -f v100
```

To submit batch job\(s\) add following line to your batch script.

```text
#SBATCH --constraint=v100
```

