# Module Dependencies

## Internal Dependency Graph

### Core Layer (Used by everything)
- `senspy.core.types`: Protocol enums, type aliases.
- `senspy.utils`: Statistical helpers (`delimit`, `normal_pvalue`).
- `senspy.links`: The mathematical foundation.

### Statistical Layer (Depends on Core)
- `senspy.discrim` $\to$ `links`, `core`, `utils`
- `senspy.power` $\to$ `links`, `core`, `utils`
- `senspy.samediff` $\to$ `scipy.optimize`, `scipy.stats` (Self-contained math)
- `senspy.dod` $\to$ `scipy.optimize`

### Presentation Layer (Depends on Statistical)
- `senspy.plotting` $\to$ `roc`, `links`

## Critical Paths
- **`senspy/links/psychometric.py`**: If this breaks, `discrim`, `power`, and `simulation` all break. It defines the relationship between $d'$ and probability for all standard protocols.

## External Libraries
- **Required**: `numpy`, `scipy`.
- **Optional**: `plotly` (plotting), `pandas` (data input), `matplotlib` (legacy plotting support).
