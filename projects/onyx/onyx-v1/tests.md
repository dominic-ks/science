# Onyx V1 — Submersion Testing Record

This file records the water tests performed during V1 and the observations that should carry forward into V2.

Unlike the build notes, this is not a component-by-component design record. It is a practical test history: what was put in the water, what happened, and what that means for the next stage.

---

## Summary

The V1 submersion tests confirmed that the submarine could be assembled, sealed, placed in water, and actuated, but not with enough reliability or stability to continue developing V1 as a full RC vehicle.

The main outcomes were:

- Bluetooth control is not viable for live submerged RC with the V1 hardware; the connection is lost as soon as the unit submerges.
- This did not invalidate the V1 submersion tests because the firmware could command an autonomous dive, wait 10 seconds, and resurface without maintaining a link.
- The hull seal is not reliable enough for electronics-first testing.
- The Schrader valve did not seal gas properly during syringe operation.
- The syringe ballast mechanism itself was mechanically promising.
- Ballast distribution and internal layout produced poor balance.
- T3 measured hull-only displacement at approximately 2,460 cm³, close to the 2,376 cm³ nominal prediction, but water ingress around the valve was still observed.

V1 should therefore not be used for further live RC-control development in its current hardware configuration. It can still be used as a controlled physical measurement platform before V2, especially for buoyancy, density, ballast, centre-of-mass, and syringe-actuation questions.

---

## Test Record

### T1 — Initial Powered Submersion

![The Onyx during the first submersion test](images/image.png)
*The Onyx shortly after being placed in the water for the first time. You can see the heavy listing, which was largely due to difficulty distributing the ballast effectively as a result of generally cramped conditions on board.*

**Date:** [08/04/2026, 17:50 BST]

**Goal:**
Confirm whether the assembled submarine could be controlled while submerged.

**Setup:**
- Full V1 hull assembled with internal chassis installed.
- Pi Pico, HC-05 Bluetooth module, motor driver, power bank, ballast syringe, and lead shot ballast fitted.
- Control attempted from an Android phone using the SerialConnector app.

**Result:**
Although the syringe ballast could be actuated, the submarine did not dive below the surface.

**Observations:**
- The electronics and syringe actuator worked well.
- The submarine was listing heavily in the water.
- The syringe appeared around half full of air due to drawing it from the tube, it is still assumed that 40ml of water was successfully onboard, though this was not measured.
- The submarine was observed to be taking on water, which may have been due to the hull seal, the Schrader valve, or both.

**Conclusion:**
The definitive reason that the submarine did not submerge is not known, but the most likely cause is that the ballast was insufficient to overcome the buoyancy of the hull and internal components. The listing suggests that the ballast was also unevenly distributed, which would have made it harder to submerge.

**Issues to Carry Forward:**
- Must ensure ballast is sufficient to submerge the hull with all internal components installed.
- Must design the internal layout to allow for even ballast distribution.

---

### T2 — Autonomous Dive / Resurface Attempt

**Date:** [22/04/2026, 18:30 BST]

**Goal:**
To repeat the submersion test with the ballast more evenly distributed. 

**Setup:**
- As per test T1, but with the lead shot ballast distributed more evenly across the hull.

**Result:**
There was still some listing, but considerably less than T1, however, there was no improvement in the submarine's ability to submerge.

**Observations:**
- The submarine was more balanced than in T1, but still not level.
- The submarine did not submerge at all, even with the ballast syringe fully actuated.
- The submarine was observed to be taking on water, which may have been due to the hull seal, the Schrader valve, or both.
- The Schrader valve was observed to be leaking air when the syringe was actuated.

**Conclusion:**
The most likely reason that the submarine did not submerge is that the ballast was still insufficient to overcome the buoyancy of the hull and internal components. The listing suggests that the ballast was still unevenly distributed, which would have made it harder to submerge. The leaking Schrader valve may also have reduced the effective ballast.

**Issues to Carry Forward:**
- Must ensure ballast is sufficient to submerge the hull with all internal components installed.
- Must design the internal layout to allow for even ballast distribution.
- Must find a more reliable method of sealing the ballast water inside the hull, as the Schrader valve is not sufficient.

---

### T3 — Hull-Only Ballast Validation

**Date:** [21/06/2026]

**Goal:**
Validate the displacement and ballast calculations using the sealed hull only, before reintroducing the internal chassis, electronics, motors, syringe, or power system.

**Source:**
Completed field sheet: [t3-field-sheet_completed.pdf](./t3-field-sheet_completed.pdf)

#### Pre-Test Calculation and Measured Setup

The original estimate used the nominal hull dimensions and assumed material density. The completed test substituted the measured empty hull mass.

| Parameter | Value | Notes |
|-----------|-------|-------|
| Hull OD | 110 mm | From build spec |
| Hull ID | 104 mm | From build spec |
| Hull length | 250 mm | From build spec |
| Lid thickness | 3 mm | From build spec |
| Acrylic density | 1.18 g/cm³ | Standard extruded clear acrylic |
| Water density (fresh) | 1.00 g/cm³ | Tap water approximation |
| Measured empty hull mass | 455 g | Scale accuracy noted as questionable |
| Recalculated ballast target | 1,921 g | 2,376 g − 455 g |
| Phase 1 start mass | 1,421 g | Target − 500 g |

**Displaced volume (outer cylinder only, not accounting for lid overhangs):**

V_displaced = π × (55 mm)² × 250 mm = **2,376 cm³**

This is the volume of water pushed aside — and therefore the maximum mass the hull can carry before sinking.

**Setup:**
- Empty V1 hull assembled with both lids installed.
- Internal chassis, electronics, motors, syringe, and power bank removed.
- Syringe tube hole blocked with Blu Tack.
- Known ballast masses added progressively and distributed evenly along the hull length.
- Test container water dimensions recorded as approximately 33 cm deep, 66 cm long, and 59 cm wide.

**Result:**
The hull transitioned from near-waterline float to sinking between **2,004 g and 2,005 g** of added ballast. The final 2,005 g sink mass was rechecked.

Measured total mass at first clear sink:

455 g hull + 2,005 g ballast = **2,460 g**

At 1.00 g/cm³ water density, this implies a measured displaced volume of approximately **2,460 cm³**, which is **84 cm³ higher** than the 2,376 cm³ nominal calculation.

This is within the original ±100 g tolerance, so the displacement calculation is close enough for T4 planning. The result also shows that the hull-only neutral ballast requirement is higher than the measured-mass estimate by about 84 g.

**Recorded Test Steps:**

Float state key: **F** = floats clearly / **N** = near waterline / **S** = sinks

Tilt key: **L** = level

| Step | Total ballast (g) | Float | Tilt | Notes |
|------|-------------------|-------|------|-------|
| 1.1 | 1,421 | F | L | Slight tilt; sits quite low |
| 1.2 | 1,671 | F | L | Low; water clearly entering around valve |
| 1.3 | 1,921 | N | L | Very low |
| 2.1 | 1,971 | F | L | |
| 2.2 | 2,021 | S | L | |
| 3.1 | 1,981 | F | L | |
| 3.2 | 1,991 | F | L | |
| 3.3 | 2,001 | F | L | |
| 3.4 | 2,011 | S | L | Tiny bit at the bottom |
| 4.1 | 2,002 | N | L | |
| 4.2 | 2,003 | N | L | |
| 4.3 | 2,004 | N | L | Recorded as last mass that floated, despite near-waterline state |
| 4.4 | 2,005 | S | L | Final sink mass, rechecked |

**Observations:**
- All pre-requisites were checked before testing.
- The syringe hole was blocked with Blu Tack.
- Water was clearly entering around the valve by step 1.2.
- The scale accuracy is questionable; it was sometimes skipping 2 g at a time.
- The final ballast mass was rechecked at 2,005 g.

**Conclusion:**
The hull-only buoyancy calculation is trustworthy enough to use as a T4 baseline, with measured displacement taken as **approximately 2,460 cm³** rather than the nominal 2,376 cm³.

For future tests, use the measured displacement as the mass budget:

m_fixed_ballast = 2,460 g − installed dry vessel mass − desired syringe margin

If the syringe can reliably admit about 60 ml of water, the fixed-ballast target should leave roughly a 60 g positive-buoyancy margin before syringe intake. Using the hull-only test as a simple reference, that would put the hull near sinking at about 2,005 g of fixed ballast and near syringe-controlled transition at about 1,945 g of fixed ballast.

The sealing result did not pass: water ingress around the valve was observed. The valve or blocked syringe-hole area must be treated as unresolved before any electronics-installed water test.

**Addendum — Displacement Model Correction:**
After reviewing the T3 result, the main source of the prediction error was identified as the external lid geometry. The original displacement estimate treated the hull as the main 110 mm diameter, 250 mm long cylinder only. The actual hull includes two external square acrylic lid plates, each approximately 13 cm × 13 cm × 3 mm, which add displaced volume.

| Item | Old assumption | Corrected assumption | Measured / observed |
|------|----------------|----------------------|---------------------|
| Main tube displaced volume | 2,376 cm³ | 2,376 cm³ | Same |
| External lid displaced volume | 0 cm³ | ~101 cm³ | 2 × 13 cm × 13 cm × 0.3 cm |
| Total predicted displacement | 2,376 cm³ | ~2,477 cm³ | ~2,460 cm³ |
| Difference from measured displacement | +84 cm³ measured vs old | -17 cm³ measured vs corrected | Within test uncertainty |

One of the lid plates is not a full square because a corner is cut off. That missing corner likely explains much of the remaining ~17 cm³ difference between the corrected square-lid estimate and the measured displacement.

| Item | Old mass model | Corrected mass model | Measured |
|------|----------------|----------------------|----------|
| Tube wall material mass | ~298 g | ~298 g | |
| Lid plate material mass | ~67 g, based on circular plates | ~120 g, based on square plates | |
| Rings, O-rings, valve, magnets allowance | ~40 g | ~40 g | |
| Predicted empty hull mass | ~405 g | ~458 g | 455 g |

| Item | Old prediction | Corrected prediction | Measured |
|------|----------------|----------------------|----------|
| Predicted displacement | 2,376 g water | ~2,477 g water | ~2,460 g water |
| Predicted hull mass | ~405 g | ~458 g | 455 g |
| Predicted ballast to sink | ~1,971 g | ~2,019 g | 2,005 g |
| Error vs measured sink ballast | +34 g measured vs old | -14 g measured vs corrected | |

Conclusion: the T3 result is consistent with the physical geometry once the square external lids are included. The corrected model is close enough for ballast planning; remaining differences are plausibly due to scale behaviour, rounded or rough lid edges, valve and Blu Tack geometry, and judgement around the near-waterline-to-sink transition.

---

### T4 — Chassis-Installed Buoyancy and Trim Reassessment

**Date:** [Planned]

**Goal:**
Reassess V1 buoyancy and trim with the internal chassis and electronics installed, using the T3 hull-only result as the baseline. Confirm the dry mass, the mass after water is taken on by the syringe, and whether syringe actuation produces a useful submerge/resurface effect.

**Setup:**
- V1 hull assembled with internal chassis and electronics reinstalled.
- Ballast actuator and syringe fitted.
- Aft motors removed only if they block useful ballast placement.
- Ballast distributed progressively, using any freed aft space to improve centre-of-mass placement.

**Measurements to Record:**
- Dry installed vessel mass before syringe intake.
- Installed vessel mass after syringe intake.
- Actual onboard water mass, calculated from the difference between dry and post-intake mass.
- Estimated hull displacement.
- Recalculated effective density before and after syringe intake.
- Added ballast mass and position.
- Centre-of-mass / trim observations.
- Syringe state and actuation direction.
- Observed float state, submersion behaviour, resurfacing behaviour, leaks, bubbles, or mechanical binding.

**Pass Condition:**
The vessel can be trimmed predictably, and any remaining ballast or syringe shortfall is measurable rather than guessed.

**Out of Scope:**
- Propulsion testing.
- Live-control communication testing.
- Real-time RC control.

**Decision to Make After Test:**
Whether the V1 hull/chassis combination can achieve neutral or negative buoyancy with practical ballast placement, and what ballast volume or layout changes V2 must allow for.

---

## V2 Test Protocol

Use this progression for V2 testing:

1. Empty hull dry assembly check.
2. Empty hull pressure or vacuum seal test.
3. Empty hull static submersion test.
4. Unpowered buoyancy test with ballast only.
5. Ballast mechanism bench test.
6. Ballast mechanism wet test without control electronics.
7. Powered dry integration test.
8. Powered shallow-water test.
9. Communication test underwater.
10. Propulsion test only after sealing, buoyancy, and ballast are stable.

Each test entry should record:

- Date.
- Goal.
- Exact hardware configuration.
- Environment, depth, and duration.
- Whether electronics were installed and powered.
- Observed leaks, bubbles, tilt, resets, signal loss, or mechanical binding.
- Decision made after the test.
