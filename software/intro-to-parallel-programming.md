# Intro to Parallel Programming

This page serves as a guide for application developers getting started with parallel programming, or users wanting to know more about the working of parallel programs/software they are using.

Although there are several ways to classify parallel programming models, a basic classification is:

1. [Shared Memory Programming](intro-to-parallel-programming.md#shared-memory-parallelism)
2. Distributed Memory Programming

## Shared Memory Parallelism

This model is useful when all threads/processes have access to a common memory space. The most basic form of shared memory parallelism is **Multithreading**. According to Wikipedia, a [thread](https://en.wikipedia.org/wiki/Thread_%28computing%29) of execution is the smallest sequence of programmed instructions that can be managed independently by a scheduler \(Operating System\).

Note that most compilers have inherent support for multithreading up to some level. Multithreading comes into play when the compiler converts your code to a set of instructions such that they are divided into several independent instruction sequences \(threads\) which can be executed in parallel by the Operating System. Apart from multithreading, there are other features like "vectorized instructions" which the compiler uses to optimize the use of compute resources. In some programming languages, the way of writing the sequential code can significantly affect the level of optimization the compiler can induce. However, this is not the focus here.

Multithreading can also be induced at code level by the application developer and this is what we are interested in. If programmed correctly, it can also be the most "efficient" way of parallel programming as it is managed at the Operating System level and ensures optimum use of "available" resources. Here too, there are different parallel programming constructs which support multithreading.

### Pthreads

POSIX threads is a standardized C language threads programming interface. It is a widely accepted standard because of being lightweight, highly efficient and portable. The routine to create Pthreads in a C program is called `pthread_create` and an "entry point" function is defined which is to be executed by the threads created. There are mechanisms to synchronize the threads, create "locks and mutexes", etc. Help pages:

* Comprehensive tutorial page on [POSIX Threads Programming](https://computing.llnl.gov/tutorials/pthreads)
* [Compiling programs with Pthreads](https://computing.llnl.gov/tutorials/pthreads/#Compiling)

### OpenMP

OpenMP is a popular directive based construct for shared memory programming. Like POSIX threads, OpenMP is also just a "standard" interface which can be implemented in different ways by different vendors.

**Compiler directives** appear as comments in your source code and are ignored by compilers unless you tell them otherwise - usually by specifying the appropriate compiler flag \([https://computing.llnl.gov/tutorials/openMP](https://computing.llnl.gov/tutorials/openMP)\). This makes the code more portable and easier to parallelize. you can parallelize loop iterations and code segments by inserting these directives. OpenMP also makes it simpler to tune the application during run time using environment variables. for example, you can set the number of threads to be used by setting the environment variable `OMP_NUM_THREADS` before running the program. Help pages:

* [https://computing.llnl.gov/tutorials/openMP](https://computing.llnl.gov/tutorials/openMP)
* [Compiling OpenMP Programs](https://computing.llnl.gov/tutorials/openMP/#Compiling)

