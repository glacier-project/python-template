# project_name

This documentation is built with Sphinx. Manual pages are written in Markdown
with MyST, while the API reference is generated from Google-style Python
docstrings.

```{toctree}
:maxdepth: 2
:caption: Contents

template
documentation
usage
api
```

## Development

Install the documentation dependencies and run the live documentation server:

```bash
uv sync --extra dev --extra docs
uv run sphinx-autobuild docs docs/_build/html
```

Build the static site with:

```bash
uv run tox -e docs
```

## API reference

The API reference is generated directly from the package. Keep module, class,
and function docstrings current and the published API documentation will follow.
