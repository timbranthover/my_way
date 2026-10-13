# MyWay — Personalized Allocation (prototype)

Clickable prototype of a **Personalized** allocation method inside the proposal tool's *Allocation Models* screen (SWP/AAP).

- Starts from a CIO strategic asset allocation (SAA).
- Four client preference questions (Taxes, Inflation, Liquidity, Geography), each with 5 answers; the middle answer = CIO weights.
- Each question moves weight between **one like-for-like pair** of asset classes (Corp IG↔Munis, Government↔TIPS, Securitized↔Hedge Funds, Large Cap↔Developed). No two questions share an asset class, so every combination is independently valid.
- Step = 15% of the source sleeve per notch, snapped to CIO's 0.5% grid. Weights always sum to 100%.
- Risk check: estimated volatility and tracking error vs. the CIO model (illustrative correlation/volatility assumptions), guardrail at 1.0% tracking.

Weights for the three models shown on the production screen are taken from it; other models and all risk statistics are illustrative.

Static site: `index.html` only. Deployed on Vercel.
