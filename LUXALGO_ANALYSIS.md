# LuxAlgo Analysis

> **Purpose**
>
> This document serves as the reverse-engineering notebook for the LuxAlgo Smart Money Concepts indicator.
>
> The goal is **not** to copy the implementation, but to understand its behaviour, architecture, algorithms, and design decisions so that we can build an independent clean-room implementation.
>
> Every observation should be classified as one of the following:
>
> - ✅ Confirmed
> - 🟡 Hypothesis
> - ❓Question
> - 🧪 Experiment
>
> Only confirmed observations should influence the implementation.

---

# Project Goal

Recreate the behaviour of the LuxAlgo Smart Money Concepts indicator while developing an original, maintainable, modular implementation.

Success is measured by behavioural parity rather than identical source code.

---

# High-Level Architecture

Current understanding of the indicator:

```
LuxAlgo Smart Money Concepts

                Inputs
                   │
                   ▼
        Swing Detection Engine
                   │
                   ▼
         Market Structure Engine
           ├── Swing Structure
           └── Internal Structure
                   │
                   ▼
      BOS / CHoCH Detection Engine
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
 Order Blocks   Liquidity   Fair Value Gaps
        │          │          │
        └──────────┼──────────┘
                   ▼
      Premium / Discount Zones
                   │
                   ▼
      Visualization & Alerts
```

Status:

🟡 Initial architecture hypothesis.

---

# Major Subsystems

| Component | Status |
|------------|--------|
| Inputs | 🟡 |
| Swing Detection | 🟡 |
| Internal Structure | 🟡 |
| Swing Structure | 🟡 |
| BOS | 🟡 |
| CHoCH | 🟡 |
| Order Blocks | 🟡 |
| Fair Value Gaps | 🟡 |
| Liquidity | 🟡 |
| Equal High / Low | 🟡 |
| Previous High / Low | 🟡 |
| Premium / Discount | 🟡 |
| Candle Coloring | 🟡 |
| Alerts | 🟡 |

---

# Data Flow

Current hypothesis:

```
OHLC Data
     │
     ▼
Pivot Detection
     │
     ▼
Swing Identification
     │
     ▼
Market Structure
     │
     ▼
Trend State
     │
     ▼
BOS / CHoCH
     │
     ├──────────────┐
     ▼              ▼
Order Blocks     Liquidity
     │              │
     └──────┬───────┘
            ▼
      Fair Value Gaps
            ▼
 Premium / Discount Zones
            ▼
      Chart Rendering
```

Status:

🟡 Needs validation.

---

# Observations

## General

Status: 🟡

Observations:

- Indicator is modular.
- Features can be individually enabled or disabled.
- Internal and Swing structures appear to operate independently.
- Several components reuse information produced by earlier stages.

---

# Unknowns

Current questions:

- Which subsystem runs first?
- Which calculations are performed on every candle?
- Which calculations only occur after pivot confirmation?
- Which objects are persistent?
- Which calculations depend on historical state?
- Which modules communicate with each other?

---

# Reverse Engineering Strategy

Each subsystem will be analysed independently.

Workflow:

1. Read source code.
2. Observe chart behaviour.
3. Form hypotheses.
4. Validate hypotheses.
5. Document findings.
6. Implement independently.
7. Compare behaviour.

---

# Feature Analysis Checklist

## Swing Detection

Status:

🔲 Not Started

Questions:

- How are pivots detected?
- Pivot length?
- Confirmation logic?
- Equal highs?
- Equal lows?
- Noise filtering?
- Internal vs Swing pivots?

---

## Market Structure

Status:

🔲 Not Started

Questions:

- How is trend determined?
- When does structure update?
- How are higher highs detected?
- How are lower lows detected?

---

## BOS

Status:

🔲 Not Started

Questions:

- What exactly confirms a BOS?
- Wick or close?
- Internal BOS?
- Swing BOS?
- Multi-break handling?

---

## CHoCH

Status:

🔲 Not Started

Questions:

- Relationship with BOS?
- Trend reversal conditions?
- Internal CHoCH?
- Swing CHoCH?

---

## Order Blocks

Status:

🔲 Not Started

Questions:

- Candidate candle?
- Validation?
- Mitigation?
- Removal rules?

---

## Fair Value Gaps

Status:

🔲 Not Started

Questions:

- Gap definition?
- Gap removal?
- Partial fills?
- Filtering?

---

## Liquidity

Status:

🔲 Not Started

Questions:

- Equal highs?
- Equal lows?
- Swing liquidity?
- Internal liquidity?

---

## Premium / Discount

Status:

🔲 Not Started

Questions:

- Reference swing?
- Calculation method?
- Midpoint?
- Dynamic updates?

---

# Experiments

This section records practical experiments performed on TradingView.

Example format:

Date:

Instrument:

Timeframe:

Settings:

Observation:

Conclusion:

---

# Conclusions

This section should contain only validated conclusions.

Nothing enters this section until it has been verified.

---

# Implementation Readiness

| Module | Analysis | Design | Code | Validation |
|---------|----------|--------|------|------------|
| Swing Detection | ⬜ | ⬜ | ⬜ | ⬜ |
| Market Structure | ⬜ | ⬜ | ⬜ | ⬜ |
| BOS | ⬜ | ⬜ | ⬜ | ⬜ |
| CHoCH | ⬜ | ⬜ | ⬜ | ⬜ |
| Order Blocks | ⬜ | ⬜ | ⬜ | ⬜ |
| Fair Value Gaps | ⬜ | ⬜ | ⬜ | ⬜ |
| Liquidity | ⬜ | ⬜ | ⬜ | ⬜ |
| Premium / Discount | ⬜ | ⬜ | ⬜ | ⬜ |