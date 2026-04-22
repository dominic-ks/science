# Onyx V1 — Build Documentation

## System Overview

| Subsystem | Description |
|-----------|-------------|
| Microcontroller | Pi Pico |
| Communication | Bluetooth (HC-05 module, Android phone control) |
| Power | Mobile phone power bank |
| Enclosure | Acrylic tube + custom acrylic lids, O-ring seals |
| Ballast | 60ml syringe-based, lead shot pouch, servo/manual actuation |
| Propulsion | 6x DC geared motors (Gebildet, double axis 1:48), intended for props and syringe drive |

---

## Parts List

**Hull:**
- Clear extruded acrylic plastic perspex tube (250mm length, 110mm OD / 104mm ID)
- Lids cut from smaller diameter acrylic tube and 3mm clear acrylic perspex sheet (300mm x 300mm, polished edges)
- Pair of small magnets attached to one lid for the propeller system

**Ballast:**
- 2kg lead shot pouch (vintage, in IKEA sandwich bag)

**Valve:**
- 1/8" NPT solid brass air compressor tank fill Schrader valve (2pcs)

**Ballast Syringe System:**
- 60ml hydroponics syringes (2pcs)
- Clear PVC tubing (8mm ID x 10mm OD, 0.5m)

**Seals:**
- Solid nitrile rubber O-ring cord, 2mm cross section (3x)
- Loctite 206 adhesive for bonding O-ring cord ends

**General Assembly:**
- Various LEGO pieces (spec to be provided)
- Zip ties and elastic bands

**Electronics:**
- Mobile phone power bank
- Micro USB cable
- Pi Pico
- HC-05 Bluetooth Serial Transceiver (paired with Android phone and SerialConnector app)
- 3x DRV8833 1.5A 2-channel H-Bridge DC gear motor driver modules
- 6x Gebildet DC3V-12V prewired geared motors (double axis 1:48, for syringe and props)
- Custom soldered PCB

---


# Hull Construction

This section documents the construction of the hull, with images and descriptions for each step and component.

## Overview

The hull consists of a clear cylindrical tube and two custom-fabricated lids. The lids are designed to seal the ends of the tube and provide access for additional components.

### Components

- **Tube:** Transparent, forms the main body of the hull.
- **Lids:** Two square acrylic plates with circular cutouts and attached rings to fit inside the tube.
- **Valve:** One lid is fitted with a Schrader valve for pressure control.
- **Magnets:** A pair of small magnets are attached to one lid, intended for use in the propeller system. Their resistance to corrosion is being monitored.
- **Seals:** O-rings are used to ensure a watertight fit between the lids and the tube.

---

## Images

### Hull Tube and Lids

![Hull tube and lids overview](images/20260421_221231.jpg)
*The clear cylindrical tube and both lids. The lids are square acrylic plates with circular rings attached, designed to fit snugly inside the tube.*

### Lids Close-Up (No Seals)

![Lids close-up, no seals](images/20260421_221244.jpg)
*Close-up of the two lids. The right lid has a Schrader valve embedded for pressure control. A pair of small magnets are also visible, which are being considered for the propeller system. Their condition is monitored for corrosion due to exposure to water.*

### Lids Close-Up (No Seals, Top View)

![Lids close-up, top view](images/20260421_221253.jpg)
*Another angle showing the lids without seals. The Schrader valve and magnets are visible.*

### Lids with Seals

![Lids with seals](images/20260421_221459.jpg)
*Both lids fitted with O-ring seals, ready to be inserted into the tube for a watertight fit.*

---

## Waterproofing Approach

### V1 Method

- Primary seal: [TBC — original approach]
- Secondary: [TBC]
- Known weaknesses: seal reliability unconfirmed under pressure

### Updates During V1

- Nitrile glue ordered as replacement/improvement
- [Note any cable entry points and how they were sealed]

### What Was Not Done

- No pressure testing at depth
- No validated seal protocol

---

## Issues

### Flat Panel Lids — Cutting Difficulty

The flat acrylic panels were difficult to cut accurately. A hacksaw was used but proved hard work and incapable of cutting to a precise shape, so the lids were left in their roughly cut form rather than being trimmed to a cleaner finish.

The roughly cut acrylic edges were also sharp enough to cause injury during handling.

### Schrader Valve — Not Properly Sealed

The Schrader valve's intended role was to relieve excess pressure when pushing the lids on. Later its role expanded: the plan was to open the valve and pull the syringe all the way out, allowing excess air to escape, so that when the syringe was pushed back in, the vessel would be at low pressure. This would:
- (a) help keep the lids on, and
- (b) prevent increased internal pressure on the lids when submerged with the syringe extended.

However, the valve was not properly sealed. While it did not appear to let water in, it did allow gas to pass during syringe operation — a stream of bubbles was observed during testing when the syringe was being drawn out.

### Syringe Tube Hole — Worked Well

The hole in the same lid for the syringe tube performed surprisingly well, remaining sealed simply by the presence of the tube inserted through it. No additional sealing was needed.

### O-Ring Seals — Ongoing Point of Failure

Getting the seals right proved difficult throughout, and they remained a point of failure during testing, allowing water ingress. Key issues:

- **Thickness:** The gap between the inner and outer hull is 2mm — the difference between the inner diameter of the outer tube (104mm) and the outer diameter of the inner tube — so a slightly thicker seal was desired so it would compress to a tight fit when stretched. The closest available was 2.3mm cord, but stretching it far enough to lose 0.3mm of thickness proved too much for any adhesive tested. The 2mm cord was ultimately used, which felt snug but may not have provided sufficient compression.
- **Adhesive:** Loctite 206 was the clear winner for bonding the seal cord ends.
- **Alignment:** Gluing the seals straight around the lid was very difficult, and the joins are likely to have been points of failure.
- **Quantity:** Three O-rings were used per lid precisely because at 2mm thickness the contact surface area was small, meaning a single ring did not provide enough grip to keep the lid seated in the tube.

---

## Next Build — Hull Improvements

- [ ] **Lid cutting:** Use a laser cutter or CNC router to cut the flat acrylic panels accurately to shape, rather than a hacksaw. This would allow proper circular or hex profiles that fit the tube cleanly.
- [ ] **Acrylic edge safety:** Smooth or deburr all cut acrylic edges before handling and assembly. Wear gloves when handling freshly cut or rough acrylic parts.
- [ ] **Schrader valve sealing:** Properly seal the valve into the lid using thread sealant (e.g. PTFE tape + Loctite) or a rubber-backed nut on the reverse side. Pressure-test before assembly to confirm it holds gas.
- [ ] **Schrader valve alternative:** Consider replacing with a simple one-way check valve or a plug with a bleed hole that can be temporarily blocked with a finger — simpler and less likely to leak.
- [ ] **O-ring groove:** Machine or laser-cut a shallow groove into the lid at the correct diameter to locate the O-ring precisely and keep it straight during fitting, rather than relying on gluing cord freehand.
- [ ] **O-ring cord thickness:** The gap is a known 2mm (defined by the tube dimensions). Source 2.5mm or 3mm nitrile cord and test whether it can be stretched to fit without adhesive failure.
- [ ] **O-ring joins:** Experiment with vulcanising O-ring cord joins (heated tool method) rather than adhesive, which would produce a stronger, more uniform join with no raised bead.
- [ ] **Lid retention:** Investigate adding a positive locking mechanism (e.g. a twist-lock lip, a retaining ring, or a threaded end cap) so the lids are mechanically retained as well as sealed, removing reliance on O-ring friction alone.
- [ ] **Magnets:** Assess corrosion on the existing magnets after water exposure. If corroded, replace with coated or stainless-backed alternatives. Consider whether a magnetic coupling is the right approach for the propeller system or whether a shaft seal would be more reliable.
- [ ] **Pressure testing:** Before any water testing, perform a bench pressure/vacuum test on the sealed hull to confirm all seals hold — e.g. pressurise slightly and check for pressure loss over time, or submerge in a container and look for bubbles.
- [ ] **Waterproof testing:** Perform dedicated water-ingress tests on the assembled hull before fitting electronics or running open-water trials. Test progressively with longer submersion times and inspect the inside for any moisture after each test.

---

# Electronics

## Overview

The electronics assembly consists of three core components mounted on a custom-built LEGO frame, with a phone power bank providing power via USB:

| Component | Role |
|-----------|------|
| Raspberry Pi Pico | Microcontroller — all logic and motor control |
| HC-05 Bluetooth module (ZS-040) | Wireless communication, paired with Android phone via SerialConnector app |
| DRV8833 dual H-bridge motor driver | Drives up to 2 DC motors at up to 1.5A per channel |

All components were fitted with pin headers and sockets so that every module can be removed and reused independently without desoldering. This worked well in practice.

---

## Photo

![Electronics assembly — Pico, Bluetooth module and motor driver](images/20260422_121049.jpg)
*Electronics mounted inside the LEGO chassis. Left: Raspberry Pi Pico. Right (top): HC-05 Bluetooth module (ZS-040). Right (bottom): DRV8833 motor driver. A phone power bank is visible below, connected via USB.*

---

## Issues

### Manual PCB — Functional but Messy

A custom PCB was hand-soldered to connect the components. While it worked, the process was fiddly and the result was untidy. Reliability concerns remain around borderline solder joints, and any rework would be difficult.

### Bluetooth Does Not Work Underwater

Bluetooth signals do not penetrate water. As soon as the submarine submerged, the Bluetooth connection was immediately lost, rendering real-time remote control non-functional for the duration of a dive.

**Workaround applied:** The control logic was modified to operate autonomously — on command, the sub would dive, hold for 10 seconds, then resurface. This avoided the need for an active connection during submersion but significantly limited operational capability.

> **Scope note:** This constraint also shaped the effective scope of V1. Rather than a fully RC-controlled submarine, V1 became a platform for testing controlled submersion and resurfacing only. Full real-time RC control underwater requires a fundamentally different communication technology. See the [Project Overview](./README.md) for more on how this shaped V1's objectives.

### Motor Driver — Insufficient Channel Count

The DRV8833 provides 2 independent motor channels. Three were required:

| Motor axis | Role |
|------------|------|
| Ballast actuator | Drives the syringe piston to control buoyancy |
| Fore/aft thruster | Longitudinal propulsion |
| Lateral thruster | Transverse (side-to-side) propulsion |

Only two of the three axes could be driven at once with the hardware fitted, limiting manoeuvring capability.

### Battery — Not Fit for Purpose

The mobile phone power bank was available and convenient but is not appropriate for this application:

- Power banks automatically cut output at low current draw (interpreting it as the device being fully charged), causing unexpected resets during low-power operation.
- Capacity, discharge rate, and voltage regulation are optimised for phone charging, not motor drive loads.
- No power budget was established before the build, so actual requirements were unknown.

Battery selection needs to be properly revisited for V2.

### Motor Capability — Unknown

No datasheet was available for the Gebildet DC geared motors. Stall current, no-load current, torque, and rated speed were all unknown going into the build. As a result:

- PWM duty cycles and drive parameters were effectively guesses.
- The motors may have been running well outside their optimal operating range.
- Power draw and efficiency are uncharacterised; the risk of motor or driver damage from over-driving is non-trivial.

---

## Next Build — Electronics Improvements

- [ ] **PCB design:** Replace the hand-soldered PCB with a properly designed board. Use a PCB design tool (e.g. KiCad) to plan the layout before committing. At minimum, use well-laid-out stripboard with a clear schematic.
- [ ] **Communication technology:** Replace Bluetooth with an underwater-capable alternative. Acoustic communication is the established method for underwater vehicles; for short-range, shallow-water use, a wired tether is the simplest reliable interim option.
- [ ] **Motor driver channel count:** Use a driver combination supporting at least 3 independent channels (e.g. two DRV8833 modules, or a single board with 3+ channels).
- [ ] **Power budget:** Before selecting a battery, measure current draw of all motors under representative load using a bench supply and multimeter. Sum the draw, add margin, and use this to specify battery capacity and continuous discharge rating.
- [ ] **Battery selection:** Based on the power budget, select an appropriate LiPo or similar battery. Confirm it can deliver sufficient peak current without triggering a low-current cutoff. Add a low-voltage alarm or cutoff to protect the pack.
- [ ] **Motor characterisation:** Source datasheets or, if unavailable, characterise the motors on the bench — measure no-load current, stall current, and approximate torque at operating voltage. Use this to set appropriate drive parameters and confirm the motor driver stays within its rated limits.
- [ ] **Wiring tidiness:** Document and label all connections. Use consistent wire colours and lengths. Ensure all connectors are mechanically retained and will not vibrate loose during operation.

---

# Annex / Notes

---

## Power System

| Parameter | Value |
|-----------|-------|
| Battery type | Mobile phone power bank |
| Capacity | 500mAh |
| Voltage | 5V (USB output) |
| Estimated runtime | [TBC — not measured] |
| Charging method | Standard USB recharge |
| Low-power measures | None (see notes) |

**Notes:**
- Power supplied via USB from a mobile phone power bank for ease of use and recharging.
- The Pi Pico and all electronics powered from USB 5V.
- **Issue:** If the unit was drawing very little current (e.g., idle or only Pico running), the power bank would automatically switch off, likely assuming the "phone" was fully charged. This caused unexpected shutdowns during low-power operation.
- No additional low-voltage cutoff or protection circuitry was used.
- Power draw from motors vs. electronics was not profiled; runtime not measured.
