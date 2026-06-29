# Real Options Valuation of Pharmaceutical R&D Using Black-Scholes

A framework for valuing the decision to continue or abandon a drug candidate at a clinical trial milestone as a financial option, rather than as a single static net-present-value calculation. Standard NPV penalizes early-stage R&D for its uncertainty. Real options valuation, on the other hand, treats that uncertainty as a source of value, the same way a call option becomes more valuable, not less, as volatility rises.

## Motivation

Pharma R&D investment decisions are staged: a company (or investor) commits capital at each trial phase with the right, but not the obligation, to keep funding the next phase if results justify it. That is structurally identical to a call option. This notebook adapts the Black-Scholes options pricing model to quantify the value of that staged decision right, giving a more realistic valuation for high-uncertainty, milestone-gated investments than a traditional discounted cash flow model.

## Mathematics and Methodology:
The five standard Black-Scholes inputs are re-mapped to the pharma R&D context:

| Black-Scholes Parameter | Pharma R&D Equivalent |
|---|---|
| **S** — spot price | Present value of projected cash flows from a successful drug launch |
| **K** — strike price | Capital required to fund the next phase of development |
| **T** — time to maturity | Time remaining until the next trial milestone / patent-exclusivity window |
| **r** — risk-free rate | Cost of capital / discount rate |
| **σ (sigma)** — volatility | Uncertainty in clinical and commercial success, estimated from comparable public biotech stocks |

Volatility is not assumed. It's estimated by pulling historical price data for comparable biotech names (VRTX, BIIB, INCY) and using their realized volatility as a sector-specific proxy, yielding σ ≈ 32.5%.

## Key Results:

Using these inputs, the baseline model returns:
- Real Option Value: ≈ $297.1M
- d1: 2.05
- Implied probability of reaching commercial viability (N(d2)): ≈ 92.6%
- Delta: 0.98 

## Languages and Packages Used for this Project:
- Python (NumPy, SciPy - norm.cdf, Matplotlib)
- Jupyter
- A market-data API for historical volatility

## Limitations & Future Work
- Volatility is proxied from comparable public biotech equities, which captures market-wide sentiment but not asset-specific clinical risk (e.g., trial design, indication, mechanism novelty).
    1. A next step would be blending this with phase-specific historical success-rate data.
- The current model values a single decision gate. Extending it to a compound/sequential option would better reflect how staged R&D investment actually unfolds.
- Adding a sensitivity sweep over σ and T directly in the notebook would make the "which assumption matters most" analysis self-contained.
