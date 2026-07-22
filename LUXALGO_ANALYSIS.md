# LuxAlgo Analysis

> **Purpose**
>
> This document captures the reverse engineering process of the LuxAlgo Smart Money Concepts indicator.
>
> The objective is to understand the indicator's architecture, algorithms, and behaviour in order to build an independent clean-room implementation for the Atlas Engine.
>
> No source code from LuxAlgo is reproduced here. Only observations, hypotheses, experiments, conclusions, and Atlas design decisions are documented.

---

# Reverse Engineering Sessions

---

# Session 001 — Core Data Model & Engine State

**Date:** 2026-07-21

## Objective

Understand how the indicator models market concepts and manages state before analysing any trading algorithms.

---

## OBS-001 — Domain-Driven Design

**Status:** ✅ Confirmed

The indicator models trading concepts as reusable data structures (UDTs) rather than relying solely on primitive variables.

### Identified Domain Models

| Data Structure | Purpose |
|----------------|---------|
| `alerts` | Stores alert events generated during the current bar |
| `pivot` | Represents a market structure pivot |
| `trend` | Stores current trend bias |
| `orderBlock` | Represents an Order Block |
| `fairValueGap` | Represents a Fair Value Gap |
| `trailingExtremes` | Tracks recent market extremes |
| `equalDisplay` | Stores Equal High / Low drawing objects |

### Conclusion

The indicator is organized around domain objects, making the code modular and easier to maintain.

---

## OBS-002 — Persistent Engine State

**Status:** ✅ Confirmed

The indicator stores market state across bars using persistent objects (`var`) and arrays.

Persistent state includes:

- Swing High
- Swing Low
- Internal High
- Internal Low
- Equal High
- Equal Low
- Swing Trend
- Internal Trend
- Order Blocks
- Fair Value Gaps
- Historical price data

### Conclusion

The engine continuously updates market state rather than recalculating everything from scratch on every candle.

---

## OBS-003 — Historical Data Storage

**Status:** ✅ Confirmed

Historical market data is stored explicitly.

Observed collections include:

- Parsed Highs
- Parsed Lows
- Raw Highs
- Raw Lows
- Time values
- Order Blocks
- Fair Value Gaps

### Conclusion

The engine relies on maintained historical state instead of depending exclusively on Pine Script's historical indexing.

---

## OBS-004 — Price Preprocessing

**Status:** ✅ Confirmed

Before higher-level market structure calculations begin, price data is preprocessed.

Observed preprocessing:

- Volatility measurement
- High-volatility candle detection
- Parsed High
- Parsed Low

### Conclusion

Swing detection is likely performed on processed price data rather than raw OHLC values.

The exact preprocessing algorithm requires further investigation.

---

## OBS-005 — Rendering Optimization

**Status:** ✅ Confirmed

Chart objects such as Order Block boxes are created only once during script initialization and reused afterwards.

### Conclusion

The indicator minimizes runtime object creation by updating existing graphical objects.

This is a performance optimization.

---

## HYP-001 — Initial Processing Pipeline

**Status:** 🟡 Hypothesis

Based on the analysed section, the engine appears to follow the pipeline below:

```
New Candle
      │
      ▼
Read OHLC
      │
      ▼
Volatility Filter
      │
      ▼
Parsed High / Parsed Low
      │
      ▼
Store Historical Data
      │
      ▼
Market Structure Engine
```

This hypothesis will be validated during Swing Detection analysis.

---

# Atlas Design Decisions

The following decisions apply to Atlas and are independent of LuxAlgo.

---

## AD-001 — Engine / Renderer Separation

**Decision**

Atlas will separate market logic from visualization.

The core engine will contain only market data and trading logic.

Rendering (boxes, labels, lines, colours) will be implemented in a dedicated visualization layer.

### Reason

This allows the same engine to be reused by:

- TradingView
- Python
- Backtesting
- AI Trading Assistant

without introducing TradingView-specific dependencies.

---

# Session Summary

### Confirmed Findings

- Domain-driven architecture
- Persistent engine state
- Explicit historical data storage
- Price preprocessing stage
- Rendering object reuse

### Open Questions

- How are pivots detected?
- Why are Parsed High and Parsed Low required?
- How does preprocessing affect Swing Detection?
- Which subsystem consumes `trailingExtremes`?
- When is trend state updated?

---

# Next Session

**Topic**

Swing Detection Engine

Objectives:

- Understand pivot detection
- Identify swing confirmation rules
- Analyse internal vs swing pivots
- Document the complete Swing Detection pipeline