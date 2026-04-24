# Air Portsmouth AQ V1 — Build Documentation

## System Overview

| Subsystem | Description |
|-----------|-------------|
| PM Sensor | PMS5003 |
| Gas Sensors | MICS6814, MQ-135 |
| Env Sensor | DHT22 (initial) |
| Controller | Raspberry Pi Pico |
| Host | Raspberry Pi Zero W |
| Comms | USB serial between Pico and Pi |
| Output Path | Device data forwarded from Pi Zero over network upload [TBC — specific upload implementation] |

---

## Build Intent

V1 was built to answer a practical device question: can a low-cost node collect particulate, environmental, and experimental gas-sensor data in the field using a Pi Zero + Pico split?

The build should be understood as exploratory integration rather than a validated instrument design.

---

## Sensors

### PMS5003

**Role:** particulate measurement for PM2.5 / PM10 trend monitoring.

**Strength:**
- Produces data that appears stable enough to observe relative changes and trends.

**Limitations:**
- Not calibrated against a local reference.
- Readings may be affected by humidity.
- Absolute accuracy is unknown.

### MICS6814

**Role:** experimental multi-gas sensing for broad CO / NO2 / NH3 response.

**Strength:**
- Allows experimentation with a compact low-cost gas-sensor module.

**Limitations:**
- Cross-sensitive across multiple gases.
- Subject to drift.
- Does not provide pollutant-specific values without a stronger calibration and interpretation model.

### MQ-135

**Role:** broad gas / VOC indication.

**Strength:**
- Useful only as a rough exploratory signal.

**Limitations:**
- Not reliable for meaningful AQ interpretation.
- Effectively unusable for serious measurement without a very constrained experimental context.

### DHT22

**Role:** temperature and humidity context.

**Strength:**
- Low-cost and simple to integrate.

**Limitations:**
- Low precision.
- Slow response.
- Too weak as the long-term environmental sensor for correction work.

---

## Architecture

The device uses a split architecture:

- The Raspberry Pi Pico handles direct sensor interfacing.
- The Raspberry Pi Zero W handles network connectivity and data upload.
- Communication between the two is via USB serial.

This separation is useful because it keeps timing-sensitive sensor logic away from higher-level host tasks. It also makes it easier to evolve sensor firmware and host-side handling separately.

Current architectural understanding:

- Pico side: sensor reads, UART handling, and analog acquisition via [`dominic-ks/iot-pico-enviro`](https://github.com/dominic-ks/iot-pico-enviro)
- Pi Zero side: local host duties, buffering, and network upload via [`dominic-ks/iot-nest-firmware`](https://github.com/dominic-ks/iot-nest-firmware)

[TBC — specific serial protocol format and message schema]

---

## Power and Deployment

Known deployment assumptions for V1:

- Mains powered
- USB cables run through windows where needed
- WiFi used for connectivity

This is sufficient for exploratory fixed-location deployment, but not yet a validated long-term installation approach.

---

## Issues

### No Calibration Baseline

No calibration baseline is recorded for V1. This means the system can collect values, but cannot support strong claims about absolute particulate or gas concentrations.

### Unknown PM Accuracy

The PMS5003 may still be useful for trends, but its local absolute accuracy is unknown without co-location against a reference station or equivalent validation method.

### Gas Sensors Are Not Interpretable

The MICS6814 and MQ-135 add exploratory signals, but those signals do not currently support defensible interpretation. The cross-sensitivity and drift make them poor candidates for trusted pollutant values in V1.

### No Controlled Airflow Design

No validated enclosure or airflow path is documented. Without controlled intake, outlet, and sensor positioning, it is hard to know whether the device is sampling air consistently.

### Sensor Placement Is Inconsistent

Sensor placement and local environmental exposure are not yet documented or standardised tightly enough to compare deployments with confidence.

### Environmental Correction Not Applied

Humidity and temperature context are important for interpreting particulate readings, but no environmental correction workflow is documented for V1.

---

## Next Build — Key Hardware Improvements

- [ ] Replace the DHT22 with a higher-quality environmental sensor such as BME280
- [ ] Remove MQ-135 from the core measurement path
- [ ] Keep MICS6814 only as an experimental channel unless a clear interpretation method is proven
- [ ] Define and test a controlled enclosure and airflow path
- [ ] Standardise sensor placement and deployment method
- [ ] Record the Pico-to-Pi serial schema and host-side handling explicitly
- [ ] Run calibration and co-location work before making stronger measurement claims
