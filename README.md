# MyWay — Personalized Allocation (prototype)

Clickable prototype of personalizing a CIO strategic asset allocation (SAA) inside the proposal tool's *Allocation Models* screen (SWP/AAP).

**Principle:** risk tolerance decides *how much* risk; personalization decides *how that risk is spent*. Personalized by facts, refined by preferences.

## Inputs
| Input | Source | Mechanism |
|---|---|---|
| Taxes | Client profile (federal bracket, state) | Corp IG ↔ Municipals, 5 notches |
| Alternatives | Client profile (eligibility, liquidity need) | Gate: Full / Reduced by half / None; removed hedge-fund weight spread pro-rata across the rest of the model |
| Geography | Client preference | Large Cap ↔ Developed Markets, 5 notches |
| Income | Client preference | Large Cap → US Equity Income, up to 2 notches |

Profile inputs are prefilled from the client record. The advisor can override them, but must record a reason before the allocation can be applied.

## Math
- Each notch moves 15% of the CIO source sleeve; amounts snap to CIO's 0.5% grid; weights always sum to 100%.
- Geography and Income both draw on Large Cap; each is capped at 30% of the CIO sleeve, so weights never go negative.
- Risk check: estimated volatility and tracking error vs. the CIO model; guardrail at 1.0% tracking error and 0.5% volatility change.
- All 668 valid input combinations across the 8 models were checked: every result sums to 100%, is non-negative and on the 0.5% grid; about 8% exceed the tracking guardrail (max 1.21%) and are flagged for review.

Weights for the three models shown on the production screen come from it. Other models, the sample client records, the US Equity Income sleeve and all risk statistics are illustrative.

Static site: `index.html` only. Deployed on Vercel.
