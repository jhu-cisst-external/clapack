# CLAPACK

This repository is based on http://netlib.org/clapack/clapack-3.2.1-CMAKE.tgz  For the orginal README, see README.install

CLAPACK provides the same functions as LAPACK but the original FORTRAN code has been converted to C using f2c (and we assume many other manual changes).  It is useful on OSs that don't come with a FORTRAN compiler.  Unfortunately this package has not been updated for a while (since 2009) so we created our own "fork" to apply minor patches to compile with recent OSs/compilers.

# Builds

We currently disabled the compilation of most tests so we use GitHub actions just to make sure we can compile the core libraries.  We're currently testing:
- ubuntu-latest with gcc and clang
- macos-latest with clang
- windows-latest with cl

[![CMake on multiple platforms](https://github.com/jhu-cisst-external/clapack/actions/workflows/cmake-multi-platform.yml/badge.svg)](https://github.com/jhu-cisst-external/clapack/actions/workflows/cmake-multi-platform.yml)
