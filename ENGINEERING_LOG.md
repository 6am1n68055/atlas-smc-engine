# Engineering Log

This document records important engineering decisions, architecture discussions,
implementation notes, and project milestones throughout the development of the
SMC Engine.

Unlike `CHANGELOG.md`, this file captures *why* decisions were made.

---

# 2026-07-21

## Sprint 0 – Project Foundation

### Repository

- Created the `smc-engine` GitHub repository.
- Initialized Git.
- Adopted a feature-branch workflow.
- `main` will always remain stable.

---

### Development Workflow

Every feature follows the same lifecycle:

1. Research
2. Design
3. Implementation
4. Review
5. Validation against LuxAlgo
6. Commit
7. Merge into `main`

No feature is considered complete until it passes validation.

---

### Branch Strategy

Development will never happen directly on `main`.

Feature branches will be used for every subsystem.

Example:

- feature/project-setup
- feature/swing-detection
- feature/market-structure
- feature/bos
- feature/choch

---

### Project Goal

Build a clean-room implementation of the LuxAlgo Smart Money Concepts indicator.

Objectives:

- Match LuxAlgo behaviour as closely as possible.
- Produce maintainable, well-documented code.
- Design the engine so it can later be ported to Python.
- Build the foundation for a local AI-powered trading assistant.

---

### Architecture Decision

The project will be developed as an **SMC Engine**, not merely as a TradingView indicator.

The indicator is considered one consumer of the engine.

Future consumers include:

- TradingView
- Python
- Telegram Alert Engine
- AI Trading Assistant
- Backtesting Engine

---

### Development Principles

- Readability over cleverness.
- Deterministic calculations.
- Modular design.
- Test before merge.
- Document every algorithm.
- Keep functions focused on a single responsibility.

---

### Validation Philosophy

Success is measured by **decision parity**, not visual similarity.

The engine should identify the same:

- Swing Highs
- Swing Lows
- BOS
- CHoCH
- Order Blocks
- Fair Value Gaps
- Liquidity events

on the same candles as LuxAlgo.

Visual appearance is secondary.

---

### Documentation Strategy

Every subsystem will receive dedicated documentation before implementation.

Examples:

- ARCHITECTURE.md
- SWING_DETECTION.md
- MARKET_STRUCTURE.md
- BOS.md
- CHOCH.md
- ORDER_BLOCKS.md
- FVG.md

---

### Current Milestone

Sprint 0

Status:

✅ Repository created

✅ Git workflow established

✅ Branch strategy defined

✅ Initial architecture discussion completed

⏳ Reverse engineering LuxAlgo architecture

⏳ Swing Detection design

---

### Notes

The project will prioritize engineering quality over development speed.

Time invested in design and documentation is expected to reduce implementation complexity
and improve long-term maintainability.