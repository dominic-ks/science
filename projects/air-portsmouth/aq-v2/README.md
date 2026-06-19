# Air Portsmouth AQ V2

This directory records the second Air Portsmouth air quality device. For overall project context, see the [project README](../README.md).

Within the wider Air Portsmouth project, this documentation covers my personal development work on the node hardware rather than the full project repository or application stack.

## What Is V2?

V2 builds on the V1 prototype. The core aim is to turn the system into a more credible measurement platform — replacing the weakest hardware components, running the calibration and co-location work that V1 did not complete, and establishing a structured test methodology for future deployments.

The first hardware upgrade stage is complete. The DHT22 has been replaced with a BME680, the MQ-135 has been removed from the core measurement path, and the upgraded unit is deployed with sensors reporting. The MICS6814 is kept but treated as experimental only, with investigation of its V1 dropout as part of the test programme.

The V2 programme is structured in three phases:

- **Phase 1** — build and validate the V2 sensor platform on the existing mains/WiFi architecture.
- **Phase 2** — develop and validate a LoRa/battery field node for temporary co-location deployments without local power or network infrastructure.
- **Phase 3** — co-location calibration against official local sensors using the Phase 2 field node.

---

## Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Replace DHT22 with BME680 for better environmental sensing | ✅ Done |
| 2 | Remove MQ-135 from core measurement path | ✅ Done |
| 3 | Retain MICS6814 as experimental only, investigate V1 dropout | ✅ Done |
| 4 | Design and test a controlled enclosure and airflow path | ⬜ Not started |
| 5 | Develop and validate a LoRa/battery field node for temporary co-location deployments | ⬜ Not started |
| 6 | Run co-location calibration with official local sensors | ⬜ Not started |
| 7 | Quantify and model PM vs humidity correction | ⬜ Not started |
| 8 | Establish a validated test methodology for future deployments | ⬜ Not started |

---

## Status

**V2 is in progress.** The first hardware upgrade stage is complete and the upgraded mains/WiFi unit is running in home deployment.

---

## Document Index

| File | Purpose |
|------|---------|
| [build.md](./build.md) | V2 hardware architecture, sensor choices, and design changes from V1 |
| [tests.md](./tests.md) | Planned and completed tests for V2 |
| [approach.md](./approach.md) | Project-specific working method for AQ device development |

---

## How to Use This Docs System

- **Sensor choice, architecture, or design changes?** → [build.md](./build.md)
- **What testing is planned or has happened?** → [tests.md](./tests.md)
- **How should AQ work be run?** → [approach.md](./approach.md)
