# Building
Zisa uses CMake as a to building the project. Well, technically, to configure a
build system which can then build Zisa. If our variant of using CMake isn't
familiar, please read [CMake Usage].

## Project specific flags                                         {#cmake_flags}
The script for installing the dependencies generates part of the CMake command
required for compiling Zisa, see [Automated Dependencies]. You'll need to add
flags to control which dependencies should be used:

  * `-DZISA_HAS_MPI={0,1}` for MPI.
  * `-DZISA_HAS_CUDA={0,1}` for CUDA (experimental). Please report or fix issues.

Further, you should choose a build type:

  * `Debug` the CMake built in, essentially just `-g`.
  * `FastDebug` optimized build with debug symbols and assertions.
  * `Release` the CMake built in, essentially `-O3 -DNDEBUG`.

Running an unoptimized build can be very slow. Therefore, if you need only
semi-meaningful backtraces and want assertions, `FastDebug` is a good
choice. Now, for more specialized settings we provide:

  * `GPERFTOOLS` adds the flags required for `gperftools`, a sampling profiler.
  * `ASAN` adds the flags for Clangs AdressSanitizer.
  * `UBSAN` adds the flags for Clangs undefined behaviour sanitizer.

all three are based on an optimized build with debug symbols. Note that `ASAN`
and `UBSAN` expect the Clang compilers. The details can be found in `cmake/`.

## IDEs
The tested way of using Zisa in an IDE is to configure the IDE to pass the
required flags to CMake. In order to figure out which flags are needed you
could follow the instructions for the CLI and once you have the correct flags
copy-paste them into the settings menu of the IDE.

[CMake Usage]: @ref cmake_usage
[Automated Dependencies]: @ref automated_dependencies

