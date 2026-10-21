# MyWay — Personalized Allocation (prototype)

Clickable prototype of personalizing a CIO strategic asset allocation (SAA) inside the proposal tool's *Allocation Models* screen (SWP/AAP).

**Principle:** risk tolerance decides *how much* risk; personalization decides *how that risk is spent*. Personalized by facts, refined by preferences.

## Inputs
| Input | Source | Mechanism |
|---|---|---|
| Taxes | Client profile (federal bracket, state) | Corp IG ↔ Municipals, 5 notches |
| Alternatives | Client profile (net worth → eligibility) | Gate: Full (qualified purchaser) / Reduced by half (accredited) / None (not accredited); removed hedge-fund weight spread pro-rata across the rest of the model |
| Geography | Client preference | Large Cap ↔ Developed Markets, 5 notches |
| Income | Client preference | Large Cap → US Equity Income, up to 2 notches |

The screen is always opened for a specific client, so profile inputs are prefilled from that client's facts on file. The advisor can adjust them; a marker shows the profile setting, and What changed tags the input as Adjusted.

## Controls only show what is possible
- Two-way input: CIO in the center, 5 notches.
- One-way input (the model holds none of what one direction would sell): CIO sits at that end, labeled with why (e.g. "CIO · no munis held", "CIO · total return"), 3 notches toward the possible side.
- Impossible input: collapses to one line ("No stocks in this model", "No alternatives in this model").
- Profile inputs show a Profile chip; once moved, an Adjusted chip and a ring marking the profile setting. Options the client is not eligible for are locked.

## Math
- Each notch moves 15% of the CIO source sleeve; amounts snap to CIO's 0.5% grid; weights always sum to 100%.
- Geography and Income both draw on Large Cap; each is capped at 30% of the CIO sleeve, so weights never go negative.
- Risk check: estimated volatility and tracking error vs. the CIO model; guardrail at 1.0% tracking error and 0.5% volatility change.
- All 668 valid input combinations across the 8 models were checked: every result sums to 100%, is non-negative and on the 0.5% grid; about 8% exceed the tracking guardrail (max 1.21%) and are flagged for review.

Weights for the three models shown on the production screen come from it. Other models, the client's facts (37% bracket, New York, $3.4M net worth), the eligibility thresholds, the US Equity Income sleeve and all risk statistics are illustrative.

Static site: `index.html` only. Deployed on Vercel.

## Guided demo
"Guided demo" (top right) runs an 8-step walkthrough over the app: today's screen → Personalize → profile-set tilts → base vs. personalized → a client preference → a one-way input → What changed and the risk check → a 100% bond model. Each step sets the app to a known state, so Back/Next are always consistent. Keys: ← → to step, Esc to exit. Open with `#demo` to start it automatically.

## Branding
The feature is branded **MyWay**: the screen's own typeface, bold, in one brand green (#0E7A57; #46C79A on dark surfaces). A small "tuned line" symbol follows the word (three lines, the middle one adjusted with a dot: the sliders, distilled). No badge or brackets. It appears on the Personalize button, the personalization screen title, the personalized tile's tag, the Apply confirmation and the demo's closing card. The CIO base tile, What changed and the sliders stay unbranded so they read as CIO governance.

## Proposal PDF
While personalizing, **Proposal PDF** (footer) opens a preview of a 3-page US Letter proposal: (1) CIO model vs. MyWay allocation with a full asset-class table, (2) why the allocation differs, risk check and next steps, (3) important information. **Download PDF** uses the browser's print engine, so text stays vector and crisp; choose "Save as PDF" as the destination. No performance (past, projected or hypothetical) is shown, which keeps the document clear of SEC Marketing Rule hypothetical-performance conditions; risk estimates carry methodology and limitation language in the spirit of FINRA Rule 2214. All disclosures are sample placeholders; final language must come from Compliance. Every page is marked "Sample".
