# Zisa                                                               {#mainpage}                                        
This repository contains the combined source code of Zisa. If you like to use
and IDE to navigate all of Zisa rather than just one library at a time, please
use this repository.

## Quickstart
Start by cloning the repository
```
git clone --recursive https://github.com/1uc/Zisa.git
```
and change into the newly created directory. If you forgot the `--recursive`
you could run
```
git submodule init
git submodule update
```
Presumably you'll want to make changes to the source code. If so, please make
sure the submodule track the branch `main` or a feature branch
```
git submodule foreach 'git checkout main'
```
See [Superbuilds] for details.

Now, proceed to install the dependencies:
```
bin/install_dir.sh COMPILER DIRECTORY       \
                   [--zisa_has_mpi={0,1}]   \
                   [--zisa_has_cuda={0,1}]
```
they will be placed into a subdirectory of `DIRECTORY` and print
part of the CMake command needed to include the dependencies. `COMPILER` must
be replaced with the compiler you want to use.

If this worked continue by adding [project specific flags] to the CMake
command. If not it's not going to be a quick start. Please read
[Dependencies] and then [Building].

[project specific flags]: @ref cmake_flags
[Dependencies]: dependencies.md
[Building]: cmake.md
[Superbuilds]: @ref superbuilds
