# Onyx V1 — Project Overview

## What Is This?

The Onyx is a small, remote-controlled submarine. V1 was an exploratory build to prove out the core concept and identify the real engineering challenges.

It is **not** a polished product. It is the first iteration of a structured learning process.

---

**Inspiration:**
This project was inspired by the [Brick Experiment Channel RC Submarine 4.0](https://brickexperimentchannel.wordpress.com/2022/07/01/rc-submarine-4-0-hull-3-10/). The goal was to build a similar vessel using technology we’re more familiar with and as much as possible with parts and materials we already had on hand.

---

## Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Build a watertight enclosure | ⚠️ Partial — reliability unresolved |
| 2 | Achieve basic RC control | ✅ Functional |
| 3 | Implement IR communication | ✅ Transmit + receive working |
| 4 | Achieve controlled submersion | ⚠️ Attempted — not yet stable |
| 5 | Syringe-based ballast system | ⚠️ Acquired, installation pending |

---

## Final Status

**V1 is at end-of-life.** It achieved a functional milestone but did not reach stable, repeatable operation.

> **Scope note:** The original aim was to build a fully RC-controlled submarine in a single version. In practice, the discovery that Bluetooth does not work underwater meant V1's effective scope narrowed considerably — it became a platform for testing controlled submersion and resurfacing only, rather than real-time remote operation. This is a meaningful outcome, but it is not a complete submarine. V2 will address the communication problem as a hard prerequisite.

### What Works
- Basic electronics (ESP32-C3, IR TX/RX)
- Power system (LiPo battery)
- RC control (IR-based)
- Partial submersion

### What Doesn't
- Reliable waterproofing (seals not yet confirmed)
- Stable buoyancy / balance underwater
- Consistent ballast control
- Internal component orientation (may require mounting upside down)

---

## Key Learnings

1. **Physical design dominates** — software complexity is not the bottleneck; sealing, buoyancy, and layout are.
2. **Fixed solutions are limiting** — adjustable/modular systems are required for reliable iteration.
3. **Orientation matters more than expected** — the unit may need to run upside down to function correctly.
4. **Waterproofing needs multiple layers** — single-point sealing is not sufficient.
5. **Tight enclosures constrain everything** — component placement must be solved before electronics.

---

## Document Index

| File | Purpose |
|------|---------|
| [build.md](./build.md) | System design, components, physical layout |
| [tests.md](./tests.md) | All experiments and test logs |
| [failures.md](./failures.md) | Explicit failure tracking |
| [lessons.md](./lessons.md) | Engineering insights and process lessons |
| [v2-plan.md](./v2-plan.md) | Forward planning for V2 |

---

## How to Use This Docs System

- **Adding a test?** → [tests.md](./tests.md) — follow the template exactly
- **Something broke?** → [failures.md](./failures.md) — log it immediately
- **Had an insight?** → [lessons.md](./lessons.md)
- **Planning V2?** → [v2-plan.md](./v2-plan.md)
