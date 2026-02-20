# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

cfdb-models is a Python library defining shared data models (msgspec Structs and enums) for the cfdb ecosystem. It is intentionally kept separate from the core cfdb engine so dependent packages like cfdb-vars can reuse the models without pulling in the full engine.

## Ecosystem Context

This package provides the shared "definition" layer for the cfdb ecosystem. cfdb (sibling repo at `../cfdb`) imports `Type`, `Compressor`, `Axis`, and `DataType` from `cfdb_models.data_models`. cfdb keeps its own runtime structs (`DataVariable`, `CoordinateVariable`, `SysMeta`) locally since those are tightly coupled to its storage engine.

**cfdb-vars** is a separate package that will use cfdb-models to store predefined variable metadata definitions using `DataVarDef`, `CoordVarDef`, and `VarAttrs`.

## Common Commands

```bash
# Environment setup
uv sync

# Run tests
uv run pytest
uv run pytest cfdb_models/tests/test_file.py::test_name   # single test

# Linting and formatting
uv run ruff check .               # lint
uv run ruff check --fix .         # lint with auto-fix
uv run black .                    # format
uv run black --check --diff .     # format check only
uv run mypy --install-types --non-interactive cfdb_models  # type check

# Documentation
uv run mkdocs serve    # local dev server
uv run mkdocs build    # build static site

# Build and publish
uv build
uv publish
```

## Architecture

All data models live in a single module: `cfdb_models/data_models.py`. This file contains:

- **Enums** (`Type`, `Compressor`, `Axis`) — string-valued enums for dataset types, compression codecs, and coordinate axes
- **Structs** (msgspec.Struct subclasses) — `DataType`, `DataVarDef`, `CoordVarDef`
- **Attribute schemas** — `VarAttrs` (CF variable attributes), `DatasetAttrs` (CF global/group attributes)

`DataVarDef` and `CoordVarDef` are tagged unions (`tag` parameter) for variable definition templates. They use `DataType` for encoding info and can carry a `VarAttrs` for CF-compliant metadata.

Tests go in `cfdb_models/tests/`. The `conftest.py` file is the place for shared pytest fixtures.

## Code Style

- Line length: 120
- Formatter: black (skip string normalization)
- Target: Python 3.10+
- All imports must be absolute (relative imports are banned via ruff `TID` rules)
- Docstrings: Google style
- `cfdb_models` is configured as a known first-party package for import sorting
