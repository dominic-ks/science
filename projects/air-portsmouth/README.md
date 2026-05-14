# Air Portsmouth

Air Portsmouth is a low-cost air quality monitoring project focused on combining existing air quality data sources with locally-built sensors to improve neighbourhood-level visibility, as well as an exploratory scientific exercise simply to observe what is happening across the city.

The main Air Portsmouth project repository is [dominic-ks/air-portsmouth](https://github.com/dominic-ks/air-portsmouth). The documentation in this repository is narrower in scope: it records my personal device-development work for the sensor nodes used in that wider project.

The device work is aimed at understanding how locally-built sensor nodes can produce credible neighbourhood-scale data when paired with calibration, environmental correction, and careful deployment practice.

---

## Device Description

This documentation focuses on the node hardware rather than the wider software or platform stack. The current device should be treated as a prototype used to understand what can be measured reliably, what needs calibration or correction, and what the next hardware iteration needs to fix.

---

## Purpose

- Build and document low-cost air quality nodes for real deployment.
- Test whether the sensor stack produces useful local trend data.
- Identify which sensors are worth keeping for the next hardware iteration.
- Record what would be required before the device could support stronger claims.

## Device Scope

The device is intended to:

- Capture local trends
- Capture environmental context alongside particulate readings
- Test gas sensors while documenting calibration limits clearly
- Expose what needs calibration, correction, enclosure work, or removal in V2

At this stage, it should be described as **low-cost air quality monitoring hardware under active calibration and validation**.

---

## Code References

- Raspberry Pi Zero W host code: [`dominic-ks/iot-nest-firmware`](https://github.com/dominic-ks/iot-nest-firmware)
- Raspberry Pi Pico sensor code: [`dominic-ks/iot-pico-enviro`](https://github.com/dominic-ks/iot-pico-enviro)

---

## Versions

| Version | Status | Notes |
|---------|--------|-------|
| [AQ V1](./aq-v1/README.md) | Complete | First hardware iteration used to test sensor mix, Pi Zero + Pico architecture, and real-world data collection |
| [AQ V2](./aq-v2/README.md) | In progress | Improved hardware with BME680, controlled enclosure, and structured calibration and co-location test programme |

---

## Current Direction

V1 is complete. It demonstrated that a low-cost device can be assembled and deployed, and identified what needs to change for the next iteration.

V2 is now in progress. The main objectives are:

- Replace the DHT22 with a BME680 for reliable environmental correction data
- Remove the MQ-135 and treat the MICS6814 as experimental only
- Design a controlled enclosure and airflow path
- Run co-location calibration of PMS5003 against official local sensors
- Complete the temperature and humidity correction work needed before making stronger particulate claims
