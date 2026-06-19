# Air Portsmouth AQ V2 — Build Documentation

## Build Intent

V2 builds on the V1 prototype. The goal is to improve hardware reliability and environmental sensing, reduce the sensor stack to what can actually be characterised, and run the calibration and co-location work that V1 did not complete.

The V2 programme evolved during development into two related deployment architectures:

- **Standard mains/WiFi nodes** — for long-term home and fixed-site deployments.
- **Low-power LoRa/battery field nodes** — for temporary co-location and remote deployments without local power or network infrastructure.

The two architectures share the same sensor stack, payload structure, and backend ingestion pipeline, but differ in transport layer, power strategy, and deployment assumptions.

The build is structured in two phases accordingly:

- **Phase 1** — build and validate the V2 sensor platform on the mains/WiFi architecture.
- **Phase 2** — develop and validate the LoRa/battery field node architecture.

Phase 3 (co-location calibration) uses the Phase 2 field node at the co-location site and does not require a separate build.

The build should be understood as an improved calibration and validation platform — not a finished measurement system.

---

## Changes from V1

| Area | Change | Reason |
|------|--------|--------|
| Environmental sensing | DHT22 → BME680 | DHT22 precision and response were too limited for correction work |
| Gas sensing | MQ-135 removed | Too broad and unreliable for meaningful AQ interpretation |
| Gas sensing | MICS6814 retained as experimental only | V1 dropout cause unknown — keep for investigation but treat as untrusted |
| Enclosure | Controlled enclosure and airflow path to be designed | V1 had no validated intake or outlet |

---

## Sensors

### PMS5003

**Role:** particulate measurement for PM2.5 / PM10 trend monitoring.

**Strength:**
- Produces data that appears stable enough to observe relative changes and trends.

**Limitations:**
- Requires co-location calibration against official local sensors.
- Readings are affected by humidity and require correction.
- Dominant power consumer in battery deployments — power-cycle between readings rather than running continuously.

### BME680

**Role:** core environmental sensing — temperature, humidity, and pressure for AQ correction work. Gas resistance output is experimental.

**Strength:**
- Significantly better precision and response than the DHT22 it replaces.
- Pressure output adds useful environmental context.

**Limitations:**
- Gas resistance output should not be treated as a trusted pollutant value without further characterisation.
- Current V2 deployment has shown a fixed-temperature fault: temperature flat at 34.7 deg C from 2026-06-15 03:32:29, followed by a reporting gap from 2026-06-17 02:27:30 for approximately 36 hours, then reporting resumed still fixed at 34.7 deg C. Restarting did not clear the fault. Investigate before relying on BME680 data for correction work.

### MICS6814

**Role:** experimental multi-gas sensing for broad CO / NO2 / NH3 response.

**Status:**
- Retained from V1 for investigation purposes only.
- Stopped reporting data during V1 deployment — cause unknown. Investigating this is part of the V2 test programme.
- Do not include in the core measurement path until interpretation method is validated and dropout cause is resolved.
- Likely to be excluded from Phase 2 battery deployments: heater power requirements are problematic for duty-cycled operation, and gas values are not part of the co-location calibration programme.

**Exploratory analysis note:**
Even though MICS6814 output is not being treated as a primary measurement, there may be value in running exploratory analysis during mains-powered home deployments. Cross-referencing MICS values against PMS5003 readings and BME680 temperature, humidity, and pressure — and potentially applying correction models derived from the PMS5003 calibration work — may reveal whether any interpretable signal exists. This is not a calibration objective but may be worth documenting.

---

## Phase 1 — V2 Sensor Platform (Mains / WiFi)

### Hardware Overview

| Subsystem | Description |
|-----------|-------------|
| PM Sensor | PMS5003 |
| Gas Sensor | MICS6814 (experimental only) |
| Env Sensor | BME680 (temperature, humidity, pressure, experimental gas resistance) |
| Controller | Raspberry Pi Pico |
| Host | Raspberry Pi Zero W |
| Comms | USB serial between Pico and Pi |
| Output Path | Device data forwarded from Pi Zero over network upload [TBC — specific upload implementation] |

### Architecture

- The Raspberry Pi Pico handles direct sensor interfacing.
- The Raspberry Pi Zero W handles network connectivity and data upload.
- Communication between the two is via USB serial.

- Pico side: sensor reads, UART handling, and analog acquisition via [`dominic-ks/iot-pico-enviro`](https://github.com/dominic-ks/iot-pico-enviro)
- Pi Zero side: local host duties, buffering, and network upload via [`dominic-ks/iot-nest-firmware`](https://github.com/dominic-ks/iot-nest-firmware)

[TBC — specific serial protocol format and message schema]

### Enclosure and Airflow

The enclosure and airflow design must prevent the environmental sensor from measuring sun-warmed enclosure air instead of ambient air. The current enclosure has bottom ventilation holes, but field observations suggest that may not be enough during sunny periods.

Requirements:
- Controlled air intake and outlet
- Defined sensor positioning
- Protection from direct exposure without blocking airflow
- Repeatable installation method
- Shield environmental sensor from direct and indirect solar heating
- Keep environmental sensor airflow representative of ambient air

**Candidate enclosure:** 150×110×70mm waterproof PC plastic junction box — [Temu](https://www.temu.com/uk/-1-2pcs-waterproof-sand-resistant-outdoor-electrical-junction-box-durable-pc-plastic-enclosure-for-tight-spaces-no-opening-design--wiring-150x110x70-grey-wall-mount-box-secure--closure--seal-g-601101116601921.html) (available as 1 or 2 pack — consider ordering 2 to allow lid swapping during sensor work).

**Candidate environmental sensor shield:** use a white plumbing part as a passive radiation shield, with upward-sloped drilled side holes for ventilation, insect net over the bottom opening, and the BME680 mounted inside. The sensor cable runs back to the main unit. This should be tested against the current configuration and nearby weather station data before deciding whether it becomes part of the standard node design.

### Power and Deployment

- Mains powered
- WiFi used for connectivity
- USB cables run through windows where needed

---

## Phase 2 — LoRa / Battery Architecture

Phase 2 replaces USB serial and WiFi with LoRa point-to-point telemetry, and replaces mains power with a LiPo battery and charging circuit. This allows the field node to be deployed at temporary co-location sites without local power or network infrastructure.

The LoRa/battery architecture is not intended to replace mains/WiFi nodes. It is intended to enable temporary deployments, calibration studies, and locations that are hard to network or reach with mains power.

### Field Node

Battery-powered low-power sensor node.

#### Hardware Overview

| Subsystem | Description |
|-----------|-------------|
| PM Sensor | PMS5003 |
| Env Sensor | BME680 |
| Gas Sensor | MICS6814 (optional — include if power budget allows) |
| Controller | Raspberry Pi Pico |
| Comms | Adafruit RFM95W LoRa breakout (868 MHz) |
| Power | LiPo battery + Adafruit bq25185 USB/DC/Solar charger + 5V boost board |

#### Power Architecture

- LiPo battery feeds the bq25185 charger/boost board, providing a 5V rail output.
- 5V rail powers PMS5003 directly, and the Pico via VSYS/VBUS.
- 3V3 rail from the Pico powers the LoRa module, BME680, and other low-voltage sensors.

#### Duty Cycle

To minimise power consumption during battery deployments:

1. Wake node
2. Enable PMS5003
3. Wait for airflow stabilisation
4. Collect sensor readings
5. Transmit LoRa packet
6. Return to sleep

### Home Gateway

Fixed gateway receiving LoRa packets from the field node and forwarding data upstream.

#### Hardware Overview

| Subsystem | Description |
|-----------|-------------|
| LoRa Receiver | LilyGO TTGO LoRa32 (868 MHz) |
| Host | Raspberry Pi Zero W |
| Comms | USB serial between TTGO and Pi Zero |
| Output Path | Pi Zero handles packet ingestion, buffering, and network upload |

#### Architecture

- The TTGO LoRa32 acts as a LoRa packet receiver and serial bridge.
- The Pi Zero ingests packets from the TTGO and forwards data to the backend.
- Backend payload format is transport-agnostic — same schema whether data arrives via LoRa, USB serial, or WiFi.

Note: 868 MHz (UK/EU band) only.

### Parts to Purchase

The following Phase 2 components are yet to be purchased:

| Item | Source |
|------|--------|
| Adafruit RFM95W LoRa breakout (868 MHz) | [The Pi Hut](https://thepihut.com/products/adafruit-rfm95w-lora-radio-transceiver-breakout-868-or-915-mhz?variant=27740304337) |
| 2000mAh 3.7V LiPo battery | [The Pi Hut](https://thepihut.com/products/2000mah-3-7v-lipo-battery?variant=42143258050755) |
| Adafruit bq25185 USB/DC/Solar charger + 5V boost board | [The Pi Hut](https://thepihut.com/products/adafruit-bq25185-usb-dc-solar-charger-with-5v-boost-board?variant=53804937380225) |
| LilyGO TTGO LoRa32 (868 MHz) | [AliExpress](https://www.aliexpress.com/item/1005003062523617.html) |

---

## Open Items

### Phase 1

- [ ] Design and test enclosure and airflow path
- [ ] Determine whether a spare enclosure or additional lid is needed to enable swapping during sensor replacement
- [ ] Investigate MICS6814 dropout cause from V1
- [ ] Document serial protocol format and message schema
- [ ] Standardise sensor placement and deployment method

### Phase 2

- [ ] Select and source all field node and gateway hardware
- [ ] Build and bench test field node
- [ ] Build and bench test home gateway
- [ ] Define and document LoRa packet payload schema
- [ ] Determine whether MICS6814 is viable within battery power budget
- [ ] Design and implement power management and duty cycle
- [ ] Investigate BME680 fixed-temperature fault before relying on environmental correction values
- [ ] Build and test passive radiation shield / external BME680 arrangement
