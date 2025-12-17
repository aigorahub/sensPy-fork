# Gotchas and Pitfalls

## 1. R Parity Specifics
- **Tolerances**: Floating point differences between R and Python mean exact equality is rare. Tests use relative tolerance (usually `1e-6`).
- **Optimization**: Python's `scipy.optimize` may find slightly different local maxima than R's `optim` for complex models (`dod`, `samediff`).

## 2. Statistical Edge Cases
- **Perfect Scores**: If a subject gets 100% correct, MLE $d'$ is $+\infty$. The code handles this but downstream functions (like plotting) must check for `np.inf`.
- **Chance Performance**: If performance is below guessing, $d'$ is typically clamped to 0.

## 3. Link Functions
- **Approximations**: Some protocols (e.g., `hexad`, `twofive`) use mathematical approximations in `sensR`. `sensPy` replicates these approximations to maintain parity, even if exact combinatorial formulas exist.
- **Double Protocols**: Double protocols (e.g., `double_triangle`) often rely on numerical integration, which is slower than single protocols.

## 4. Parameter Scales
- **Probabilities**: Always [0, 1]. Never percentages [0, 100].
- **d-prime**: Standard normal scale. Typically 0 to 4. Values > 10 usually imply numerical issues or perfect data.

## 5. Input Shapes
- Most functions accept scalar or array inputs (`ArrayLike`). The return type matches the input (scalar $\to$ scalar, array $\to$ array) where possible, but `scipy` functions often return 0-d arrays for scalars.
