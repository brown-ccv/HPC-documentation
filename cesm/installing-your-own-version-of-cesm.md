# Installing your own version of CESM

These instructions are for users who need to download their own version of CESM2

{% hint style="warning" %}
Do not load the CESM module. If you have a cesm module loaded, unload it:

`module unload cesm`
{% endhint %}

```text
git clone -b release-cesm2.1.1 https://github.com/ESCOMP/cesm.git
cd cesm
./manage_externals/checkout_externals
```

The repository [https://github.com/hkershaw-brown/oscar\_cime](https://github.com/hkershaw-brown/oscar_cime) has Oscar appropriate files you can use:

* config\_batch.xml
* config\_compilers.xml
* config\_machines.xml

To create your own ~/.cime directory:

`git clone https://github.com/hkershaw-brown/oscar_cime .cime`

To setup, build and run on Oscar

```text
module load netcdf/4.7.0_intel2019.3 hdf5/1.10.0 mpi/mvapich2-2.3a_intel esmf/8.0.0b perl/5.18.2 intel/2019.3 blas/3.7.0 yaml-cpp/0.6.2_intel2019.3 lapack/3.6.0
cd cime/scripts
./create_newcase --case CASENAME --compset COMPSET --res GRID --mach oscar
```

line 1. Load CESM dependencies

line 2. cd to cime scripts directory

line 3. create a new case using 'oscar' for the machine

{% hint style="info" %}
Note the **./** for ./create\_newcase
{% endhint %}

