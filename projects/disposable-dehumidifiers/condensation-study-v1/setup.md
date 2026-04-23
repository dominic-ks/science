# Condensation Study V1 — Setup

This file records the measurement setup for the first disposable dehumidifier study.

---

## Measurement Location

| Field | Value |
|-------|-------|
| House area | Loft bedroom |
| Specific location | Eaves storage |
| Reason for selection | Condensation build-up is frequently observed here |
| Sensor placement | TBC |
| Distance from wall / roof / stored objects | TBC |
| Ventilation state | TBC |

Record any access doors, vents, insulation, stored items, or local cold surfaces that may affect readings.

---

## Sensor Hardware

| Component | Detail |
|-----------|--------|
| Computer | Raspberry Pi Zero |
| Sensor | DHT22 temperature / humidity sensor |
| Firmware | [`iot-nest-firmware`](https://github.com/dominic-ks/iot-nest-firmware) |
| Power source | USB from mains power |
| Network connection | WiFi |

---

## Data Sources

| Source | Measurement | Notes |
|--------|-------------|-------|
| DHT22 in eaves storage | Local temperature and relative humidity | Primary indoor measurement |
| [OpenWeatherMap](https://openweathermap.org/) | Outside temperature and relative humidity | Used to compare indoor changes with outdoor conditions |

The OpenWeatherMap location used, sampling interval, and data retention method are still TBC.

---

## Setup Checks

- [ ] Confirm the DHT22 is logging plausible temperature and humidity readings.
- [ ] Confirm timestamps are recorded consistently.
- [ ] Confirm data can be exported for analysis.
- [ ] Confirm OpenWeatherMap data is available for the same period.
- [ ] Record the sensor placement with enough detail to repeat the setup.
- [ ] Avoid moving the sensor between S1 and S2 unless the move is explicitly recorded.

---

## Known Limitations

- DHT22 readings may not be precision-grade, so the experiment should focus on sustained differences and trends rather than tiny changes.
- The eaves storage may be affected by outdoor weather, heating patterns, ventilation, and room use.
- A disposable dehumidifier collecting water does not prove the space is drier overall; humidity readings before and after installation are needed.
