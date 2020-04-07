# Intro to CUDA

## Introduction to CUDA

[CUDA](https://developer.nvidia.com/what-cuda) is an extension of the C language, as well as a runtime library, to facilitate general-purpose programming of NVIDIA GPUs. If you already program in C, you will probably find the syntax of CUDA programs familiar. If you are more comfortable with C++, you may consider instead using the higher-level [Thrust](http://thrust.github.com) library, which resembles the Standard Template Library and is included with CUDA.

In either case, you will probably find that because of the differences between GPU and CPU architectures, there are several new concepts you will encounter that do not arise when programming serial or threaded programs for CPUs. These are mainly to do with how CUDA uses threads and how memory is arranged on the GPU, both described in more detail below.

There are several useful documents from NVIDIA that you will want to consult as you become more proficient with CUDA:

* [CUDA C Programming Guide](http://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html)
* [CUDA C Best Practices Guide](http://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html)
* [CUDA Runtime API](http://docs.nvidia.com/cuda/cuda-runtime-api/index.html)

There are also many CUDA tutorials available online:

* [CUDA Training](https://developer.nvidia.com/cuda-training) from NVIDIA
* [CUDA, Supercomputing for the Masses](http://www.drdobbs.com/parallel/cuda-supercomputing-for-the-masses-part/207200659)
* [CUDA Tutorial](http://supercomputingblog.com/cuda/cuda-tutorial-1-getting-started/) from The Supercomputing Blog

### Threads in CUDA

CUDA uses a data-parallel programming model, which allows you to program at the level of what operations an individual thread performs on the data that it owns. This model works best for problems that can be expressed as a few operations that all threads apply in parallel to an array of data. CUDA allows you to define a thread-level function, then execute this function by mapping threads to the elements of your data array.

A thread-level function in CUDA is called a **kernel**. To launch a kernel on the GPU, you must specify a **grid**, and a decomposition of the grid into smaller **thread blocks**. A thread block usually has around 32 to 512 threads, and the grid may have many thread blocks totalling thousands of threads. The GPU uses this high thread count to help it hide the latency of memory references, which can take 100s of clock cycles.

Conceptually, it can be useful to map the grid onto the data you are processing in some meaningful way. For instance, if you have a 2D image, you can create a 2D grid where each thread in the grid corresponds to a pixel in the image. For example, you may have a 512x512 pixel image, on which you impose a grid of 512x512 threads that are subdivided into thread blocks with 8x8 threads each, for a total of 64x64 thread blocks. If your data does not allow for a clean mapping like this, you can always use a flat 1D array for the grid.

The CUDA runtime dynamically schedules the thread blocks to run on the **multiprocessors** of the GPU. The M2050 GPUs available on Oscar each have 14 multiprocessors. By adjusting the size of the thread block, you can control how much work is done concurrently on each multiprocessor.

### Memory on the GPU

The GPU has a separate memory subsystem from the CPU. The M2050 GPUs have GDDR5 memory, which is a higher bandwidth memory than the DDR2 or DDR3 memory used by the CPU. The M2050 can deliver a peak memory bandwidth of almost 150 GB/sec, while a multi-core Nehalem CPU is limited to more like 25 GB/sec.

The trade-off is that there is usually less memory available on a GPU. For instance, on the Oscar GPU nodes, each M2050 has only 3 GB of memory shared by 14 multiprocessors \(219 MB per multiprocessor\), while the dual quad-core Nehalem CPUs have 24 GB shared by 8 cores \(3 GB per core\).

Another bottleneck is transferring data between the GPU and CPU, which happens over the PCI Express bus. For a CUDA program that must process a large dataset residing in CPU memory, it may take longer to transfer that data to the GPU than to perform the actual computation. The GPU offers the largest benefit over the CPU for programs where the input data is small, or there is a large amount of computation relative to the size of the input data.

CUDA kernels can access memory from three different locations with very different latencies: global GDDR5 memory \(100s of cycles\), shared memory \(1-2 cycles\), and constant memory \(1 cycle\). Global memory is available to all threads across all thread blocks, and can be transferred to and from CPU memory. Shared memory can only be shared by threads within a thread block and is only accessible on the GPU. Constant memory is accessible to all threads and the CPU, but is limited in size \(64KB\).

