# actions-use-homebrew-tools

![actions-use-homebrew-tools](https://github.com/tecolicom/actions-use-homebrew-tools/actions/workflows/test.yml/badge.svg)

This GitHub action installs homebrew packages and cache them for later
use.  When executed next time with same package list, and any other
environment are not changed, installed files are extracted from the
cached archive.

When valid cached archive is not found, all packages are installed by
`brew` command.  Incremental installation is not supported.

This actions assumes `brew` command is already installed.  So please
install it before calling if not available.

Installed files are taken by comparing directory before and after
installation.  So it takes time to find them if many files are already
installed before command execution.

By default, only files under the directory returned by `brew --prefix`
will be archived.  If the `brew` command installs files in other
directories, specify them with the `path` parameter.

Output is same as
[`@actions/cache`](https://github.com/actions/cache).

## Usage

```yaml
# inputs:
#   tools:   { required: true,  type: string }
#   key:     { required: false, type: string }
#   path:    { required: false, type: string }
#   cache:   { required: false, type: string, default: yes }
#   verbose: { required: false, type: boolean, default: false }

- uses: tecolicom/actions-use-homebrew-tools@v1
  with:

    # homebrew packages
    tools: ''

    # Additional cache key
    key: ''

    # Additional path required other than $(brew --prefix)
    path: ''

    # Cache strategy
    #
    # yes:      activate cache
    # no:       no cache
    # workflow: effective within same workflow (mainly for test)
    #
    cache: yes

    # verbose: show verbose output
    verbose: false
```

## Example

```yaml
- uses: tecolicom/actions-use-homebrew-tools@v1
  with:
    tools: rcs
```

## See Also

### [tecolicom/actions](https://github.com/tecolicom/actions)

### [`@tecolicom/actions-install-and-cache`](https://github.com/tecolicom/actions-install-and-cache)

This action is just a glue for
[`@actions-install-and-cache`](https://github.com/tecolicom/actions-install-and-cache).
