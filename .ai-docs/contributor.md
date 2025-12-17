# Contributor Guide

## Prerequisites
- **Python**: 3.10 or higher
- **Package Manager**: `poetry` or `uv` (recommended)

## Installation

```bash
# Using uv (faster)
uv venv
source .venv/bin/activate
uv pip install -e ".[dev]"

# Using poetry
poetry install --with dev
```

## Testing
Tests are crucial because this library claims numerical parity with R.

```bash
# Run all tests
pytest tests/

# Run with coverage
pytest tests/ --cov=senspy
```

**Note:** Tests rely on `tests/fixtures/golden_sensr.json`. If you change math logic, you must ensure it still matches these reference values.

## Linting & Formatting
The project uses `ruff` and `black` (configuration in `pyproject.toml`).

```bash
ruff check .
black .
```

## Development Workflow
1.  Create a branch.
2.  Add feature/fix.
3.  **Add/Update Tests**: Every statistical function must have a test case.
4.  Verify against R outputs if adding new statistical methods (optional but recommended).
5.  Open PR.
