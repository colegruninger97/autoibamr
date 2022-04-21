autoibamr
=========

The ``autoibamr.sh`` shell script downloads, configures, builds, and installs
[ibamr](https://ibamr.github.io) with common dependencies on
Linux and macOS computers.

`autoibamr` is based on candi: https://github.com/dealii/candi

Dependencies
----

autoibamr requires that your present machine already have a working copy of MPI
and the standard MPI compiler wrappers installed. If you want to use custom MPI
compiler wrappers then you should set `CC`, `CXX`, and `FC` to full paths to the
C, C++, and Fortran compilers, respectively.

Several IBAMR dependencies require using MPI compiler wrappers, so providing
`MPI_ROOT` and using a separate compiler toolchain is presently not supported.

Quickstart
----

The following commands download the current stable version of the installer and
then install the latest IBAMR release and common dependencies:

```bash
  git clone https://github.com/ibamr/autoibamr.git
  cd autoibamr
  ./autoibamr.sh
```

Follow the instructions on the screen
(you can abort the process by pressing < CTRL > + C)


### Installation

If you are on a cluster you will typically want to run `module load mpi` to set
up the correct MPI environment. After that you can run

```bash
  ./autoibamr.sh
```

Working with IBAMR examples
----
autoibamr sets up IBAMR and its dependencies for use in external projects. It
can be used to develop IBAMR itself in two different ways:
1. The IBAMR source directory, is, by default, `autoibamr/tmp/unpack/IBAMR-0.10.1/`
   and the build directory is `autoibamr/tmp/build/v0.10.1/`. While this is not
   the intended way to use autoibamr, you can compile and run examples from the
   build directory after installation.
2. You can install your own development copy of IBAMR that uses the dependencies
   installed by autoibamr. To do this you should provide the `--dependencies-only`
   flag and then download and compile IBAMR yourself after autoibamr finishes.
3. Finally, you could set up the IBAMR examples as external projects configured
   with CMake in the normal way by copying and pasting them.

Advanced Configuration
----

### Command line options

#### Help: ``[-h]``, ``[--help]``
You can get a list of all command line options by running
```bash
  ./autoibamr.sh -h
  ./autoibamr.sh --help
```

You can combine the command line options given below.

#### Prefix path: ``[-p <path>]``, ``[-p=<path>]``, ``[--prefix=<path>]``
```bash
  ./autoibamr.sh -p "/path/to/install/dir"
  ./autoibamr.sh -p="/path/to/install/dir"
  ./autoibamr.sh --prefix="/path/to/install/dir"
```

#### Multiple build processes: ``[-j<N>]``, ``[-j <N>]``, ``[--jobs=<N>]``
```bash
  ./autoibamr.sh -j<N>
  ./autoibamr.sh -j <N>
  ./autoibamr.sh --jobs=<N>
```

* Example: to use 2 build processes type ``./autoibamr.sh -j 2``.

#### Debug mode: `--enable-debugging`
```bash
  ./autoibamr.sh --enable-debugging
```
Sets up a debug build, where dependencies are compiled with assertion checking,
debug symbols, and optimizations and IBAMR is compiled with assertions, no
optimizations, and debug symbols.

#### Platform-specific optimizations: `--enable-native-optimizations`
```bash
  ./autoibamr.sh --enable-native-optimizations
```
Turns on processor-specific optimizations. Incompatible with debug mode.

#### User interaction: ``[-y]``, ``[--yes]``, ``[--assume-yes]``
```bash
  ./autoibamr.sh -y
  ./autoibamr.sh --yes
  ./autoibamr.sh --assume-yes
```

With this option you skip the user interaction. This might be useful if you
submit the installation to the queueing system of a cluster.

By default both libMesh and SILO will be set up and used as dependencies. They
can be disabled with `--disable-libmesh` and `--disable-silo` respectively.

### Configuration file options

Some less-used configuration options are available in `autoibamr.cfg`. In a
future version of autoibamr these features will become command-line arguments.
