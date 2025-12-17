# Coding Conventions

## Naming
- **Functions/Variables**: `snake_case` (e.g., `discrim_power`, `d_prime`).
- **Classes**: `CamelCase` (e.g., `DiscrimResult`).
- **Mathematical Variables**: Keep distinct from R but recognizable.
  - $d'$ $\to$ `d_prime` (not `d.prime`).
  - $P_c$ $\to$ `pc`.
  - $P_d$ $\to$ `pd`.

## Type Hinting
- Strict typing is enforced.
- Use `ArrayLike` for inputs that can be scalars or lists.
- Use `NDArray` for internal array processing.

## Docstrings
- **Style**: NumPy style.
- **Content**: Must include `Parameters`, `Returns`, and `Examples`.
- **References**: Cite the corresponding `sensR` function if applicable (e.g., "Corresponds to `discrim()` in sensR").

## Error Handling
- Raise `ValueError` for invalid statistical inputs (e.g., negative counts, probabilities > 1).
- Handle edge cases (e.g., perfect scores) gracefully, often returning `np.inf` for $d'$ or specific boundary codes.

## Testing Pattern
Tests check against `tests/fixtures/golden_sensr.json`. Do not hardcode magic numbers in tests; load them from the fixture to ensure parity with R.
