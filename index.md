---
layout: home
---
This is [IBM CODAIT](http://codait.org)'s [PyTorch](https://pytorch.org) prebuilt packages for
[IBM Z](https://www.ibm.com/it-infrastructure/z) and
[LinuxONE](https://www.ibm.com/it-infrastructure/linuxone). Our build is currently minimal and
supports CPU only. This project is still in its beta phase, and any feedback is welcome.

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

    $ pip install https://github.com/CODAIT/pytorch-on-z/raw/packages/torch-1.9.0-cp36-cp36m-linux_s390x.whl

For Python 3.8, run:

    $ pip install https://github.com/CODAIT/pytorch-on-z/raw/packages/torch-1.9.0-cp38-cp38-linux_s390x.whl

For Python 3.9, run:

    $ pip install https://github.com/CODAIT/pytorch-on-z/raw/packages/torch-1.9.0-cp39-cp39-linux_s390x.whl

## Known Issues

Not all tests for the C++ library can pass for PyTorch version 1.8.1 and 1.8.2.

## How We Built These Packages

We built the packages as follows on RHEL 8 on LinuxONE.

1. Create an empty virtual environment and activate it:

        $ python3.9 -m venv ~/.pytorch-build  # Replace python3.9 with python3.8/python3.6 if building for Python 3.8/3.6
        $ . ~/.pytorch-build/bin/activate

1. Clone PyTorch source code and check out the PyTorch version to build:

        $ git clone --recursive https://github.com/pytorch/pytorch.git
        $ cd pytorch
        $ git checkout v1.9.0
        $ git submodule update --recursive

1. Install dependencies:

        $ pip install -r requirements.txt
        $ pip install wheel

1. Run the build commands:

        $ DEBUG=0 CMAKE_EXPORT_COMPILE_COMMANDS=YES USE_OPENMP=0 USE_DISTRIBUTED=0 USE_MKLDNN=0 USE_NCCL=0 USE_CUDA=0 USE_PYTORCH_QNNPACK=0 USE_XNNPACK=0 USE_QNNPACK=0 USE_NNPACK=0 USE_QNNPACK=0 USE_FBGEMM=0 BUILD_TEST=1 USE_NUMA=OFF python3 setup.py develop --cmake-only
        $ MAX_JOBS=1 python setup.py develop

1. Run the tests:

        $ python test/run_test.py

1. Create the package:

        $ python setup.py bdist_wheel

Now the package should be available in the directory `dist/`.
