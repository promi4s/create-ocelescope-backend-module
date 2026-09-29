# create-ocelescope-backend-module

A [Copier](https://copier.readthedocs.io) template for an **Ocelescope** backend module: a FastAPI app that `ocelescope-backend` discovers through the `ocelescope_backend.modules` entry point.

## Create a backend module

In an [Ocelescope module project](https://github.com/promi4s/ocelescope-module-template), use its script, which also registers the module:

```sh
pnpm run add:backend my-module
```

Or on its own, with [uv](https://docs.astral.sh/uv/):

```sh
uvx copier copy gh:promi4s/create-ocelescope-backend-module my-module
```

You will be asked for the module name (defaults to the folder name), a short description and an author. All other names are derived from the module name:

| Module name  | Python project / package                                       | Module key       | Class            |
| ------------ | -------------------------------------------------------------- | ---------------- | ---------------- |
| `My Module`  | `ocelescope-module-my-module` / `ocelescope_module_my_module`   | `myModule`       | `MyModule`       |
| `OCEL Stats` | `ocelescope-module-ocel-stats` / `ocelescope_module_ocel_stats` | `ocelStats`      | `OCELStats`      |
| `3D Viewer`  | `ocelescope-module-3d-viewer` / `ocelescope_module_3d_viewer`   | `module3dViewer` | `Module3DViewer` |

The module is served under `/modules/<key>/v1`. A [frontend module](https://github.com/promi4s/create-ocelescope-frontend-module) with the same name generates its API client from this key by default.

## Update an existing module

Generated modules remember their answers in `.copier-answers.yml`. To pull template changes into a module, commit your work and run in its folder:

```sh
uvx copier update
```

## Developing this template

The generated module lives in [`template/`](template/). Files ending in `.jinja` are rendered with the answers from [`copier.yml`](copier.yml); other files are copied as-is. Try your local changes with:

```sh
uvx copier copy --vcs-ref HEAD . /tmp/test-module
```

or in a module project with `OCELESCOPE_BACKEND_TEMPLATE=/path/to/this/repo pnpm run add:backend test-module`.
