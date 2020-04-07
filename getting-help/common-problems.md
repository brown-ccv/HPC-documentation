# Common Problems

## VNC problems

**Solution:**

1. Note that you have to use the same username and password that you

   use for SSH'ing to Oscar.

2. Make sure you are using the latest version from the [VNC page](https://github.com/brown-ccv/HPC-documentation/tree/274acf2ee119a42697ed887d0deb64f3f06d57c1/getting-help/vnc/README.md)
3. Check the Java version on your computer. We recommend at least java

   version 8.

4. SSH to Oscar \(not through VNC\) and run the command "`myq`" to see if

   there are any VNC jobs running. If there are, cancel those jobs

   using the command "`scancel <jobID>`". Now try using VNC.

5. Make sure you are not over disk quota using the command "`myquota`".

## Disk quota exceeded

This means that either your home, data or scratch directory is over its disk quota limit and the grace period has also expired \(or you have hit the highest possible limit too\).

The command to monitor your disk quota usage is:

```text
myquota
```

Example output:

```text
                   Block Limits                              |           File Limits              
Type    Filesystem           Used    Quota   HLIMIT    Grace |    Files    Quota   HLIMIT    Grace
-------------------------------------------------------------|--------------------------------------
USR     home               8.401G      10G      20G        - |    61832   524288  1048576        -
USR     scratch              332G     512G      12T        - |    14523   323539  4194304        -
FILESET data+apollo        11.05T      20T      24T        - |   459764  4194304  8388608        -
```

There are limits on the amount of data as well as number of files. "Grace" is the grace period you have left after you exceed the quota. After the grace period expires, you will not be allowed to write to files and a "disk quota exceeded" error will be shown. "HLIMIT" is the highest limit which can't be breached even in the grace period.

If you find you are above quota limits, you can delete or compress files to bring down your usage. If your home directory is over limits, you can move files to your data directory. You can also simply ask your PI to get additional storage allocation. Here are the [rates](https://github.com/brown-ccv/HPC-documentation/tree/274acf2ee119a42697ed887d0deb64f3f06d57c1/getting-help/doc/rates/README.md).

## Your account has expired

We set an expiry date on all student accounts and guest accounts. This is to avoid misuse of those accounts and prevent cluttering up of the system after those users have become inactive or are no longer at Brown.

In case you want to continue using CCV resources and face this error while logging in, simply send us an e-mail at support@ccv.brown.edu and we will reactivate your account. If you have an estimated graduation date, let us know so that we can set the expiry around that time.

## **Warning: Remote host identification has changed**

**Error:** Offending RSA key in ~/.ssh/known\_hosts:**4**. This indicates you have an offending RSA key at line no. 4

**Solution 1**

```text
$ vi ~/.ssh/known_hosts
remove line no: 4.
Save and Exit, and Retry.
```

**Solution 2**

```bash
ssh-keygen -R "ssh.ccv.brown.edu"
```

## GLIBCXX\_&lt;version&gt; not found OR cc1plus: error: unrecognized command line option "-std=c++11"

**Solution:** Run your program after loading a more recent gcc module. For example,

```text
 module load gcc/5.4
```

The default version of `gcc` on Oscar is 4.8.5 which comes installed as part of the OS.

## Prompted twice for password - Deleted files in `~/.ssh` directory by mistake

**Solution:** Run `setup_ssh` from command line when logged in to Oscar. This will restore your SSH key files.

## How to restore files deleted by mistake?

**Solution:** See the "Restoring Files" section on the [file systems](../managing-files/filesystem/restore.md) page.

## Error while loading shared libraries - Cannot open shared object file - Library not found

**Solution:** Many programs are compiled with dynamic linking to libraries on which they depend. The dynamic linker called `ld` looks for these dependencies during run time and complains if it can't find them.

Example:

```text
libmpichcxx.so not found
```

Here, it is looking for a library which is part of MPI implementations. You can load a module like `mvapich2` so that the path to this library is added to `LD_LIBRARY_PATH` and can be found by the run time linker. It might happen that only a particular version is required. A web search on the library name also might reveal what software package it belongs to.

If you want to know what all shared libraries are required during run time by an executable, you can use the `ldd` utility. For example:

```text
    $ ldd /gpfs/runtime/opt/paraview/4.2.0/bin/paraview
  linux-vdso.so.1 =>  (0x00007fffecfff000)
  /usr/local/lib/libslurm.so (0x00007f70f8348000)
  libc.so.6 => /lib64/libc.so.6 (0x0000003e18800000)
  libdl.so.2 => /lib64/libdl.so.2 (0x0000003e19000000)
  libpthread.so.0 => /lib64/libpthread.so.0 (0x0000003e19400000)
  /lib64/ld-linux-x86-64.so.2 (0x0000003e18400000)
```

We generally make it a point to add information about these dependencies to the modules such that the info is displayed while loading modules. If you find a package for which dependencies are not displayed while loading modules or you are not able to figure out where to find the library file, contact us at support@ccv.brown.edu and we will correct the mistake.

## Perl module not found

**Solution:** In most cases, you can check whether a module exists using the command:

```text
 perldoc -l Module::Name
```

For example,

```text
$ perldoc -l Math::CDF
/gpfs/runtime/opt/perl/5.18.2/lib/site_perl/5.18.2/x86_64-linux-thread-multi/Math/CDF.pm
```

If it does not exist, you can email us.

Also, chances are that you are using the "wrong" Perl to execute your script. Check the first line of the script. Does it say:

```text
 #!/usr/bin/perl
```

If yes, it is using the Perl executable `/usr/bin/perl` instead of the one under "perl/5.18.2" \(the module for this is loaded by default on Oscar\). This line is called a "shebang". This should be fine as such, but sometimes it may produce errors due to conflict between the Perl versions.

Change this to:

```text
 #!/usr/bin/env perl
```

so that it uses the first Perl executable in your PATH environment variable which should be the 5.18.2 version.

## All other errors

Generally, by doing a web search on the error, you can find out the issue, if not solve it. Do a web search on the actual error message \(usually starts with "Error:"\). Other information displayed with the message is also important, but including that in the web search might make it too specific and filter out useful results.

Finally, feel free to send us an email at support@ccv.brown.edu if you are not able to resolve the issue.

