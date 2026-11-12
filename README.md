# Tick-Level Regime Backtester & ML Filter (R&D)

Author: Vlad Agapov, PhD (Applied Mathematics, University of Alberta)
Status: Active R&D — dual-state architecture and proprietary regime filter

---

## 📊 Visual Proof of Concept

### 1. The Problem: Static Grids Bleed in Trends

A standard grid-martingale strategy over 11 months of tick data (USDCHF) produces steady profits during ranging markets but suffers catastrophic drawdowns when the market shifts from mean-reverting to trending (e.g., March 2020).

### 2. The Experiment: Can danger regimes be detected before the loss compounds?

We trained a **proprietary regime classifier** on minute-level state data and tested it on a walk-forward out-of-sample block.

**Results (from the confusion matrix):**

| Metric | Value |
|---|---|
| Specificity on healthy minutes | **99.97%** (7 false alarms in 27,408) |
| Precision on danger flags | **100%** (every flag was correct) |
| Recall on danger minutes | **~40%** |

**Interpretation:** The classifier almost never interrupts a healthy trade. When it raises a "danger flag," that flag is always correct. It catches the clearest danger regimes — the remaining danger minutes are structurally interleaved with safe ones, which the execution layer handles.

### 3. The Math: Capped Bets + Reallocation

We frame each stochastic process as a binary outcome: X → 0 (Stop Loss) or X → 2X (Take Profit). By capping losses and reallocating capital, we turn a choppy equity curve into a consistent winner.

**The role of the regime filter:** filter out the X → 0 scenarios before they compound, while leaving X → 2X scenarios intact.

---

## 🛠️ The Dual-State Architecture (Next Step)

We are moving from a static filter to a fully dynamic **Dual-State engine**:

- **State 1 (Low Vol):** mean-reversion grid.
- **State 2 (High Vol):** directional momentum ladder.

The core backtesting engine (tick-accurate, no look-forward bias) is modularized and validated.

---

## 💼 Available for R&D Pilots

I am looking for 1–2 quantitative funds to run a **1-week paid pilot**.

- You provide tick data.
- I calibrate the **proprietary regime classifier** on your data.
- You test the resulting signal in your sandbox.

**What you get:** a regime filter with **high specificity on healthy minutes** and **high precision on danger flags**, tailored to your strategy. You retain full data ownership and IP of the calibration.

### Contact

- GitHub: VladAgapov1969
- LinkedIn: Vladislav Agapov
- Telegram: @agapov_vl
