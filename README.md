Forked repository of GOTM for the implementation of CSIB2 in GOTM-FABM

CSIB2 code is in FABM

    GOTMcode/extern/fabm/src/models/uvic


## GOTM
GOTM - the **G**eneral **O**cean **T**urbulence **M**odel is an ambitious name for a one-dimensional water column model for marine and limnological applications. It is coupled to a choice of traditional as well as state-of-the-art parameterisations for vertical turbulent mixing. The package consists of the FORTRAN source code, a number of idealised and realistic test cases, and a scientific documentation, all published under the GNU public license.

A comprehensive description including compilation instructions are given at the official [GOTM homepage](http://www.gotm.net/portfolio/software).



# CSIB2 in GOTM-FABM

Instructions on downloading, compiling and running the model.

## Download code

Get GOTM and FABM code (this will downlowd code from various repos)
    
    git clone --recursive https://github.com/AntoineHaddon/GOTMcode.git

Get folders with forcing and parameter files for simulations
    
    git clone https://github.com/AntoineHaddon/GOTMcases.git


## Compiling

Code can compile succesfull but then fail to run if compiled with certain (newer?) versions of netcdf. Works with netCDF 4.7.3

Make some directories
    
    mkdir build && cd build && mkdir gotm && mkdir fabm

Build FABM
    
    cd fabm
    cmake ../../GOTMcode/extern/fabm -DFABM_HOST=gotm
    make install

Build GOTM
    
    cd ../gotm
    FABM=true && FABMDIR=../../GOTMcode/extern/fabm && FABM_PREFIX=~/local/fabm/gotm && FORTRAN_COMPILER=GFORTRAN && NETCDF_VERSION=NETCDF4
    cmake ../../GOTMcode -DGOTM_USE_STIM=ON -DGOTM_USE_FABM=ON
    make install


## Runing a simulation

    cd ../../GOTMcases/resolute
    ../../build/gotm/gotm
