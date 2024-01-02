# Spack Quick Guide

To install Spack you must clone the repository:

    git clone https://github.com/spack/spack.git ${SPACK_DIR}

In every shell you want to use Spack perform:

    source ${SPACK_DIR}/share/spack/setup-env.sh

which will modify environment variables such as `PATH` to include `spack`.

## Spack Environments
These are much like Python virtual environments. First create a Spack
environment and activate it. Then add all dependencies and install everything

    spack env create zisa-deps
    spack env activate -p zisa-deps
    spack add ...
    spack install -j $(nproc)

The required dependencies are documented in a `spack-env.yml` found in each
component of Zisa.

Subsequently, activate the environment as follows:

    spack env activate -p zisa-deps

This will modify environment variables to ensure the dependencies are made
available. Notably, it sets `CMAKE_PREFIX_PATH` which ensures that
`find_package` can find the newly installed versions of, say, `Catch2`.

### Known Issues

After adding new dependencies, it's prudent to deactivate and activate the
environment again, since often important environment variables aren't updated
until the next `spack env activate`.

Adding the same dependency twice (with minor variations) will likely cause a
conflict since the same library is now listed twice, i.e. `spack add` does not
overwrite or update a dependency it adds a new one.

### Tricks

Use `spack config edit` to edit the environment.
