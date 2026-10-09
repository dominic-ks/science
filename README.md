# Scientific Experiments

This repository records my scientific, engineering, and practical experiments.

The purpose is not just to store finished results. Each project should preserve the reasoning trail: what was tried, what was measured, what failed, what worked, and what question should be answered next.

---

## Projects

| Project | Status | Notes |
|---------|--------|-------|
| [Onyx](./projects/onyx/README.md) | Active measurement / planning | Small remote-controlled submarine project, currently using V1 to answer buoyancy and ballast questions before V2 |
| [Disposable dehumidifiers](./projects/disposable-dehumidifiers/README.md) | Planning / baseline setup | Household condensation monitoring study using a Pi Zero, DHT22, and weather data |
| [Air Portsmouth](./projects/air-portsmouth/README.md) | Exploratory hardware / documentation | Low-cost, exploratory air quality monitoring project combining public AQ data with locally-built sensors to fill spatial gaps |
| [Sensor calibration](./projects/sensor-calibration/README.md) | Planned (setup ready) | Checking low-cost humidity sensors against physical references; first check is the Sonoff SNZB-02D over saturated salt, which anchors the device-003 DHT22 correction |

---

## Shared Documentation

| File | Purpose |
|------|---------|
| [approach.md](./approach.md) | General working process for all projects |
| [scientific-documentation-standard.md](./scientific-documentation-standard.md) | Reusable documentation structure for projects, phases, builds, and tests |

---

## Repository Structure

```text
README.md
approach.md
scientific-documentation-standard.md
projects/
  onyx/
    README.md
    onyx-v1/
      README.md
      build.md
      tests.md
      v2-plan.md
      approach.md
      images/
  disposable-dehumidifiers/
    README.md
  air-portsmouth/
    README.md
    aq-v1/
      README.md
      build.md
      tests.md
      v2-plan.md
      approach.md
  sensor-calibration/
    README.md
    sonoff-salt-check/
      README.md
      setup.md
      tests.md
      next-plan.md
```

Project directories contain their own overview and version/phase documentation. Root-level documents define the common process and documentation standard.
