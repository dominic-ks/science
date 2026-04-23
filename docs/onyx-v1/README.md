# Onyx V1

This directory records the first Onyx build. For the overall project context and inspiration, see the [main project README](../../README.md).

## What Was V1?

V1 was an exploratory build to prove out the core concept and identify the real engineering challenges. It reached a useful checkpoint, but not stable repeatable operation.

---

## Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Build a watertight enclosure | ⚠️ Partial — reliability unresolved |
| 2 | Achieve basic RC control in air | ✅ Functional |
| 3 | Achieve real-time control underwater | ❌ Blocked — Bluetooth does not work underwater |
| 4 | Achieve controlled submersion | ⚠️ Attempted — not yet stable |
| 5 | Syringe-based ballast system | ⚠️ Mechanically promising, not fully validated |

---

## Final Status

**V1 is no longer suitable for full RC development.** It achieved a functional milestone but did not reach stable, repeatable operation.

> **Scope note:** The original aim was to build a fully RC-controlled submarine in a single version. In practice, the discovery that Bluetooth does not work underwater, lack of enough motor drivers on the circuit, and various other design issues meant V1's effective scope narrowed considerably — it became a platform for testing controlled submersion and resurfacing only, rather than real-time remote operation. This is a meaningful outcome, but it is not a complete submarine. V2 will look to address as many issues as possible, as well as implement a more robust development process.

Although V1 should not be developed further as an RC vehicle, it remains useful as a physical measurement platform. In particular, the existing hull can still answer important questions about displacement, required ballast, centre of mass, ballast distribution, and whether the syringe actuator produces a measurable submerge/resurface effect.

### What Works
- Basic electronics (Pi Pico, HC-05 Bluetooth, motor driver)
- Power from a phone power bank
- RC control in air via Bluetooth serial
- Partial submersion
- Syringe ballast actuation

### What Doesn't
- Reliable waterproofing (seals not yet confirmed)
- Stable buoyancy / balance underwater
- Consistent ballast control
- Real-time underwater communication
- Clean internal packaging and component retention

---

## Document Index

| File | Purpose |
|------|---------|
| [build.md](./build.md) | V1 build record, component notes, and observed issues |
| [tests.md](./tests.md) | Submersion test record and V2 water-test protocol |
| [v2-plan.md](./v2-plan.md) | Forward planning for V2 |
| [approach.md](./approach.md) | Project-level working method for V2 |

---

## How to Use This Docs System

- **Build or component detail?** → [build.md](./build.md)
- **Water test or submersion observation?** → [tests.md](./tests.md)
- **V2 requirement, experiment, or backlog item?** → [v2-plan.md](./v2-plan.md)
- **Process rule or working principle?** → [approach.md](./approach.md)
