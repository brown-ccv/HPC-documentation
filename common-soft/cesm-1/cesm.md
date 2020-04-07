# Using a CESM module

There are several versions of CESM available as modules

`cesm/1.2.1` `cesm/1.2.2` `cesm/2.1.1`

[CESM2 ](http://www.cesm.ucar.edu/models/cesm2/)is the current supported version by NCAR.

To load a particular version:

`module load cesm/2.1.1`

Be sure to load the dependencies - these are printed in the load message for the CESM module. For example for cesm/2.1.1

`module load netcdf/4.7.0_intel2019.3 hdf5/1.10.0 mpi/mvapich2-2.3a_intel esmf/8.0.0b perl/5.18.2 intel/2019.3 blas/3.7.0 yaml-cpp/0.6.2_intel2019.3 lapack/3.6.0`

The following example shows how to create a new case on Oscar.

```text
create_newcase --case /gpfs/scratch/ccvtest/cesm2_C --res T62_g17 --compset C --machine oscar
./case.setup
./case.build 
./xmlchange JOB_WALLCLOCK_TIME=0:20:00 --subgroup case.run
./case.submit
```

line 4. shows how to use xmlchange to change run options. For a full list of options you can change with xmlchange:

`./xmlquery --listall`

{% hint style="warning" %}
Note for CESM2 you can have a directory ~/.cime with your own cime files. Be aware of this if you are switching between your own install and the module install.
{% endhint %}

