# Stage 4 – Final Analysis & Hedge Recommendation

**Created by:** Cameron | **Updated by:** Cameron
**Date Created:** April 3, 2026 | **Date Updated:** April 3, 2026
**Version:** 1.0 | **LLM Used:** Claude (Anthropic, claude-sonnet-4-6)

---

## A. Exposure Summary

Greenfield Solar, a U.S.-based solar equipment importer, holds a **€4,500,000 EUR-denominated receivable** due **April 3, 2027** — one year from today. The firm operates and reports in USD, creating full transaction exposure over the settlement horizon.

At today's spot rate of **1.1522 USD/EUR**, the receivable carries a USD equivalent of **$5,184,900**. However, the one-year forward rate is quoted at **1.0875 USD/EUR**, reflecting a market-implied EUR depreciation of approximately 5.6% — itself driven by the 162.5 basis point interest rate differential between the U.S. (3.625%) and the Eurozone (2.00%). If the euro depreciates further beyond the forward rate, unhedged USD proceeds could fall well below $4,893,750. A 10% depreciation from today's spot would reduce proceeds to approximately $4,669,860 — a $515,040 shortfall relative to today's spot-equivalent value.

The business consequence is direct: Greenfield Solar's USD operating costs, debt service, and shareholder distributions are fixed. Any shortfall in FX proceeds flows straight to the bottom line.

---

## B. Summary of Hedge Outcomes

The following results are drawn from the Stage 2 Excel model at base scenario (S_T = S₀ = 1.1522):

| Strategy | USD Proceeds | vs. Spot Unhedged | Key Trade-Off |
|---|---|---|---|
| No Hedge (at S₀) | $5,184,900 | — | Full upside and full downside; zero cost |
| Forward Contract | $4,893,750 | −$291,150 | Complete certainty; no upside participation |
| Money Market Hedge | ~$4,893,750 | −$291,150 | Synthetic forward; operationally complex |
| Put Option (floor) | ~$4,826,138 | −$358,762 | Downside protected; upside retained; premium cost |
| Call Option | Not applicable | — | Relevant for payables, not receivables |

**Forward Hedge:** Locks in $4,893,750 with zero uncertainty. The cost is the $291,150 opportunity loss relative to today's spot — but that gap largely reflects the interest rate differential already priced into the forward, not a true economic loss. For a firm that needs budget certainty, this is the cleanest outcome.

**Money Market Hedge:** Produces virtually identical proceeds to the forward (~$4,893,750), confirming covered interest parity. However, it requires borrowing €4,411,765 at the ECB rate, converting at spot, and investing USD — a three-step operational process that consumes credit capacity and introduces execution risk. The economic outcome is equivalent to the forward; the operational complexity is not.

**Put Option:** Establishes a USD floor of approximately $4,826,138 (after FV of $67,500 premium compounded at R_USD) while preserving full upside if EUR appreciates above K_PUT = 1.0875. If the euro strengthens to 1.20, unhedged proceeds jump to $5,400,000 — the put holder captures that gain while the forward holder does not. The premium is the price of that optionality.

**Call Option:** A EUR call gives the right to buy EUR — structurally a payable hedge. It is not the primary instrument for a receivable scenario and is included for completeness only.

**No Hedge:** At S_T = S₀, proceeds are $5,184,900 — the highest base-case outcome. But this is also the riskiest position. EUR/USD has moved more than 10% in a single year multiple times in the past decade. An unhedged receivable is a directional bet on EUR strength, not a treasury strategy.

---

## C. Sensitivity Interpretation

The Stage 2 sensitivity table spans S_T from **1.0946 (−5%)** to **1.2098 (+5%)** in 1% increments around today's spot.

**EUR depreciation scenarios (S_T < 1.1522):**
The forward and money market hedges outperform both the unhedged position and the put option at every depreciation scenario. At S_T = 1.0946 (−5%), the unhedged position yields $4,925,700 — below the forward's locked-in $4,893,750 only marginally, but the gap widens sharply beyond −5%. The put option underperforms the forward in all depreciation scenarios because the premium cost reduces net proceeds even when the put is exercised at the floor. The forward is the clear winner when EUR weakens.

**EUR appreciation scenarios (S_T > 1.1522):**
The no-hedge position and the put option both outperform the forward when EUR strengthens. At S_T = 1.2098 (+5%), unhedged proceeds reach $5,444,100 versus the forward's fixed $4,893,750 — a $550,350 opportunity cost of having hedged. The put option at this level yields approximately $5,376,600 (market conversion minus FV premium), capturing most of the upside while still having been protected on the downside. This asymmetry — limited downside, meaningful upside — is the defining feature of the put.

**Key strategic insight:** The forward dominates in bear scenarios; the put dominates when there is genuine two-way uncertainty; the no-hedge position is only rational if management has a strong directional view that EUR will appreciate. In the current macro environment — with the Fed holding rates meaningfully above the ECB — the structural bias favors USD strength, making an unhedged position difficult to justify.

---

## D. Strategic Recommendation

**Recommended strategy: Forward Contract**

The forward contract is the recommended hedge for this receivable. It locks in **$4,893,750** with complete certainty, requires no upfront premium, and eliminates all downside exposure over the one-year horizon.

The rationale is threefold. First, the current macro environment structurally favors EUR depreciation — the 162.5 bps USD/EUR rate differential is already embedded in the forward rate, and additional Fed/ECB policy divergence could push EUR lower still. Hedging with a forward protects against the most likely directional outcome. Second, Greenfield Solar is an importer with USD-denominated operating costs — cash flow predictability has direct operational value. A $291,150 reduction in spot-equivalent value is the known cost of certainty, not an unexpected loss. Third, the money market hedge produces an equivalent economic outcome but introduces unnecessary operational complexity and consumes credit capacity that may be better deployed elsewhere.

The put option is a reasonable alternative if management believes EUR appreciation is likely or wishes to retain upside participation — but the $67,500 upfront premium (FV ~$69,944) represents a real cost that reduces the floor to ~$4,826,138, approximately $67,612 below the forward outcome. For a firm prioritizing budget certainty over optionality, this premium is not justified by the current risk profile.

---

## E. Executive Justification

**Cash flow stability:** The forward contract converts a variable EUR receivable into a fixed USD cash inflow of $4,893,750 on April 3, 2027. This number can be booked into the operating budget today with no revision required regardless of market movement.

**Budget certainty:** Greenfield Solar's procurement, payroll, and debt service are denominated in USD. Locking in the receivable value eliminates the risk of a budget shortfall driven by FX rather than operating performance — keeping FX out of the variance conversation with the CFO.

**Liquidity impact:** The forward requires no upfront cash outlay. Unlike the put option ($67,500 premium) or the money market hedge (requires a EUR credit facility), the forward preserves working capital and leaves existing credit lines undrawn.

**Optionality value:** The put option's upside retention is theoretically attractive but practically limited in the current environment. With the forward rate already pricing in 5.6% EUR depreciation, the probability of EUR appreciating enough to make the put's upside worth $69,944 in premium is low under consensus forecasts. Paying for optionality in a market with a clear directional bias is a below-average expected value trade.

**Accounting implications (optional):** If designated as a cash flow hedge under ASC 815, the forward contract qualifies for hedge accounting treatment — gains and losses flow through OCI rather than P&L until settlement, smoothing earnings volatility. This is an additional argument in favor of the forward for a public or audit-sensitive entity.

---

## F. Structured AI Prompt

The following prompt is designed to instruct an AI assistant to fully reconstruct the Stage 2 FX hedge Excel model from written instructions alone.

---

```
# GOAL
Build a professional Excel workbook modeling three FX hedging strategies
for a USD-reporting firm with a EUR-denominated receivable. The model must
be auditable, color-coded, and suitable for CFO presentation.

# SCENARIO
Firm: Greenfield Solar (U.S.-based solar equipment importer)
Exposure: EUR receivable, due in 1 year
Context: Full transaction exposure — firm reports in USD

# INPUT VARIABLES
Use the following named ranges for all editable inputs.
Highlight all input cells in YELLOW.

  FC_AMT     = 4,500,000      (EUR receivable amount)
  S0_in      = 1.1522         (USD/EUR spot rate at inception)
  F0_in      = 1.0875         (USD/EUR 1-year forward rate)
  R_USD      = 0.03625        (U.S. annual interest rate, simple)
  R_FC       = 0.02000        (EUR annual interest rate, simple)
  K_PUT      = 1.0875         (EUR put strike, USD/EUR)
  K_CALL     = 1.0875         (EUR call strike, USD/EUR)
  PREM_PUT   = 0.015          (put premium per EUR, USD)
  PREM_CALL  = 0.018          (call premium per EUR, USD)
  T_DAYS     = 365            (days to settlement)

# COLOR CODING CONVENTION
  Yellow  = Editable inputs
  Blue    = Assumptions / notes
  Green   = Intermediate formula calculations
  Gray    = Final outputs and summary KPIs

# MODEL LOGIC

## Sheet 1: FX Hedge Model

### Section 1 — Inputs
- List all named ranges above with labels, values, units, and data sources
- All cells editable (yellow); use named ranges throughout — no hardcoded values

### Section 2 — Forward Hedge
- Locked-in USD proceeds = FC_AMT × F0_in
- Label result clearly; mark as gray output
- Note: proceeds are fixed regardless of S_T at maturity

### Section 3 — Money Market Hedge (3 steps, show each explicitly)
- Step 1 (Borrow): PV_EUR = FC_AMT / (1 + R_FC × T_DAYS/365)
- Step 2 (Convert): USD_converted = PV_EUR × S0_in
- Step 3 (Invest): MM_Proceeds = USD_converted × (1 + R_USD × T_DAYS/365)
- Add parity check row: MM_Proceeds − Forward_Proceeds ≈ $0

### Section 4 — Option Hedges
- Put premium total (USD) = PREM_PUT × FC_AMT  [negative — cash outflow]
- FV of put premium = Put_Premium_Total × (1 + R_USD)
- Put proceeds at maturity:
    If S_T < K_PUT: Gross = FC_AMT × K_PUT  (exercise)
    If S_T ≥ K_PUT: Gross = FC_AMT × S_T   (let expire)
    Net = Gross + FV_Put_Premium  (FV premium is negative)
- Call premium total (USD) = PREM_CALL × FC_AMT  [reference only]
- FV of call premium = Call_Premium_Total × (1 + R_USD)
- Call proceeds = FC_AMT × S_T + FV_Call_Premium

### Section 5 — Sensitivity Table
- Vary S_T from 0.95 × S0_in to 1.05 × S0_in in 11 steps of 1%
- Columns:
    Col A: S_T (USD/EUR)
    Col B: No Hedge = FC_AMT × S_T
    Col C: Forward = FC_AMT × F0_in  (constant)
    Col D: Money Market = MM_Proceeds  (constant, from Section 3)
    Col E: Put Option = IF(S_T < K_PUT, FC_AMT×K_PUT, FC_AMT×S_T) + FV_Put_Premium
    Col F: Hedge P&L vs No Hedge (Forward): Col C − Col B
    Col G: Hedge P&L vs No Hedge (MM): Col D − Col B
    Col H: Hedge P&L vs No Hedge (Put): Col E − Col B
    Col I: Winner vs No Hedge (nested IF picking max of B,C,D,E)
    Col J: Winner among Hedges Only (nested IF picking max of C,D,E)
- Highlight base row (S_T = S0_in) in gold
- Add line chart: USD Proceeds (y-axis) vs S_T (x-axis), all 4 strategies

### Section 6 — Summary Output (gray cells)
- No Hedge at S0: FC_AMT × S0_in
- Forward Hedge: FC_AMT × F0_in
- Money Market Hedge: MM_Proceeds
- Put Option Floor: FC_AMT × K_PUT + FV_Put_Premium
- Placeholder row: "Hedge Recommendation — To be completed in Stage 4"

## Sheet 2: Notes & Assumptions
Include the following:
- Rate basis: annual simple interest, T = T_DAYS/365
- Option strikes assumed ATM at 1.0875; confirm from scenario data
- FV of premium convention: premium × FC_AMT × (1 + R_USD)
- Transaction costs excluded (bid-ask spreads, broker fees)
- Money market hedge assumes available EUR credit facility
- Single isolated receivable — no portfolio netting

# VERIFICATION CHECKS
- Forward Proceeds and MM Proceeds should differ by less than $100 (parity)
- Put proceeds should equal floor value when S_T ≤ K_PUT and track market when S_T > K_PUT
- No hardcoded values anywhere in formula cells — all must reference named ranges
- All input cells yellow; all output cells gray

# EXPORT
- File name: cameron-stage2-model.xlsx
- Tabs: "FX Hedge Model" and "Notes & Assumptions"
- Professional formatting: consistent font (Arial 10pt), column widths, frozen header rows
```

---

## Extra Credit: Areas for Further Study

### 1. AI Skills & Automation

The workflow used across Stages 1–4 of this project represents a primitive version of what modern AI-augmented treasury teams are beginning to deploy at scale. At the individual stage level, Claude assisted with memo drafting, formula logic, and spec writing — tasks that took minutes rather than hours. The next frontier is closing the loop entirely: an AI system that pulls live EUR/USD spot and forward rates from a market data API (Bloomberg, Refinitiv, or FRED), populates the named input cells automatically, reruns the sensitivity analysis, and flags when hedge proceeds fall outside a pre-set threshold. Monte Carlo simulation — running 10,000 random S_T draws from a calibrated volatility distribution rather than a fixed ±5% range — would replace the deterministic sensitivity table with a probability-weighted outcome distribution. A treasury analyst could then present not just "the forward locks in $4,893,750" but "the forward eliminates 94% of downside tail risk at the 95th percentile." Claude Code or a Python-based Claude integration could automate this entire pipeline on a scheduled basis with no manual intervention.

### 2. GitHub & Version Control

The GitHub-based structure of this project — committing specs, models, and memos as versioned files — is directly analogous to how production financial models are governed at Big 4 firms and investment banks. Every commit represents a timestamped, auditable record of what was built, when, and why. If a regulator, auditor, or senior manager asks "what assumptions drove the hedge recommendation in Q2 2026?", the answer is a single git log command away. Stages 1 through 3 of this project demonstrate the full audit trail: the Stage 1 memo documents the business rationale, the Stage 2 model contains the calculations, and the Stage 3 spec provides the reconstruction blueprint. In a production hedge accounting context under ASC 815, this version-controlled documentation chain could serve directly as hedge effectiveness documentation — reducing audit preparation time and eliminating the risk of after-the-fact rationalization. An AI assistant with access to the full repository history could also flag inconsistencies between stages automatically, functioning as a continuous model governance layer.


### 3. Multi-File Reasoning

One of the most underappreciated capabilities of modern AI systems is the ability to reason across multiple documents simultaneously — treating a repository not as a collection of isolated files but as an interconnected knowledge graph. In the context of this project, an AI with access to all four stage deliverables could automatically cross-check consistency: verifying that the spot rate in the Stage 1 memo matches the S0_in input in the Stage 2 model, that the named ranges in the Stage 3 spec align with the actual named ranges defined in the Excel file, and that the recommendation in Stage 4 is numerically supported by the sensitivity table in Stage 2. Any drift between stages — the kind that accumulates naturally when a model is revised after a spec is written — would be flagged automatically. Beyond consistency checking, multi-file reasoning enables automated dashboard generation: an AI could read the Stage 3 spec as a blueprint, pull live market data, repopulate the Stage 2 model inputs, rerun the sensitivity analysis, and produce an updated Stage 4 recommendation memo — all without human intervention. This is exactly the kind of analyst-to-automation pipeline that treasury teams at large corporates are beginning to build using tools like Claude, GPT-4, and Python-based orchestration frameworks. The GitHub repository structure used in this project — with standardized file names, consistent named ranges, and a spec detailed enough for reconstruction — is the prerequisite infrastructure that makes this level of automation possible.

### 4. Accounting & Audit Integration

Hedge accounting under ASC 815 (U.S. GAAP) introduces documentation and effectiveness requirements that significantly raise the bar for financial model governance. To qualify for cash flow hedge accounting — which allows gains and losses on the hedging instrument to flow through Other Comprehensive Income (OCI) rather than directly through P&L — a firm must formally designate the hedge relationship at inception, document the risk management objective and strategy, and demonstrate ongoing hedge effectiveness throughout the life of the instrument. The forward contract recommended in Stage D of this analysis would qualify for cash flow hedge accounting if properly designated, smoothing reported earnings by deferring FX gains and losses in OCI until the hedged transaction (the receivable settlement) affects earnings. The GitHub-based documentation structure of this project maps directly onto these requirements. The Stage 1 memo serves as the hedge designation document — capturing the risk management objective and the nature of the exposure at inception. The Stage 2 model provides the quantitative effectiveness assessment, demonstrating that the forward rate closely approximates the hedged rate. The Stage 3 spec functions as the methodology documentation an auditor would request to verify that the model is reproducible and free of post-hoc adjustment. The version-controlled commit history provides an immutable timestamp for each document — critical for demonstrating that designation occurred before, not after, the hedged transaction. In a Big 4 audit context, a client who can produce a Git repository with timestamped hedge documentation, a reproducible quantitative model, and a written spec detailed enough for independent reconstruction has effectively pre-answered the auditor's most common hedge accounting questions before the engagement begins.
