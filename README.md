# Aiyagari Model with Unemployment Insurance

> **Course Project · Macroeconomics: Incomplete Markets**  
> Suryashis Ghosh  & Sneha Thankkam Raju · May 2025

A computational implementation of the Aiyagari (1994) incomplete-markets model, extended to include unemployment insurance financed by a proportional wage tax. We solve for the stationary general equilibrium and study how the tax rate affects capital accumulation and the wealth distribution.

---

## Overview

In this model:
- A **unit mass of heterogeneous agents** face idiosyncratic employment risk
- Employment follows a **two-state Markov process** (employed / unemployed)
- Agents can only self-insure by **saving in a single risk-free asset** (no borrowing below a floor)
- The **government runs a balanced budget**: it taxes employed workers' wages and redistributes as unemployment benefits
- **Competitive firms** determine the interest rate `r` and wage `w` via a Cobb-Douglas production function

We solve for equilibrium at three tax rates — **10%, 20%, 30%** — and compare the resulting capital distributions and aggregate capital levels.

---

## Key Results

| Tax Rate | Aggregate Capital K | Equilibrium r |
|----------|-------------------|---------------|
| 10%      | 6.06              | ~0.047        |
| 20%      | 4.44              | ~0.055        |
| 30%      | 3.02              | ~0.065        |

Higher taxes reduce after-tax wages and precautionary savings motives, shifting the wealth distribution toward lower capital holdings.

---

## Repository Structure

```
aiyagari-incomplete-markets/
│
├── README.md                         # This file
│
├── notebooks/
│   └── Aiyagari_Model.ipynb          # Main simulation notebook (all code)
│
├── docs/
│   └── Macro_Incomplete_markets.pdf  # Written report with derivations
│
├── figures/
│   └── capital_distribution.png      # Capital distribution plot (t=10,20,30%)
│
└── results/
    └── aggregate_capital_summary.md  # Tabulated equilibrium results
```

---

## Model Summary

### 1. Employment Markov Process

The transition matrix for employment status is:

```
         Unemployed(t+1)   Employed(t+1)
Unemployed(t)    0.2            0.8
Employed(t)      0.3            0.7
```

The stationary distribution is: **π_U = 3/11**, **π_E = 8/11**.

### 2. Unemployment Benefit

From the government's balanced budget constraint:

```
b = (8/3) · t · w
```

where `t` is the tax rate and `w` is the equilibrium wage.

### 3. Agent's Value Function

The Bellman equation for an agent with assets `k` and employment state `s ∈ {0,1}`:

```
v(k, s) = max_{k'} { ln[ rk + ws + (8t/3)w·(1-s) - k' + (1-δ)k + θ ]
                     + β · Σ_{s'} P_{ss'} · v(k', s') }
```

Parameters: `β = 0.96`, `δ = 0.075`, `α = 0.33`, `θ = 1e-5` (utility smoothing), `A = 1.0` (TFP).

### 4. Equilibrium

The equilibrium interest rate `r*` is found by iterating until the capital market clears:

```
K(r*, t) = K_supply   ←→   r* = A·α·K^(α-1)
```

Solved numerically using Brent's method (`scipy.optimize.root_scalar`).

---

## Setup & Usage

### Requirements

```bash
pip install numpy matplotlib numba scipy quantecon
```

### Running the Model

Open and run the notebook:

```bash
jupyter notebook notebooks/Aiyagari_Model.ipynb
```

The notebook will:
1. Solve the household's dynamic programming problem (policy iteration via `quantecon.markov.DiscreteDP`)
2. Iterate to find the general equilibrium `r*` for each tax rate
3. Plot the stationary capital distribution
4. Print aggregate capital and equilibrium interest rates

---

## References

- Aiyagari, S. R. (1994). *Uninsured Idiosyncratic Risk and Aggregate Saving*. Quarterly Journal of Economics, 109(3), 659–684.
- QuantEcon lectures: [https://quantecon.org](https://quantecon.org)
