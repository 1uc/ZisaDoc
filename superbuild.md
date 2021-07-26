# Superbuilds                                                     {#superbuilds}
Zisa is organized in separate libraries. The code of each of these lives in a
separate git repository. This is different from the organization style where
the whole application is located in a single repository. In particular when it
comes to code navigation, the *other* parts of Zisa are treated as external
dependencies and are therefore not modifiable. This can be unwieldy. A solution
to this problem is something called superbuilds.

The variant we'll discuss here is intended to be used by developers, i.e.
people who want to navigate and modify the combined source code of Zisa. The
`zisa` repository is such a superbuild. The summary for using the Zisa
superbuild is:

    git clone --recursive git@github.com:1uc/zisa.git
    git submodule foreach "git checkout main"

then continue working as if they were a single combinded code base, organized
in separate independent git repositories.

The steps for creating a new superbuild are:

* Create an empty repository and add all required parts of Zisa to
  it as Git submodules. Now since the aim is to modify the code, each submodule
  must be up-to-date, i.e. on the `main` branch. This can be achieved by a
  ```
    git submodule foreach "git checkout main"
  ```

* A boilerplate top-level `CMakeLists.txt` must be created, which does two
  things:
  1. Replace `find_package` with a no-op for Zisa internal dependencies.
  2. Add all the subdirectories, which brings in the Zisa related targets.

* Tidy things up by adding the scripts required to manage any external
  dependencies.

## Random Notes
A couple of important things to refer back to:

* One can use `git clone --recursive URL` to checkout a repository
  with all it's submodules.

* When recursively cloning a repository with submodules, will be in detached
  HEAD mode and each submodule points to a commit with specific SHA. Detached
  HEAD is a bad place to start making modifications. Therefore, these developer
  superbuilds should work more naturally, if the submodules checkout the `main`
  branch.

* It seems that if the submodules track the `main` branch they behave much like
  independent Git repositories; and the normal workflow can be used in each
  repository, e.g., create a feature branch, commit changes, create pull request,
  etc.

* The literature mentions a "war over the SHA". That is, since in the outer
  repository the submodules are stored by means of just a SHA, updating this
  SHA is similar to updating a file which changes completely everytime.
  Therefore, there is a large potential for merge conflicts. Since in this
  variant of the superbuild the submodules checkout the branch `main` it's
  irrelevant which value of SHA the outer repo points to. Any reasonably current
  version which compiles seems like a sane value. Hence, I don't see these
  merge conflicts becoming a particular headache.

* Given how shallow the outer repository is, it's not clear it must be shared
  or pushed to a remote at all. A simple backup might be sufficient. Therefore,
  eliminating any non standard submodule related interations with other people.
