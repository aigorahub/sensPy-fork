# Codebase Manifest

## Directory Structure

### `senspy/` (Source Code)
The core library package.
- **`__init__.py`**: Top-level API exports.
- **`core/`**: Infrastructure and base types.
  - `types.py`: Enums (`Protocol`, `Statistic`) and type aliases.
  - `base.py`: Base dataclasses for results (`DiscrimResult`).
- **`links/`**: Psychometric functions connecting $d'$ to proportions.
  - `psychometric.py`: Standard protocols (triangle, 2-AFC, etc.).
  - `double.py`: Double protocols (double triangle, etc.).
- **`utils/`**: Statistical helpers.
  - `stats.py`: P-value calculation, critical values.
  - `transforms.py`: Converters for $P_c \leftrightarrow P_d \leftrightarrow d'$.
- **Model Modules**: Each implements a specific statistical model:
  - `discrim.py`: Core d-prime estimation.
  - `power.py`: Power analysis.
  - `betabin.py`: Beta-binomial models.
  - `samediff.py`: Same-Different protocol.
  - `twoac.py`: 2-AC protocol.
  - `dod.py`: Degree-of-Difference model.
  - `anota.py`: A-Not-A protocol.
  - `roc.py`: ROC and SDT analysis.

### `tests/` (Test Suite)
Comprehensive tests using `pytest`.
- **`fixtures/`**: Static JSON data (`golden_sensr.json`) containing validated outputs from R's `sensR` package.
- **`conftest.py`**: Fixtures for loading golden data and setting tolerances.
- **`test_*.py`**: Unit tests mirroring the module structure.

### `docs/` (Documentation)
MkDocs source files.

## Key Files
- **`pyproject.toml`**: Dependency and build configuration (Poetry).
- **`senspy/links/psychometric.py`**: The mathematical heart of the library; contains the formulas for all protocols.
- **`senspy/discrim.py`**: The primary entry point for most users analysis.
