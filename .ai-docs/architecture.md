# System Architecture

## Overview
`sensPy` is a **statistical library** designed as a functional port of the R package `sensR`. It does not maintain global state. It uses a "Result Object" pattern similar to `statsmodels`.

## Data Flow

1.  **Input**: User calls a function (e.g., `discrim(correct=10, total=20, method='triangle')`) with raw counts.
2.  **Validation**: Inputs are checked for logical consistency (e.g., `correct <= total`).
3.  **Link Resolution**: The `method` string is parsed into a `Protocol` enum, which resolves to a `Link` object from `senspy.links`.
4.  **Estimation**: 
    - **Simple cases**: Closed-form math via `senspy.links`.
    - **Complex cases**: Numerical optimization (`scipy.optimize`) using MLE.
5.  **Output**: A frozen Dataclass (e.g., `DiscrimResult`) containing estimates, standard errors, and confidence intervals is returned.

## Key Abstractions

### `Protocol` (Enum)
Defines the sensory test type (Triangle, Duo-Trio, etc.). Holds metadata like `p_guess`.

### `Link` (Dataclass)
Encapsulates the mathematics of a protocol:
- `linkfun`: $P_c \to d'$
- `linkinv`: $d' \to P_c$
- `mu_eta`: Derivative for delta-method SE calculation.

### Result Objects
All statistical functions return rich objects (Dataclasses) that compute secondary metrics (CIs, summaries) lazily or on initialization. They implement `__str__` for R-like console output.

## External Dependencies
- **NumPy/SciPy**: Heavy lifting for math, optimization, and distributions.
- **Plotly**: (Optional) Interactive plotting backend.
- **Pandas**: (Optional) Input data handling in some functions.
