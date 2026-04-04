# FX Receivable Exposure — EUR Hedge Strategy Memo

**Created by:** Cameron | **Updated by:** Cameron
**Date Created:** April 3, 2026 | **Date Updated:** April 3, 2026
**Version:** 1.0 | **LLM Used:** Claude (Anthropic, claude-sonnet-4-6)

---

## Executive Summary

Greenfield Solar, a U.S.-based solar equipment importer, expects to receive **€4,500,000** from a European supplier in approximately one year (maturity: April 3, 2027). At today's spot rate of **1.1522 USD/EUR**, this receivable carries a USD equivalent of roughly **$5,184,900**. However, the one-year forward rate has been quoted at **1.0875**, implying that markets already expect the euro to weaken — translating to a forward-locked value of **$4,893,750**, a $291,150 reduction from today's spot value. Further EUR depreciation beyond the forward rate would erode proceeds even more. This memo outlines the exposure, articulates the downside risk, introduces three hedging strategies, and maps the analytical work to be completed in Stages 2 through 4.

---

## Background & Objectives

Foreign exchange receivables expose U.S. firms to translation risk: when payment is denominated in a foreign currency, any depreciation of that currency before settlement directly reduces dollar-equivalent proceeds. Greenfield Solar's €4,500,000 receivable is fixed in euros, meaning the company bears full EUR/USD exchange rate risk over the next twelve months.

The current macro environment amplifies this concern. EUR/USD has traded between **1.0805 and 1.2079** over the past 52 weeks — a range of over 1,200 pips. The Federal Reserve is holding its target rate at **3.50–3.75%**, while the ECB's deposit facility rate sits at **2.00%**, creating a meaningful interest rate differential that structurally favors the dollar. In covered interest rate parity terms, this differential is already embedded in the forward rate of 1.0875, which sits well below the current spot of 1.1522. Should the euro weaken further than the forward implies — a plausible outcome given ongoing Middle East geopolitical uncertainty and elevated U.S. inflation — unhedged USD proceeds could fall materially below $4,893,750.

**Primary Objective:** Identify and evaluate hedging strategies that protect USD proceeds from the €4,500,000 receivable maturing April 3, 2027.

**Secondary Objectives:**
- Quantify the cost and payoff profile of each hedge under bear, base, and bull EUR/USD scenarios
- Establish a replicable framework for managing future FX receivable exposure
- Deliver a CFO-ready recommendation supported by a working financial model

---

## Methods

This analysis is structured across four stages:

**Stage 1 — Executive Memo (current):** Frame the exposure, quantify the risk, and introduce hedge candidates at a strategic level.

**Stage 2 — Excel Model:** Build a working `.xlsx` prototype computing net USD proceeds for each hedge strategy across three rate scenarios — bear (EUR depreciates to ~1.03), base (rate holds near forward at 1.0875), and bull (EUR appreciates to ~1.22). Model outputs will include a payoff comparison table and scenario summary chart.

**Stage 3 — Technical Specification:** Document model logic, assumptions, data sources, and formula structure. Design an improved production version precise enough for reconstruction by another analyst or AI assistant.

**Stage 4 — Final Analysis & Recommendation:** Select the preferred hedge using model results, document AI interactions in a prompt log, and present a structured recommendation to the CFO.

**Hedge Strategies Under Consideration:**

| Strategy | Mechanism | Pro | Con |
|---|---|---|---|
| **Forward Contract** | Lock in 1.0875 USD/EUR today for delivery in 1 year | Full USD certainty; no premium cost | No upside if EUR strengthens; obligatory settlement |
| **EUR Put Option** | Buy the right to sell €4.5M at strike k; premium = $0.015/EUR ($67,500 total) | Downside protected; upside retained if EUR rises | Upfront premium paid regardless of outcome |
| **Money Market Hedge** | Borrow PV of €4.5M today at EUR rate (2.00%), convert to USD at spot (1.1522), invest at USD rate (3.625%); repay loan with receivable | Synthetic forward using cash markets; no derivatives | Requires credit capacity; operationally more complex |

**Market Inputs (as of April 3, 2026):**

| Input | Value | Source |
|---|---|---|
| EUR/USD Spot | 1.1522 | Yahoo Finance |
| 1-Year Forward Rate | 1.0875 | Scenario given |
| USD Interest Rate | 3.625% | Fed Funds midpoint (3.50–3.75% target) |
| EUR Interest Rate | 2.00% | ECB Deposit Facility Rate |
| EUR Put Premium | $0.015/EUR | Scenario given |
| EUR Call Premium | $0.018/EUR | Scenario given |

---

## Limitations & Next Steps

**Limitations:**
- Forward and option rates are indicative; actual executable quotes may differ at time of hedging
- The money market hedge assumes Greenfield Solar has available EUR-denominated credit capacity, which has not been confirmed
- Rate scenarios in Stage 2 are illustrative; realized EUR/USD volatility may exceed modeled bounds
- This analysis covers a single isolated receivable; portfolio netting and natural hedges are outside scope
- Option strike price (k) is pending confirmation from the scenario data sheet — assumed at-the-money (1.0875) for now

**Next Steps:**

| Action | Owner | Target |
|---|---|---|
| Confirm option strike price (k) from scenario inputs | Cameron | Immediately |
| Build Stage 2 Excel payoff model across 3 scenarios | Cameron | TBD |
| Obtain updated indicative forward and option quotes | Treasury | TBD |
| Complete Stage 3 technical specification | Cameron | TBD |
| Present Stage 4 CFO recommendation | Cameron | TBD |

---

## References

Board of Governors of the Federal Reserve System. (2026, April 3). *H.15 selected interest rates*. https://www.federalreserve.gov/releases/h15/

European Central Bank. (2026, February 5). *Monetary policy decisions*. https://www.ecb.europa.eu/press/pr/date/2026/html/ecb.mp260205~001d26959b.en.html

Hull, J. C. (2022). *Options, futures, and other derivatives* (11th ed.). Pearson.

Madura, J. (2021). *International financial management* (14th ed.). Cengage Learning.

Yahoo Finance. (2026, April 3). *EUR/USD (EURUSD=X) live rate*. https://finance.yahoo.com/quote/EURUSD=X/
