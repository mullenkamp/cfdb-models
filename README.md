# cfdb-models

<p align="center">
    <em>data models for cfdb</em>
</p>

[![build](https://github.com/mullenkamp/cfdb-models/workflows/Build/badge.svg)](https://github.com/mullenkamp/cfdb-models/actions)
[![codecov](https://codecov.io/gh/mullenkamp/cfdb-models/branch/main/graph/badge.svg)](https://codecov.io/gh/mullenkamp/cfdb-models)
[![PyPI version](https://badge.fury.io/py/cfdb-models.svg)](https://badge.fury.io/py/cfdb-models)

---

**Source Code**: <a href="https://github.com/mullenkamp/cfdb-models" target="_blank">https://github.com/mullenkamp/cfdb-models</a>

---
## Overview
This package is meant to fully define the data model of cfdb using msgspec. This has been separated from the core cfdb package to abstract away the engine implementation from the data model. This will help in defining and assigning attribute templates for things like variables (e.g. cfdb-vars).

## Development

### Setup environment

We use [UV](https://docs.astral.sh/uv/) to manage the development environment and production build. 

```bash
uv sync
```

### Run unit tests

You can run all the tests with:

```bash
uv run pytest
```

### Format the code

Execute the following commands to apply linting and check typing:

```bash
uv run ruff check .
uv run black --check --diff .
uv run mypy --install-types --non-interactive cfdb_models
```

To auto-format:

```bash
uv run black .
uv run ruff check --fix .
```

## License

This project is licensed under the terms of the Apache Software License 2.0.
