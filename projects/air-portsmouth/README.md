# Air Portsmouth

Air Portsmouth is a low-cost, exploratory air quality monitoring project focused on combining existing air quality data sources with locally-built sensors to improve neighbourhood-level visibility.

The main Air Portsmouth project repository is [dominic-ks/air-portsmouth](https://github.com/dominic-ks/air-portsmouth). The documentation in this repository is narrower in scope: it records my personal device-development work for the sensor nodes used in that wider project.

This device work is exploratory and not aimed at regulatory measurement.

---

## Device Description

This documentation focuses on the node hardware rather than the wider software or platform stack. The device work is early-stage and exploratory. The current device should be treated as a prototype used to understand what can be measured reliably, what cannot, and what the next hardware iteration needs to fix.

---

## Purpose

- Build and document low-cost air quality nodes for real deployment.
- Test whether the sensor stack produces useful trend data.
- Identify which sensors are worth keeping for the next hardware iteration.
- Record what would be required before the device could support stronger claims.

This device should not be described as regulatory-grade or equivalent to validated reference instrumentation.

---

## Device Scope

The device is intended to:

- capture local trends
- capture environmental context alongside particulate readings
- test experimental gas sensors without over-claiming what they mean
- expose what needs calibration, correction, enclosure work, or removal in V2

At this stage, it should be described as **low-cost, exploratory air quality monitoring hardware**.

---

## Code References

- Raspberry Pi Zero W host code: [`dominic-ks/iot-nest-firmware`](https://github.com/dominic-ks/iot-nest-firmware)
- Raspberry Pi Pico sensor code: [`dominic-ks/iot-pico-enviro`](https://github.com/dominic-ks/iot-pico-enviro)

---

## Versions

| Version | Status | Notes |
|---------|--------|-------|
| [AQ V1](./aq-v1/README.md) | Exploratory prototype | First hardware iteration used to test sensor mix, Pi Zero + Pico architecture, and real-world data collection |

---

## Current Direction

V1 appears useful as a technical prototype, but not yet as a defensible measurement device.

The main questions now are:

- how much trust can be placed in PMS5003 trend data
- how strongly humidity affects the readings
- which sensors belong in the next device revision
- what calibration, enclosure, and test method are required before V2 can support stronger claims
