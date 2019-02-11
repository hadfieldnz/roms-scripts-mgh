# ROMS environment examples

This file contains example Bash code snippets to set up the environment for building
and running ROMS

Gfortran 4.8.5 on CentOS 7
```
function set-roms-gfortran ()
{
    echo Setting environment variables for ROMS with GFORTRAN

    export FC=gfortran
    export FORT=${FC}

    # CentOS keeps its module files in a non-standard location,
    # so we have to specify the netCDF interface locations
    # explicitly
    export USE_NETCDF4=
    export NETCDF_INCDIR=/usr/lib64/gfortran/modules
    export NETCDF_LIBDIR=/usr/lib64
    export NETCDF_LIBS=-lnetcdff

    export MCT_INCDIR=${HOME}/.local/include
    export MCT_LIBDIR=${HOME}/.local/lib

    export USE_MPIF90=on
    export PATH=/usr/lib64/openmpi/bin:${PATH}
}
```
Gfortran 7.4.0 on Cygwin
```
function set-roms-gfortran ()
{
    echo Setting environment variables for ROMS with GFORTRAN

    export FC=gfortran
    export FORT=${FC}

    export USE_NETCDF4=on;

    export USE_MPIF90=on;

    export MCT_INCDIR=/usr/local/include;
    export MCT_LIBDIR=/usr/local/lib
}
```
Gfortran 7.1.0 on the [NeSI Maui CS500 ancillary nodes](https://support.nesi.org.nz/hc/en-gb/articles/360000203776-M%C4%81ui-Ancillary-Nodes)
```
function set-roms-gfortran ()
{
    echo Setting environment variables for ROMS with Gfortran

    module load GCC/7.1.0 netCDF-Fortran/4.4.4-GCC-7.1.0

    export FORT=gfortran
    export FC=gfortran
    export CC=gcc

    export PLATFORM=$(uname -s -m | tr " " "-")-gnu

    export USE_NETCDF4=on

    export MCT_INCDIR=${HOME}/.local/${PLATFORM}/include
    export MCT_LIBDIR=${HOME}/.local/${PLATFORM}/lib
}
```
The Cray programming environment on the [NeSI Maui XC50 supercomputer](https://support.nesi.org.nz/hc/en-gb/articles/360000163695-M%C4%81ui)
```
function set-roms-cray ()
{
    echo Setting environment variables for ROMS with PrgEnv-cray

    module unload PrgEnv-gnu PrgEnv-intel
    module load PrgEnv-cray cray-netcdf cray-hdf5

    export FORT=ftn-cray
    export FC=ftn
    export CC=cc

    export PLATFORM=$(uname -s -m | tr " " "-")-cray

    export USE_NETCDF4=
    export NETCDF_INCDIR=/opt/cray/pe/netcdf/4.6.1.2/cray/8.6/include
    export NETCDF_LIBDIR=/opt/cray/pe/netcdf/4.6.1.2/cray/8.6/lib

    export MCT_INCDIR=${HOME}/.local/${PLATFORM}/include
    export MCT_LIBDIR=${HOME}/.local/${PLATFORM}/lib

    # See NeSI Support ticket 22772
    export HDF5_USE_FILE_LOCKING=FALSE
}
```
The Intel programming environment on the [NeSI Maui XC50 supercomputer](https://support.nesi.org.nz/hc/en-gb/articles/360000163695-M%C4%81ui)
```
function set-roms-intel ()
{
    echo Setting environment variables for ROMS with PrgEnv-intel

    module unload PrgEnv-cray PrgEnv-gnu
    module load PrgEnv-intel cray-netcdf cray-hdf5

    export FORT=ftn-intel
    export FC=ftn
    export CC=cc

    export PLATFORM=$(uname -s -m | tr " " "-")-intel

    export USE_NETCDF4=
    export NETCDF_INCDIR=/opt/cray/pe/netcdf/4.6.1.2/intel/16.0/include
    export NETCDF_LIBDIR=/opt/cray/pe/netcdf/4.6.1.2/intel/16.0/lib

    export MCT_INCDIR=${HOME}/.local/${PLATFORM}/include
    export MCT_LIBDIR=${HOME}/.local/${PLATFORM}/lib

    # See NeSI Support ticket 22772
    export HDF5_USE_FILE_LOCKING=FALSE
}
```
The Gnu programming environment on the [NeSI Maui XC50 supercomputer](https://support.nesi.org.nz/hc/en-gb/articles/360000163695-M%C4%81ui)
```
function set-roms-gnu ()
{
    echo Setting environment variables for ROMS with PrgEnv-gnu

    module unload PrgEnv-cray PrgEnv-intel
    module load PrgEnv-gnu cray-netcdf cray-hdf5

    export FORT=ftn-gnu
    export FC=ftn
    export CC=cc

    export PLATFORM=$(uname -s -m | tr " " "-")-gnu

    export USE_NETCDF4=
    export NETCDF_INCDIR=/opt/cray/pe/netcdf/4.6.1.2/gnu/7.1/include
    export NETCDF_LIBDIR=/opt/cray/pe/netcdf/4.6.1.2/gnu/7.1/lib

    export MCT_INCDIR=${HOME}/.local/${PLATFORM}/include
    export MCT_LIBDIR=${HOME}/.local/${PLATFORM}/lib

    # See NeSI Support ticket 22772
    export HDF5_USE_FILE_LOCKING=FALSE
}
```
