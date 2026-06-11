# Usage

The template package includes a small greeter module as an example. Replace it
with your own package code after bootstrapping a new project.

## Run the example

```bash
uv run python examples/say_hi.py
```

## Use the package

```python
from project_name import Greeter, Language

greeter = Greeter("Mario", Language.IT)
message = greeter.greet()
```

The package exposes its public interface from `project_name.__init__`. Keep that
interface deliberate and document public classes, functions, and modules with
Google-style docstrings.
