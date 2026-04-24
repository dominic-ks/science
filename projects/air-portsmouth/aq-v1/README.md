# Air Portsmouth AQ V1

This directory records the first Air Portsmouth air quality device. For overall project context, see the [project README](../README.md).

Within the wider Air Portsmouth project, this documentation covers my personal development work on the node hardware rather than the full project repository or application stack.

## What Was V1?

V1 was an exploratory prototype built to test a low-cost sensor stack, validate the system architecture, and establish whether the device could produce a usable field data stream.

It was not a calibrated instrument and should not be treated as suitable for defensible measurements. Its value is mainly in exposing which parts of the system behave consistently enough to justify a more rigorous V2.

---

## Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Collect particulate data using PMS5003 | ⚠️ Partial — useful trend data appears possible, but absolute accuracy is unvalidated |
| 2 | Capture environmental context with temperature and humidity sensing | ⚠️ Partial — data possible, but DHT22 quality and consistency are limited |
| 3 | Experiment with low-cost gas sensors | ⚠️ Partial — sensors produced output, but interpretation is weak |
| 4 | Validate the Pi Zero + Pico split architecture | ⚠️ Partial — architecture appears workable, but field robustness and documentation remain incomplete |
| 5 | Produce a usable device-side data stream | ⚠️ Partial — the device appears to output data, but scientific trust in that data is unresolved |

---

## Final Status

**V1 is technically useful but scientifically incomplete.**

It demonstrated that a low-cost device can be assembled and deployed. It did not establish that the measurements are calibrated, interpretable, or suitable for claims beyond trend-level exploratory use.

V1 should therefore be treated as an architecture and sensor-evaluation platform rather than a finished air quality monitor.

### What Works

- PMS5003 appears capable of providing stable trend data
- The Pi Zero + Pico split architecture appears workable
- A device-side data collection path exists
- Devices can be deployed in real environments

### What Doesn't

- No calibration baseline exists
- Gas sensors are unreliable for absolute pollutant values
- Environmental sensing is inconsistent because DHT22 quality is limited
- No validated enclosure or airflow design exists
- There is no confidence in absolute readings

---

## Document Index

| File | Purpose |
|------|---------|
| [build.md](./build.md) | V1 hardware architecture, sensor notes, and known design issues |
| [tests.md](./tests.md) | What was and was not validated during V1 |
| [v2-plan.md](./v2-plan.md) | Forward plan for calibration, hardware changes, and test design |
| [approach.md](./approach.md) | Project-specific working method for AQ device development |

---

## How to Use This Docs System

- **Sensor choice, architecture, or deployment detail?** → [build.md](./build.md)
- **What testing happened or is still missing?** → [tests.md](./tests.md)
- **What V2 must fix next?** → [v2-plan.md](./v2-plan.md)
- **How should future AQ work be run?** → [approach.md](./approach.md)
