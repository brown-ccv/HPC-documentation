# Using Modules

CCV uses the [PyModules](https://bitbucket.org/mhowison/pymodules) package for managing the software environment on OSCAR. The advantage of the modules approach is that it allows multiple versions of the same software to be installed at the same time. With the modules approach, you can "load'' and "unload'' modules to dynamically control your environment.

## Module commands

| command |  |
| :--- | :--- |
| `module list` | Lists all modules that are currently loaded in your software environment. |
| `module avail` | Lists all available modules on the system. Note that a module can have multiple versions. |
| `module help name` | Prints additional information about the given software. |
| `module load name` | Adds a module to your current environment. If you load using just the name of a module, you will get the default version. To load a specific version, load t he module using its full name with the version: "module load gcc/6.2" |
| `module unload name` | Removes a module from your current environment. |

## Finding modules

The `module avail` command allows searching modules based on partial names. For example:

```text
 $ module avail bo
```

will list all available modules whose name starts with "bo".

Output:

```text
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ name: bo*/* ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
boost/1.49.0        boost/1.63.0        bowtie2/2.3.0
boost/1.62.0-intel  bowtie/1.2.0
```

This feature can be used for finding what versions of a module are available.

## Auto-completion using tab key

The `module load` command supports **auto-completion** of the module name using the "tab" key. For example, writing `module load bo`"on the shell prompt and hitting "tab" key a couple of times will show results similar to that shown above. Similarly, the `module unload` command also auto completes using the names of modules which are loaded.

## Modules loaded at startup

You can customize the default environment that is loaded when you login by putting the appropriate module commands in the `.modules` file in your home directory. For instance, if you edited your `.modules` file to contain

```bash
module load python/3.5.2
```

python/3.5.2 will be loaded every time you log in.

## What modules actually do...

Loading a module sets the relevant environment variables like `PATH`, `LD_LIBRARY_PATH` and `CPATH`. For example, PATH contains all the directory paths \(colon separated\) where executable programs are searched for. So, by setting PATH through a module, now you can execute a program from anywhere in the file-system. Otherwise, you would have to mention the full path to the executable program file to run it which is very inconvenient. Similarly, LD\_LIBRARY\_PATH has all the directory paths where the run time linker searches for libraries while running a program, and so on. To see the values in an environment variable, use the `echo` command. For instance, to see what's in PATH:

```text
$ echo $PATH
/gpfs/runtime/opt/perl/5.18.2/bin:/gpfs/runtime/opt/python/2.7.3/bin:/gpfs/runtime/opt/java/7u5/bin:
/gpfs/runtime/opt/intel/2013.1.106/bin:/gpfs/runtime/opt/centos-updates/6.3/bin:/usr/lib64/qt-3.3/bin:
/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/opt/ibutils/bin:/gpfs/runtime/bin
```

