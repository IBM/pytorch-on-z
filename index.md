This page hosts [PyTorch](https://pytorch.org) prebuilt packages for
[IBM Z](https://www.ibm.com/it-infrastructure/z) and
[LinuxONE](https://www.ibm.com/it-infrastructure/linuxone). This project is still in its beta phase,
and any feedback is welcome.

## Prerequisites

A GNU/Linux distribution with glibc >= 2.28. This includes
[RHEL 8](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux) and
[Ubuntu 20.04](https://ubuntu.com/).

You also need [BLAS](http://www.netlib.org/blas/) and [LAPACK](http://www.netlib.org/lapack/). On
RHEL, install them with

    $ sudo dnf install blas lapack

On Ubuntu, install them with

    $ sudo apt install libblas3 liblapack3

Additionally, building the dependency [NumPy](https://numpy.org/) (which will be automatically
executed when installing PyTorch) requires the Python development files, a C compiler, and a Fortran
compiler.

## Installation

To install the latest package, for Python 3.6, run:

    $ pip install https://github.com/CODAIT/pytorch-on-z/raw/packages/torch-1.8.1-cp36-cp36m-linux_s390x.whl

For Python 3.8, run:

    $ pip install https://github.com/CODAIT/pytorch-on-z/raw/packages/torch-1.8.1-cp38-cp38-linux_s390x.whl
