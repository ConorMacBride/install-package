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

If you want to use the latest available version of this action instead
of hard-coding a specific version, you can replace
``ConorMacBride/install-package@v1`` by ``ConorMacBride/install-package@main``.
