# Changelog

## v0.3.4 (March 2026) — Canonical

**Parameter recalibration from sweep v1.0**

- `σr`: 1.5% → 1.0% (calibrated against 2022 realized rate volatility; targets 20–25% stress path incidence)
- `ρ`: 0.55 → 0.35 (sensitivity analysis confirmed drawdown distributions insensitive to ρ at σr = 1.0%)

**Results (1,000 paths, seed=42)**
- Stress paths: 22.9%
- Median peak NAV drawdown: −4.78%
- 95th pct drawdown: −9.69%
- 99th pct drawdown: −12.41%
- Emergency paths: 0.4% (4/1000), max 2 days
- Oracle stale paths: 16.5%

**Other changes**
- Notebook docstring updated with full parameter record and results summary
- All figure statistics computed from `summary.csv` (no hardcoded values)
- Fig6 legend repositioned to center whitespace
- Fig8 vertical elongation fixed; annotation repositioned

---

## v0.3.3 (February 2026)

- `σr` = 1.5%, `ρ` = 0.55
- Prior canonical version; superseded by v0.3.4

---

## param_sweep_v1.0 (February 2026)

- 3×3 sweep: σr ∈ {0.8%, 1.0%, 1.5%} × ρ ∈ {0.35, 0.45, 0.55}
- Results in `sweep_results.csv`
- Output informed v0.3.4 parameter selection
