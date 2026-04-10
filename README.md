# Notebooks

Supplementary Jupyter notebooks for

> *Distributional Stability of Tangent-Linearized Gaussian Inference on Smooth Manifolds.*

Each notebook is self-contained and reproduces a specific set of figures
or claims from the paper. Running a notebook top-to-bottom regenerates
the corresponding PNG/PDF assets into `notebook_figures/`.

## Requirements

- Python 3.9+
- `numpy`, `scipy`, `matplotlib`
- Jupyter (or any environment that can execute `.ipynb`)

All notebooks fix the RNG seed (`SEED = 42`) so results are deterministic.

## Notebooks

### 1. `notebook_circle_benchmark.ipynb` — Circle Benchmark (Marginalization)

Reproduces the **isotropic circle benchmark** of Section III and extends
it with anisotropic-covariance stress tests and mean-offset sweeps.

- Setting: manifold $\mathcal{M}=\{x\in\mathbb{R}^2:\|x\|=R\}$, curvature
  $\kappa=1/R$, reach $\rho=R$; ambient $X\sim\mathcal{N}(\mu,\Sigma)$
  with $\mu=(R+\delta,0)$ and linearization point $\tilde\mu=(R,0)$.
- Operations compared: **exact marginalization** (metric projection
  $Y=R\,X/\|X\|$) vs. **tangent-retraction approximation**.
- Evaluates the $W_2$ bound quantities of **Theorem III.1** specialized
  to the circle.
- Produces Figures 1–4 of the paper (visual demonstration, quantitative
  metrics, phase diagram, generality extension).

### 2. `notebook_conditioning_comparison.ipynb` — Conditioning Comparison

Experimentally verifies the **conditioning comparison** paragraph and
**Theorem IV.1**: tangent-chart conditioning breaks down *before* its
marginalization counterpart, with mode-shift and variance-mismatch
artifacts emerging below the $\sigma/R\approx 1/6$ threshold.

- Exact conditioning via inverse CDF of the surface-measure density
  $p(\theta)\propto\exp\!\bigl(-\tfrac12(x(\theta)-\mu)^\top\Sigma^{-1}
  (x(\theta)-\mu)\bigr)$ on the circle.
- Linearized conditioning on the tangent line followed by retraction.
- Six experiments: density comparison across regimes, break-down
  threshold, mode shift under tangential offset, chart-distortion
  quantities $\eta_r$ and $\|\Omega\|\kappa_\Psi$, density-shape
  artifacts that $W_2$ underestimates, and a detailed view at
  $\sigma/R=0.5$.

### 3. `notebook_planar_pushing.ipynb` — Planar Pushing

Reproduces the **planar pushing** experiment (contact-rich scenario
adapted from Guo et al., ICRA 2025 and Qadri et al., InCOpt, IROS 2022).

- Constrained covariance extraction via tangent-space projection.
- Trajectory-wide locality diagnostics (curvature, reach, spread).
- Directional noise stress test separating normal and tangential
  components.
- Generates the covariance-ellipse scenario visualization, covariance
  and constraint-satisfaction metric figures, enhanced temporal
  diagnostics, and the directional-noise overconfidence figures used
  in the paper.

## Running

From this directory:

```bash
jupyter nbconvert --to notebook --execute notebook_circle_benchmark.ipynb
jupyter nbconvert --to notebook --execute notebook_conditioning_comparison.ipynb
jupyter nbconvert --to notebook --execute notebook_planar_pushing.ipynb
```

or open each notebook in Jupyter/VS Code and run all cells. Output
figures are written to `notebook_figures/`.
