# Install linuxdeploy

[![CI](https://github.com/pcolby/install-linuxdeploy/actions/workflows/ci.yaml/badge.svg?branch=main)](
  https://github.com/pcolby/install-linuxdeploy/actions/workflows/ci.yaml)
[![CodeQL](https://github.com/pcolby/install-linuxdeploy/actions/workflows/github-code-scanning/codeql/badge.svg?branch=main)](
  https://github.com/pcolby/install-linuxdeploy/actions/workflows/github-code-scanning/codeql)

GitHub Action for installing [linuxdeploy] with optional plugins.

## Usage

```yaml
- uses: pcolby/install-linuxdeploy@v1
```

## Options

### `arch`

The target architecture to install [linuxdeploy] for. This can be any architecture that [linuxdeploy] releases binaries
for. Defaults to match the architecture of the current workflow runner (typically `x86_64`).

### `dir`

The target directory to install [linuxdeploy] to. Defaults to `${RUNNER_TEMP}/linuxdeploy`.

### `install-deps`

Whether or not to install known `apt` dependencies. Defaults to `true`.

### `plugins`

Space-separated list of optional [linuxdeploy] plugins to install. Any plugins directly listed in the
[Awesome linuxdeploy!] listing should be supported, such as `appimage` and `qt`.

Each plugin may be suffixed with a version, like `qt@v1.2.3`, to specify which version of that plugin to install. Note,
however, for plugins with actual releases (such as `appimage` and `qt`), the version is a GitHub release tag, but for
unreleased plugins (such as `gtk` and `gstreamer`) the version is a ref name or commit hash. If no version suffix is
provided, released plugins default to match the [`version`](#version) option, while unreleased plugins defualt to their
default branch (ie `master`).

> [!TIP]
> As per the [AppImage plugin's `README.md` file:](
> https://github.com/linuxdeploy/linuxdeploy-plugin-appimage?tab=readme-ov-file#updating-the-appimage-plugin)
>
> > The official linuxdeploy AppImage ships with a fairly recent version of the plugin.
>
> So while you _can_ install a specific version of the `appimage` plugin via `plugins`, which will override the default
> one shipped with [linuxdeploy], it usually isn't necessary for that plugin.

### `set-env`

Whether or not to update the `$PATH` environment variable to include the installation `dir`. Defaults to `true`.

### `version`

The [linuxdeploy] version to install, as well as the _default_ version for any `plugins` entries that don't specify a
version.

> [!IMPORTANT]
> Currently this defaults to `continuous`, as [linuxdeploy] has no official stable release yet. But at some point
> this will likely default to the most recent stable [linuxdeploy] version that has been tested with this action.

### Example with all options

```yaml
- name: Install linuxdeploy
  uses: pcolby/install-linuxdeploy@v1
  with:
    arch: x86_64
    dir: ${{ runner.temp }}/linuxdeploy
    install-deps: true
    plugins: appimage gtk@master qt
    set-env: true
    version: continuous
```

[Awesome linuxdeploy!]: https://github.com/linuxdeploy/awesome-linuxdeploy
[linuxdeploy]: https://github.com/linuxdeploy/linuxdeploy
