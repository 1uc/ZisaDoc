# Dependencies
## Automated dependencies                              {#automated_dependencies}
Naturally, while it can be useful to be able to install each of the
dependencies manually, e.g., on a pesky cluster, for the most part this can be
automated in a script.

To install the dependencies use

    $ bin/install_dir.sh COMPILER DIRECTORY

which will install the dependencies into a subfolder of `DIRECTORY` and print
part of the CMake command needed to include the dependencies. `COMPILER` must
be replaced with the compiler you want to use.

If this worked continue by adding [project specific flags]

[project specific flags]: @ref cmake_flags

## Overview of dependencies
Zisa uses modern CMake to manage any dependencies it has. We've divided them
into four categories: *system dependencies* which are hard to install, low
level libraries; *common dependencies* these are properly packaged libraries;
*internal dependencies* meaning other parts of Zisa; and finally *scientific
dependencies* these are dependencies on other scientific codes, which may not
be nicely packaged and might not be open-source.

### System dependencies
We simply assume that these are present on the system. On a personal computer
these are installed using the package manager or something similar.

ZisaSFC has no system dependencies. Examples would be:
  * CUDA
  * MPI
  * HDF5
  * NetCDF


### Common dependencies
Since these are nicely packaged C++ libraries, we could use Spack to install
them. Create a Spack environment and add the required libraries.

Please refer to [Spack Details] for further details on how we use Spack.

[Spack Details]: spack.md

### Internal dependencies
These are distributed as source. Hence one must clone or download the
repository; then compile and install using typical CMake commands. Once they're
installed they are no different from common dependencies.

### Scientific dependencies
These are installed using custom scripts, check `bin/` for anything with a
related name. Note, that these dependencies are always optional, and not present
in all parts of Zisa.

