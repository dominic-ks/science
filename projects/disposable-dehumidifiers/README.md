# Disposable Dehumidifiers

This project investigates how effective disposable dehumidifiers are in real household problem areas, starting with the eaves storage in the loft bedroom.

The practical problem is recurring condensation build-up in the eaves storage and elsewhere in the house. Disposable dehumidifiers visibly collect water, but that does not by itself prove that they meaningfully reduce the moisture level in the space. It is possible that removing moisture from the air simply draws more moisture into the area from outside, adjacent rooms, or the building fabric.

---

## Research Question

Do disposable dehumidifiers measurably reduce temperature-adjusted humidity in the loft eaves storage, compared with the same space before dehumidifiers are added?

Secondary questions:

- How variable is humidity in the eaves storage without intervention?
- How strongly does the eaves humidity track outside temperature and humidity?
- Does adding disposable dehumidifiers reduce relative humidity, absolute humidity, or dew point?
- Does any observed change persist, or does moisture appear to be replenished from elsewhere?

---

## Current Measurement Setup

| Component | Role |
|-----------|------|
| Raspberry Pi Zero | Local data-logging / IoT device |
| DHT22 | Temperature and relative humidity sensor |
| [`iot-nest-firmware`](https://github.com/dominic-ks/iot-nest-firmware) | Firmware running on the Pi Zero |
| [OpenWeatherMap](https://openweathermap.org/) | Outside temperature and humidity comparison source |

The first sensor location is the eaves storage in the loft bedroom.

---

## Experiment Phases

| Phase | Status | Purpose |
|-------|--------|---------|
| [Condensation Study V1](./condensation-study-v1/README.md) | Baseline in progress | Measure baseline temperature and humidity, then compare against a period with disposable dehumidifiers installed |

---

## Current Direction

The project should proceed in two main stages:

1. Record a baseline period with no disposable dehumidifiers installed. This is now in progress.
2. Add disposable dehumidifiers and monitor the same space over a comparable period.

The baseline collection period should run for at least two weeks and may run longer. For analysis, select a representative two-week baseline window from the collected data. The key requirement is that each analysed period should be long enough to capture normal day/night variation and weather-driven changes.

---

## Document Index

| File | Purpose |
|------|---------|
| [condensation-study-v1/README.md](./condensation-study-v1/README.md) | First measurement campaign overview |
| [condensation-study-v1/setup.md](./condensation-study-v1/setup.md) | Sensor, firmware, location, and data-source setup |
| [condensation-study-v1/tests.md](./condensation-study-v1/tests.md) | Baseline and dehumidifier test plan |
