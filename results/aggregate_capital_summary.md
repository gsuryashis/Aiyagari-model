# Equilibrium Results Summary

Results from the Aiyagari model simulation with unemployment insurance.  
All values are from the stationary general equilibrium solved via Brent's method.

## Parameters

| Parameter | Value | Description              |
|-----------|-------|--------------------------|
| β         | 0.96  | Discount factor          |
| δ         | 0.075 | Depreciation rate        |
| α         | 0.33  | Capital share            |
| A         | 1.0   | Total factor productivity|
| θ         | 1e-5  | Utility smoothing term   |

## Equilibrium Outcomes by Tax Rate

| Tax Rate (t) | Unemployment Benefit (b) | Aggregate Capital (K) | Equilibrium r |
|:------------:|:------------------------:|:---------------------:|:-------------:|
| 10%          | (8/3) · 0.10 · w        | 6.06                  | ~0.047        |
| 20%          | (8/3) · 0.20 · w        | 4.44                  | ~0.055        |
| 30%          | (8/3) · 0.30 · w        | 3.02                  | ~0.065        |

## Key Takeaways

- As the tax rate rises, **aggregate capital falls** monotonically.
- Higher taxes reduce take-home wages, weakening the precautionary savings motive.
- Simultaneously, more generous unemployment benefits lower the urgency to self-insure.
- Both channels shift the stationary wealth distribution toward **lower asset levels**.
- The equilibrium interest rate rises as capital becomes scarcer (diminishing returns to capital).

## Stationary Distribution of Employment

From the Markov transition matrix:

| State      | Stationary Probability |
|------------|------------------------|
| Unemployed | 3/11 ≈ 0.273           |
| Employed   | 8/11 ≈ 0.727           |

The unemployment rate in steady state is approximately **27.3%**.

---

*Generated from `notebooks/Aiyagari_Model.ipynb`.*
