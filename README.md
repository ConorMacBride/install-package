## install-package

[![.github/workflows/main.yml](https://github.com/ConorMacBride/install-package/actions/workflows/test_action.yml/badge.svg)](https://github.com/ConorMacBride/install-package/actions/workflows/test_action.yml)

A GitHub action to install packages with apt on Linux, brew and brew cask on macOS and choco on Windows.

## Inputs
- `brew: [package ...]` (macOS)
- `brew-cask: [package ...]` (macOS)
- `apt: [package ...]` (Linux)
- `choco: [package ...]` (Windows)
  
All inputs are accepted on all platforms, however, each input's string of packages are only installed if the platform is supported.

## Example

```yaml
jobs:
  test_code:
    name: Test code
    runs-on: ubuntu-latest
    steps:
      - uses: ConorMacBride/install-package@v1
        with:
          brew: hello yq
          brew-cask: MacVim
          apt: rolldice bcal
          choco: graphviz less
```

As the runner OS is Linux, only `rolldice` and `bcal` are installed.

## Notes

This action is intended to be used within an action, workflow or reusable workflow where the `runner.os` is variable, such as setting the runner from a matrix:

```yaml
jobs:
  test_code:
    name: Test code
    runs-on: ${{ matrix.os }}
    strategy:
      matrix: ...
    steps:
      - ...
      - uses: ConorMacBride/install-package@v1
        with:
          brew: openjpeg
          apt: libopenjp2-7
      - ...
```

This can simplify your configurations, as this action takes care of choosing which package manager to use.
It also allows for variations in the package names between package managers.

However, if the `runner.os` always stays the same in your workflow, or you are only configuring one package manager, it may be better to call the commands yourself rather than adding a new dependency to your workflow.
For example,

```yaml
jobs:
  test_code:
    name: Test code
    runs-on: ubuntu-latest
    steps:
      # ... this step:
      - uses: ConorMacBride/install-package@v1
        with:
          apt: libopenjp2-7
      # ... should probably be replaced with this step:
      - runs: sudo apt update && sudo apt install -y libopenjp2-7
```

If you want to use the latest available version of this action instead
of hard-coding a specific version, you can replace
``ConorMacBride/install-package@v1`` by ``ConorMacBride/install-package@main``.
