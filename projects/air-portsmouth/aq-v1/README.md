# Air Portsmouth AQ V1

This directory records the first Air Portsmouth air quality device. For overall project context, see the [project README](../README.md).

Within the wider Air Portsmouth project, this documentation covers my personal development work on the node hardware rather than the full project repository or application stack.

## What Was V1?

V1 was a prototype built to test a low-cost sensor stack, validate the system architecture, and establish whether the device could produce a usable field data stream.

Its value is in exposing which parts of the system behave consistently enough to justify a more rigorous V2, and in preparing the calibration work needed to turn low-cost particulate readings into credible local data.

---

## Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Collect particulate data using PMS5003 | ⚠️ Partial — useful trend data appears possible, with absolute accuracy depending on co-location calibration and environmental correction |
| 2 | Capture environmental context with temperature and humidity sensing | ⚠️ Partial — data possible, but DHT22 quality and consistency are limited |
| 3 | Test low-cost gas sensors | ⚠️ Partial — sensors produced output, but interpretation still needs stronger calibration |
| 4 | Validate the Pi Zero + Pico split architecture | ⚠️ Partial — architecture appears workable, but field robustness and documentation remain incomplete |
| 5 | Produce a usable device-side data stream | ⚠️ Partial — the device appears to output data, with trust depending on calibration, correction, and repeatability work |

---

## Final Status

**V1 is complete.**

It demonstrated that a low-cost device can be assembled and deployed. V1 should be treated as an architecture and sensor-evaluation platform and as the starting point for calibrated particulate monitoring.

The next step is V2, which replaces the weakest hardware components and runs the calibration, co-location, and environmental correction work that V1 did not complete. See [aq-v2](../aq-v2/README.md).

### What Works

- PMS5003 appears capable of providing stable trend data
- The Pi Zero + Pico split architecture appears workable
- A device-side data collection path exists
- Devices can be deployed in real environments

### What Doesn't

- No calibration baseline exists yet
- Gas sensors need stronger calibration and interpretation before they can support pollutant-specific values
- Environmental sensing is inconsistent because DHT22 quality is limited
- No validated enclosure or airflow design exists
- Absolute readings need co-location calibration before they can support stronger claims

---

## Document Index

| File | Purpose |
|------|---------|
| [build.md](./build.md) | V1 hardware architecture, sensor notes, and known design issues |
| [tests.md](./tests.md) | What was and was not validated during V1 |
| [v2-plan.md](./v2-plan.md) | Forward plan for calibration, hardware changes, and test design — the basis for V2 |
| [approach.md](./approach.md) | Working method written forward for V2 — now lives in [aq-v2/approach.md](../aq-v2/approach.md) |

---

## How to Use This Docs System

- **Sensor choice, architecture, or deployment detail?** → [build.md](./build.md)
- **What testing happened or is still missing?** → [tests.md](./tests.md)
- **What V2 must fix next?** → [v2-plan.md](./v2-plan.md)
- **How should future AQ work be run?** → [approach.md](./approach.md)
