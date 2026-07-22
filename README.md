# Atlas SMC Engine

A clean-room implementation of the Smart Money Concepts (SMC) indicator inspired by the behavior of the LuxAlgo TradingView indicator.

> **Project Status:** 🚧 Active Development

---

## Project Goals

The objective of this project is to build an independent Smart Money Concepts engine that reproduces the behaviour of the original indicator without copying its implementation.

The project follows a reverse-engineering and clean-room development methodology.

Primary goals include:

- Behavioural parity with the reference implementation.
- Clean, modular, and maintainable architecture.
- Independent implementation with no copied source code.
- Comprehensive documentation of the reverse engineering process.
- Future portability to Python for backtesting and live trading systems.

---

## Development Methodology

Every subsystem follows the same engineering workflow:

```
Observe
    ↓
Analyse
    ↓
Document
    ↓
Design
    ↓
Implement
    ↓
Validate
```

No feature is implemented before its behaviour is fully understood and documented.

---

## Current Progress

| Module | Status |
|---------|--------|
| Repository Setup | ✅ Complete |
| Project Architecture | ✅ Complete |
| Engine Data Model Analysis | ✅ Complete |
| Swing Detection Analysis | 🚧 In Progress |
| Market Structure | ⏳ Planned |
| BOS / CHoCH | ⏳ Planned |
| Order Blocks | ⏳ Planned |
| Fair Value Gaps | ⏳ Planned |
| Liquidity | ⏳ Planned |
| Premium / Discount | ⏳ Planned |
| Pine Implementation | ⏳ Planned |
| Python Port | ⏳ Planned |

---

## Repository Structure

```
docs/
pine/
screenshots/
.github/

README.md
CHANGELOG.md
ENGINEERING_LOG.md
LUXALGO_ANALYSIS.md
```

---

## Documentation

- **ENGINEERING_LOG.md** — Development history and engineering decisions.
- **LUXALGO_ANALYSIS.md** — Reverse engineering findings and architectural analysis.
- **docs/** — Detailed documentation for each subsystem.

---

## License

This project is an independent educational and engineering effort.

It is not affiliated with or endorsed by LuxAlgo.