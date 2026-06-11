# Building Documentation

Documentation is part of the normal project build. Treat documentation changes
like code changes: update the source files, build locally, and let CI run the
same strict build before merging.

## Source files

Write manual documentation as Markdown files in `docs/`. These files are parsed
by MyST, so standard Markdown works and Sphinx directives can be used when you
need richer technical documentation.

Keep API documentation in Python docstrings. Public modules, classes, and
functions should use Google-style docstrings. The API reference imports
`project_name` during the Sphinx build and renders those docstrings
automatically.

## Local build

Install the documentation dependencies once:

```bash
uv sync --extra dev --extra docs
```

Build the documentation exactly as CI builds it:

```bash
uv run tox -e docs
```

This runs:

```bash
python -m sphinx -W --keep-going -b html docs docs/_build/html
```

The `-W` flag turns documentation warnings into failures. Broken links,
malformed directives, bad API references, and import errors should be fixed
before merging. The generated HTML is written to `docs/_build/html` and is not
committed.

## Live preview

Use the live server while editing prose or docstrings:

```bash
uv run sphinx-autobuild docs docs/_build/html
```

The live server is for authoring convenience. The canonical check remains
`uv run tox -e docs`.

## CI build

GitHub Actions runs the documentation build in a dedicated `docs` job. The job
installs the docs extra, runs `tox -e docs`, and uploads `docs/_build/html` as a
workflow artifact. Pull requests should not be merged when this job fails.

## Read the Docs

Read the Docs uses `.readthedocs.yaml` and builds from `docs/conf.py`. It also
uses a warning-as-error Sphinx build, so local and CI failures should match the
published documentation build closely.

## Updating the API reference

The default API page is `docs/api.md`. Add additional `automodule`,
`autoclass`, or `autofunction` directives there when the package grows and you
want a more explicit API structure.
