# Technical Specification — FX Receivable Hedge Model

**Created by:** Cameron | **Updated by:** Cameron
**Date Created:** April 3, 2026 | **Date Updated:** April 3, 2026
**Version:** 1.0 | **LLM Used:** Claude (Anthropic, claude-sonnet-4-6)

---

## 1. Problem Statement

Greenfield Solar, a U.S.-based solar equipment importer, holds a €4,500,000 EUR-denominated receivable due April 3, 2027 — exactly one year from today. The firm reports in USD, creating full transaction exposure over the settlement horizon. At the current spot rate of 1.1522 USD/EUR, the receivable carries a USD equivalent of $5,184,900. However, the one-year forward rate is quoted at 1.0875 USD/EUR, implying market-expected EUR depreciation of approximately 5.6% — a $291,150 reduction in proceeds even under a fully hedged forward scenario. Should the EUR depreciate further beyond the forward rate, unhedged USD proceeds would fall below $4,893,750. A 10% depreciation from spot would reduce proceeds to approximately $4,669,860 — a $515,040 shortfall relative to today's spot-equivalent value. This specification documents the hedge model built in Stage 2 and defines an improved version suitable for production use.

---

## 2. Inputs — Known Variables

All inputs are defined as named ranges in the Excel model. Every editable cell is highlighted yellow.

| Named Range  | Description                        | Value     | Unit          | Source                                      |
|------------- |------------------------------------|-----------|---------------|---------------------------------------------|
| `FC_AMT`     | EUR receivable amount              | 4,500,000 | EUR           | Prof. Stauffer Scenario 1                   |
| `S0_in`      | Spot rate at inception             | 1.1522    | USD per EUR   | Yahoo Finance, April 3, 2026                |
| `F0_in`      | 1-year forward rate                | 1.0875    | USD per EUR   | Prof. Stauffer Scenario 1                   |
| `R_USD`      | USD interest rate (domestic)       | 3.625%    | Annual        | Fed Funds midpoint 3.50–3.75%, April 2026   |
| `R_FC`       | EUR interest rate (foreign)        | 2.000%    | Annual        | ECB Deposit Facility Rate, March 2026       |
| `K_PUT`      | Put option strike price            | 1.0875    | USD per EUR   | Assumed ATM; confirm from scenario sheet    |
| `K_CALL`     | Call option strike price           | 1.0875    | USD per EUR   | Assumed ATM; confirm from scenario sheet    |
| `PREM_PUT`   | Put premium per EUR                | 0.015     | USD per EUR   | Prof. Stauffer Scenario 1                   |
| `PREM_CALL`  | Call premium per EUR               | 0.018     | USD per EUR   | Prof. Stauffer Scenario 1                   |
| `T_DAYS`     | Days to settlement                 | 365       | Days          | Maturity: April 3, 2027                     |

---

## 3. Assumptions & Constraints

- **Rate basis:** Annual simple interest applied over T = 1 year (T_DAYS / 365). No continuous compounding or ACT/360 day-count adjustment applied.
- **Covered interest parity:** The forward rate is assumed to satisfy covered interest parity. The money market hedge should produce proceeds approximately equal to the forward hedge; any small deviation is attributable to rounding.
- **Option strikes:** Both K_PUT and K_CALL are assumed at-the-money (ATM) at 1.0875 USD/EUR, matching the forward rate. Actual strikes should be confirmed from the scenario data sheet.
- **Premium timing:** Option premiums are paid upfront at inception. Their future value is computed at R_USD over T to reflect the true opportunity cost at settlement: `FV_premium = PREM × FC_AMT × (1 + R_USD)`.
- **Transaction costs:** Bid-ask spreads, broker fees, and execution slippage are excluded. In practice these would reduce net proceeds across all strategies.
- **Credit capacity:** The money market hedge assumes the firm has access to a EUR-denominated credit facility at R_FC. This has not been confirmed with Treasury.
- **Single exposure:** This model covers one isolated receivable. Portfolio netting, natural hedges, and balance sheet effects are out of scope.
- **No dynamic hedging:** All strategies are static — entered at inception, held to maturity with no rebalancing.

---

## 4. Calculation Flow

### 4.1 Forward Hedge
1. Multiply `FC_AMT` by `F0_in` to compute locked-in USD proceeds.
2. Result is certain and fixed regardless of where S_T settles at maturity.

> `Forward Proceeds = FC_AMT × F0_in`

### 4.2 Money Market Hedge
1. **Borrow:** Compute the present value of the receivable in EUR by discounting at the foreign rate: `PV_EUR = FC_AMT / (1 + R_FC × T_DAYS/365)`.
2. **Convert:** Translate PV_EUR to USD at the current spot rate: `USD_converted = PV_EUR × S0_in`.
3. **Invest:** Grow the USD amount forward at the domestic rate: `MM_Proceeds = USD_converted × (1 + R_USD × T_DAYS/365)`.
4. **Parity check:** Compare MM_Proceeds to Forward Proceeds — difference should be near zero, confirming covered interest parity holds.

### 4.3 Put Option Hedge (Receivable Protection)
1. Compute total upfront premium: `Total_Premium = PREM_PUT × FC_AMT`.
2. Compute future value of premium at R_USD: `FV_Premium = Total_Premium × (1 + R_USD)`.
3. At maturity, determine exercise condition:
   - If `S_T < K_PUT`: exercise the put, sell EUR at K_PUT → `Gross = FC_AMT × K_PUT`.
   - If `S_T ≥ K_PUT`: let put expire, sell EUR at market → `Gross = FC_AMT × S_T`.
4. Net proceeds: `Put_Proceeds = Gross + FV_Premium` (FV_Premium is negative — it reduces proceeds).

### 4.4 Call Option (Reference Only)
A EUR call gives the right to buy EUR — relevant for payables, not receivables. Included for completeness:
1. Compute `FV_Call_Premium = PREM_CALL × FC_AMT × (1 + R_USD)`.
2. Net proceeds at market: `Call_Proceeds = FC_AMT × S_T + FV_Call_Premium`.

---

## 5. Outputs

The Stage 2 model produces the following outputs:

- **Forward Hedge Result:** Single USD value — locked-in proceeds at F0_in. Label: `Locked-In USD Proceeds (Forward)`.
- **Money Market Hedge Result:** Single USD value — FV of converted and invested EUR proceeds. Label: `MM USD Proceeds`.
- **Parity Check:** Difference between MM and Forward results. Should be approximately $0.
- **Option Floor:** Minimum guaranteed USD proceeds under put hedge (when S_T ≤ K_PUT). Label: `Put Option Floor`.
- **Sensitivity Table:** 11-row table varying S_T from 0.95×S₀ to 1.05×S₀ in 1% increments. Columns: S_T, No Hedge, Forward, Money Market, Put Option, Hedge P&L vs No Hedge (×3), Winner vs No Hedge, Winner among Hedges.
- **Scenario Chart:** Line chart plotting USD proceeds for all four strategies (No Hedge, Forward, MM, Put) across the S_T range.
- **Summary Output Table:** Gray-highlighted KPI block comparing all strategies at base S_T = S₀, with Stage 4 recommendation placeholder.

---

## 6. Model Review — What Worked & What to Improve

**What worked correctly:**
- Forward and money market hedge calculations are structurally sound and parity holds within rounding.
- Sensitivity table logic is correct — put option payoff kinks appropriately at K_PUT.
- Named ranges are defined and functional throughout; yellow/green/gray color coding is consistent.
- Winner columns correctly identify the dominant strategy at each spot rate using nested IF logic.

**What should be improved in a production version:**
- **ACT/360 day-count:** Replace the simplified annual basis with `T_DAYS/360` or `T_DAYS/365` depending on the currency convention (EUR typically uses ACT/360 for money markets). This will slightly change MM proceeds and the parity check.
- **K_PUT and K_CALL confirmation:** Both strikes are currently assumed ATM. A production model should pull these from a live options pricer or confirmed scenario input, not an assumption.
- **Call option tab:** The call is shown for completeness but not fully integrated into the sensitivity table. A refined model would include call proceeds as a full column in the sensitivity analysis.
- **Bid-ask spreads:** Add a transaction cost input (e.g., 2–5 pip spread) to make the forward and MM hedge costs more realistic.
- **Scenario labels:** Add explicit "Bear / Base / Bull" row labels in the sensitivity table for cleaner CFO presentation.
- **Dynamic S_T input:** Allow the user to type a single custom S_T and see all strategy payoffs update instantly — useful for ad hoc scenario testing.

---

## 7. Sensitivity Plan

The sensitivity table varies the ending spot rate S_T across 11 steps from 0.95×S₀ to 1.05×S₀ in 1% increments, centered on today's spot of 1.1522 USD/EUR. This produces a range of approximately 1.0946 to 1.2098.

The ±5% range captures realistic short-term EUR/USD volatility — the pair's realized volatility over 1-year horizons has historically averaged 6–9%, so this range represents roughly a 1-standard-deviation window. The chart plots USD proceeds for all strategies simultaneously, making three comparisons immediately visible:

1. **Forward vs No Hedge:** The forward is a flat horizontal line — it outperforms the unhedged position when EUR depreciates and underperforms when EUR appreciates.
2. **MM vs Forward:** Nearly identical lines — confirms parity and validates model accuracy.
3. **Put vs No Hedge:** The put line tracks the unhedged line above K_PUT (upside retained, net of premium) and flattens at the floor below K_PUT (downside protected).

The most analytically useful comparison is **Put vs Forward** — it quantifies the exact cost of retaining upside optionality (the premium) against the certainty of the forward.

---

## 8. Limitations & Next Steps

**Excluded from this model:**
- Dynamic or rolling hedge strategies (e.g., delta hedging, partial hedges)
- Credit risk on the counterparty or the forward contract itself
- Accounting treatment (ASC 815 hedge designation, effectiveness testing)
- Tax implications of hedge gains/losses
- Portfolio-level netting across multiple FX exposures

**How this feeds into Stage 4:**
This specification serves as the primary input to the Stage 4 AI prompt. The named ranges, calculation flow, and improvement notes in sections 2–6 above will be used to construct a structured prompt asking an AI assistant to build or critique a refined version of the model. The explicit output requirements in section 5 ensure the AI produces the exact tables and charts needed for CFO presentation. Any ambiguity left in this spec will propagate directly into the Stage 4 analysis — which is why precision here is non-negotiable.

---

## References

Board of Governors of the Federal Reserve System. (2026, April 3). *H.15 selected interest rates*. https://www.federalreserve.gov/releases/h15/

European Central Bank. (2026). *Key ECB interest rates*. https://www.ecb.europa.eu/stats/policy_and_exchange_rates/key_ecb_interest_rates/html/index.en.html

Hull, J. C. (2022). *Options, futures, and other derivatives* (11th ed.). Pearson.

Madura, J. (2021). *International financial management* (14th ed.). Cengage Learning.

Yahoo Finance. (2026, April 3). *EUR/USD live rate*. https://finance.yahoo.com/quote/EURUSD=X/
