# Deterministic Structured Credit for DeFi

**Akshay Vijayendiran** · Columbia University · [av2777@columbia.edu](mailto:av2777@columbia.edu)

> *Companion code and simulation repository for the working paper:*
> **"Deterministic Structured Credit for DeFi: Designing On-Chain Waterfalls, State Machines, and Duration-Aware Risk"**
> Available at: [SSRN link — forthcoming]

---

## Overview

Static margin frameworks in decentralized lending cannot accommodate amortizing structured credit instruments — mortgage-backed securities, CLO tranches, ABS — whose duration, spread sensitivity, and convexity evolve continuously. When rates rise and prepayments slow, effective duration can nearly double, yet the collateral factor remains fixed. This **Duration Gap** is why structured credit has remained absent from on-chain lending markets despite years of RWA tokenization activity.

This repository contains the Monte Carlo stress simulation and figure generation code underlying the paper's empirical validation. The framework implements **deterministic dynamic margining**: collateral parameters evolve automatically according to rule-based state transitions derived from observable credit risk factors, without discretionary governance intervention.

---

## Repository Structure

```
.
├── README.md
├── SIMULATION.md          # Parameter documentation and methodology
├── simulation/
│   ├── simulation_v034.ipynb   # Main simulation notebook (canonical)
│   ├── param_sweep_v1.ipynb            # 3×3 parameter sweep (σr × ρ)
│   ├── generate_figures.py              # Figure generation script (Figs 6–10)
│   ├── summary.csv                     # v0.3.4 simulation results (1,000 paths)
│   └── sweep_results.csv              # Full parameter sweep results
├── figures/
│   ├── Fig1_execution_pipeline_hires.png
│   ├── Fig3_policy_surface.png
│   ├── Fig10_capital_efficiency_vs_static.png
│   ├── MC_Fig6_min_liquidity.png
│   ├── MC_Fig7_max_daily_liquidations.png
│   ├── MC_Fig8_max_oas_bps.png
│   ├── MC_Fig9_defensive_activation.png
│   └── MC_Fig10_state_evolution.png
└── docs/
    └── CHANGELOG.md                    # Version history
```

---

## Key Results (v0.3.4, 1,000 paths)

| Metric | Value |
|---|---|
| Stress paths (min liquidity < 0.2) | 22.9% |
| Stable paths | 77.1% |
| Median peak NAV drawdown | −4.78% |
| 95th percentile drawdown | −9.69% |
| 99th percentile drawdown | −12.41% |
| Emergency unwind paths (> 0 days) | 0.4% |
| Max emergency days (any path) | 2 |
| Oracle stale gap paths | 16.5% |
| Zero-liquidation paths | 77.1% |

The bimodal liquidation distribution — 77.1% zero, 22.9% full vault — confirms the absence of partial cascade dynamics. All liquidation events resolve within a single clearing interval.

---

## Simulation Model

The simulation models a tokenized MBS vault under correlated rate, spread, liquidity, and oracle shocks over a 252-day horizon.

**Rate process:** Hull-White mean-reverting short rate  
**Spread process:** Correlated mean-reverting OAS  
**Liquidity process:** Endogenous function of OAS widening and liquidation volume  
**Oracle risk:** Bernoulli stale-data injection (p = 0.15 per interval)

The Monte Carlo framework is not intended to produce predictive asset valuations. It illustrates how deterministic policy surfaces respond to plausible market regimes — testing whether the policy engine and waterfall mechanisms contain the resulting structural stress.

See [`SIMULATION.md`](SIMULATION.md) for full parameter documentation.

---

## Quickstart

```bash
# Install dependencies
pip install numpy pandas matplotlib scipy jupyter

# Run the main simulation
jupyter notebook simulation/simulation_v034.ipynb

# Regenerate figures from existing summary.csv
python simulation/generate_figures.py

# Run parameter sweep
jupyter notebook simulation/param_sweep_v1.ipynb
```

---

## Paper Abstract

Traditional asset managers are increasingly tokenizing structured credit portfolios, yet most tokenized instruments remain economically siloed. The constraint is structural: static margin frameworks are poorly suited to amortizing credit assets whose duration, spread exposure, and liquidity evolve continuously. This paper proposes a rule-based margin framework that closes the Duration Gap by functioning as an on-chain analogue to secured funding markets. A structured credit Risk Vector feeds a deterministic Credit State Machine, whose regime classifications drive smooth collateral policy surfaces that adjust margin parameters automatically as structural risk evolves.

---

## Citation

```bibtex
@misc{vijayendiran2026,
  author    = {Vijayendiran, Akshay},
  title     = {Deterministic Structured Credit for {DeFi}: Designing On-Chain
               Waterfalls, State Machines, and Duration-Aware Risk},
  year      = {2026},
  month     = {March},
  note      = {Working Paper. Available at SSRN: [link forthcoming]}
}
```

---

## License

Code: MIT  
Paper and figures: © 2026 Akshay Vijayendiran. All rights reserved.
