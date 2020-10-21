# GitHub Action: eic/setup-spack
This GitHub Action sets up Spack for use in GitHub Workflows.

## Instructions
You can use this GitHub Action in a workflow in your own repository by with `uses: eic/setup-spack@main`.

For example, the file `.github/workflows/test.yml` could include the following stanza:
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: eic/setup-cvmfs@main
    - uses: eic/setup-spack@main
```
Note: Since the default value for spack_root points to a directory on the CernVM-FS at `/cvmfs`, we also include `uses: eic/setup-cvmfs@main`.

## Optional Parameters
The following parameters are supported:
- `spack_root` (optional, defaults to `/cvmfs/eic.opensciencegrid.org/packages/spack/current`): the root of the Spack package repository.
- `environment` (optional, defaults to empty): the environment to load, if any.

## Minimal Example

The following minimal example, which is also a workflow in this repository at [.github/workflows/minimal-usage.yml](https://github.com/eic/setup-spack/tree/main/.github/workflows/minimal-usage.yml), setups up Spack and lists the installed packages.
```yaml
name: Test setup-spack action
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: eic/setup-cvmfs@main
    - uses: eic/setup-spack@main
    - name: List packages in Spack
      run: |
        spack find
```

## What Does This Action Do?

This GitHub Action loads the [Spack](https://github.com/spack/spack) package manager from the optionally specified `spack_root` directory, and optionally loads the environment specified as the arguments `environment`.

## Limitations

This GitHub Action makes no attempt at caching. Frequent use may incur overhead on the servers you are accessing.
