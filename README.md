# `install-linuxdeploy-action`

[![CI](https://github.com/pcolby/install-linuxdeploy-action/actions/workflows/test.yaml/badge.svg?branch=main)](
  https://github.com/pcolby/pcolby/install-linuxdeploy-action/actions/workflows/test.yaml)

GitHub Action for installing [linuxdeploy] with optional plugins.

## Usage

```yaml
- uses: pcolby/install-linuxdeploy-action@v1
```

## Options

### `arch`

The target architecture to install [linuxdeploy] for. This can be any architecture that [linuxdeploy] releases binaries
for, but typically you'd want to leave it to default to `x86_64`.

### `dir`

The target directory to install [linuxdeploy] to. Defaults to `${GITHUB_WORKSPACE}/linuxdeploy`.

### `install-deps`

Whether or not to install known `apt` dependencies. Defaults to `true`.

### `plugins`

Space-separated list of optional [linuxdeploy] plugins to install. Any plugins directly listed in the
[Awesome linuxdeploy!] listing should be supported, such as `appimage` and `qt`.

### `set-env`

Whether or not to update the `$PATH` environment variable to include the installation `dir`. Defaults to `true`.

### `version`

The [linuxdeploy] version to install, as well as the _default_ version for any `plugins` entries that don't specify a
version.

> [!IMPORTANT]
> Currently this defaults to `continuous`, as [linuxdeploy] currently has no official stable release, but at some point
> this will likely default to the most recent, current, tested stable [linuxdeploy] version.

### Example with all options

```
- name: Install linuxdeploy
  uses: pcolby/install-linuxdeploy-action@v1
  with:
    arch: x86_64
    dir: ${{ github.workspace }}/linuxdeploy
    install-deps: true
    plugins: qt
    set-env: true
    version: continuous
```

[Awesome linuxdeploy!]: https://github.com/linuxdeploy/awesome-linuxdeploy
[linuxdeploy]: https://github.com/linuxdeploy/linuxdeploy
