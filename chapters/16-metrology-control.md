# Chapter 16: Metrology & Process Control

## Overview

Advanced process nodes demand real-time monitoring and feedback control. This chapter covers endpoint detection, in-situ diagnostics, ex-situ characterization, and closed-loop recipe adaptation for production contact-hole etch.

---

## 16.1 Endpoint Detection (OES)

```
Optical Emission Spectroscopy (OES) principle:

Plasma emits photons (light) during radical reactions
Different species emit at characteristic wavelengths
Monitor intensity to track etch progress

Detection wavelengths (Cl₂ etch):

Species          | Wavelength (nm) | Intensity trend during etch
-----------------|-----------------|---------------------------
Cl (atomic)      | 725.7           | High initially, drops at endpoint
Cl₂ (molecular)  | 290-300         | Moderate, stable
WCl (product)    | 380-390         | Rises during etch, drops at endpoint
O (additive)     | 777.0           | Tracks O₂ consumption
SiO₂ (dielectric)| 390-410 (weak)  | Minimal signal (SiO₂ not easily ionized)

Endpoint detection strategy:

Step 3 (selective finish, 60 sec etch through oxide):

Time (sec) | Cl @ 726nm | WCl @ 385nm | Interpretation
-----------|------------|------------|------------------------
0          | 100        | 10         | Start (W being etched)
15         | 95         | 25         | W depletion accelerating
30         | 85         | 40         | Still in W layer
45         | 75         | 50         | Approaching SiO₂ interface
57         | 60         | 60         | Near endpoint (W nearly gone)
58         | 50         | 65         | Endpoint detected! (Cl emission drops)
59         | 45         | 50         | SiO₂ now exposed (weak signal)
60         | 40         | 30         | SiO₂ dominated

Endpoint trigger:

OES intensity ratio: I_Cl(726nm) / I_Cl(initial) drops to 50%
→ Triggers endpoint signal
→ Bias power reduced to 0 (stop etch)
Total etch time: 58 sec (vs. preset 60 sec)
Margin: +2 sec conservative (safety factor)

Accuracy:

With good tuning: ±2 sec endpoint detection (3% of 60 sec)
Reduces over-etch risk to <1 nm SiO₂ penetration
Without OES (preset time only): ±10 sec uncertainty (±5 nm SiO₂ damage possible)
Value: OES prevents 80% of over-etch failures

Challenges:

1. Line-of-sight requirement:
   OES probe must "see" plasma (direct optical path)
   Chamber geometry can block some emissions
   Side-viewing windows common (cost $5-10K each)

2. Repeatability:
   Cl intensity varies with pressure, power, temperature
   Need calibration per recipe step
   Drift over time (optical window fouling)
   Daily calibration recommended

3. False signals:
   Electrode corrosion can emit similar wavelengths
   Contamination in chamber raises background noise
   High-K dielectrics may have unexpected emissions
```

---

## 16.2 In-Situ Monitoring

```
Real-time process parameter tracking:

RF forward/reflected power:

Sensor: Power meter on RF transmission line
Measurement: P_forward vs. P_reflected (both real-time)

Interpretation:

Impedance matching:
  P_reflected / P_forward = impedance mismatch
  High mismatch (>20%) → tune matching network
  Low mismatch (<5%) → optimal plasma coupling

Plasma density tracking:
  Reflected power increases with plasma density
  High P_ref relative to P_fwd → plasma non-linear
  Can indicate electrode contamination (increased arcing)

Example during etch:

Time | P_fwd | P_ref | P_net  | Interpretation
-----|-------|-------|--------|----------------------------------
0    | 1000  | 50    | 950    | Start (good match)
20   | 1000  | 70    | 930    | W etch (slight impedance change)
40   | 1000  | 120   | 880    | SiO₂ starting (dielectric mismatch)
58   | 800   | 100   | 700    | Endpoint (power reduced)

Pressure/temperature monitoring:

Pressure gauge:
  Target: 30-50 mTorr for contact etch
  Tolerance: ±2 mTorr (tight control)
  Feedback: Adjust MFC to maintain setpoint
  Cost: $2K sensor, real-time control critical

Temperature sensor:
  Substrate back-side pyrometer or thermocouple
  Target: 30-40°C (if cooling active)
  Tolerance: ±5°C (selectivity margin)
  Feedback: Adjust He flow or chiller power
  Cost: $5-10K sensor + controller

Mass flow controller (MFC) feedback:

Each gas has dedicated MFC
Reads flow in real-time, compares to setpoint
Corrects for supply pressure variation
Maintains recipe gas ratio ±1% (critical for uniformity)

Cost: $2-5K per MFC (3 gases = $6-15K total)
Value: Prevents recipe drift (recipe change = loss of 4-8 wafers during re-tune)
```

---

## 16.3 Ex-Situ Characterization

```
Post-etch wafer analysis (sampling: 1-2 wafers per 50-100 wafer lot):

Scanning Electron Microscopy (SEM):

High-resolution cross-section imaging:
  Magnification: 5,000-100,000×
  Resolution: <5 nm
  Measures: Profile (scalloping, undercut), residue, corner rounding

Per-wafer cost: $500-1000 (labor + equipment time)
Typical measurements: 5 via profiles (center, edge, corners)
Yield: Pass if all criteria met (no residue >3 nm, scallop <20 nm, etc.)

Transmission Line Model (TLM):

Measures specific contact resistivity (ρ_c):
  TLM pattern: 5-7 contact pairs at different spacings
  Pass current through contact pairs
  Plot resistance vs. spacing (linear relationship)
  Extrapolate: ρ_c = (slope × area) / 1

Target: ρ_c < 1 Ω·µm² (normal), > 1 OK but risky
Specification: 0.3-0.8 Ω·µm² (typical production)
Failure: > 5 Ω·µm² → scrap (open circuit risk)

Per-wafer cost: $200-300
Cycle time: 1-2 days (lab analysis)

Four-point probe sheet resistance:

Measures oxide thickness and dielectric properties
Rapid non-destructive screening
Cost: $50-100 per wafer
Value: Quality gate before more detailed analysis

Leakage current measurement:

Contact pad to adjacent metal
Measure current at specified voltage (1.5-3V typical)
Specification: <100 pA/contact (normal), >1 nA scrap

Equipment: Parameter analyzer ($50-100K)
Cost per wafer: $100-200
Cycle time: <1 hour (fast feedback)
```

---

## 16.4 Closed-Loop Process Control

```
Feedback control loop for in-situ optimization:

Target metric: Final via width + depth measurement (via CD and etch depth)

Measurement frequency: Every 1-2 hours (5-10 wafers sampled)

Feedback control algorithm:

1. Measure wafer: SEM image processed via image analysis
   Extract: CD (contact diameter), depth, scallop amplitude
   
2. Compare to target:
   Target CD: 50 nm ±3 nm
   Target depth: 500 nm ±5 nm
   Target scallop: <15 nm amplitude
   
3. Calculate deviation:
   ΔCD = Measured_CD − Target_CD
   ΔDepth = Measured_depth − Target_depth
   Δ_scallop = Measured_scallop − Target_scallop
   
4. Adjust recipe if needed:
   If ΔCD > 2 nm (over-etched):
     → Lower Step 3 power by 50 W (reduce etch rate)
     OR → Reduce Step 3 time by 5 sec
     
   If ΔDepth < 3 nm (under-etched):
     → Increase Step 2 time by 5 sec (more etch)
     OR → Increase Step 1 power by 100 W (more bulk)
     
   If Δ_scallop > 5 nm (rougher):
     → Enable pulsed plasma (50% duty, 5 sec ON/OFF)

5. Re-run test wafers with new recipe:
   Monitor convergence toward target
   Typical: 3-5 wafers to dial-in new condition
   Cost: $0.50-1.00 per wafer development (worth it!)

Feedback frequency:

High-volume production:
  Measure every 100 wafers (1-2 hours typical)
  Adjust recipe every 1000 wafers (~4-hour interval)
  Prevents drift from tool degradation

Advanced control (statistical):

Track 50-wafer moving average of critical dimension
Apply EWMA (exponentially weighted moving average) filter
Detect trends before they cause yield loss
Implement corrective action proactively (vs. reactively)

Cost: $50-100K for automated SEM + control software
Value: Prevents 2-3% yield loss from undetected drift
ROI: Typically <1 year in high-volume fab
```

---

## 16.5 Recipe Adaptation Strategies

```
Production recipe database:

Organization:

Node_technology / Material_stack / Feature_AR /

Example:
  7nm_logic / W_contact / 50:1_AR / baseline_recipe.txt
  5nm_logic / Cu_interconnect / 8:1_AR / high_selectivity_variant.txt
  3D_NAND / W_via / 100:1_AR / aggressive_ARDE_compensation.txt

Key recipe variations by scenario:

Scenario 1: New node qualification (first wafers)

Use conservative recipe:
  Low power (minimize damage risk)
  High selectivity (minimize over-etch)
  Longer etch time (accept slower throughput)
  
Example settings (conservative):
  Step 1: 1500 W coil, 800 W bias (vs. 2000/1500 aggressive)
  Step 3: 600 W coil, 200 W bias, +20 sec time (vs. 800/300/60 baseline)
  
Margin: Large selectivity window, minimal over-etch risk
Cost: ~15% slower throughput
Value: First 10-20 wafers often scrap anyway; conservative recovers 50-70%

Scenario 2: Thermal drift (summer vs. winter chamber)

Summer operation (higher ambient T):
  Subtract 10 W from each step bias power
  Reduce Step 3 time by 5 sec (substrate hotter anyway)
  Adjust: Compensate for natural thermal elevation
  
Winter operation:
  Add 10 W to each step bias power
  Add 5 sec to Step 3 time (substrate colder)

Cost: Simple power/time adjustment, 5-min recipe edit
Value: Prevents 3-5 wafer scrap from seasonal drift
ROI: Trivial (mostly automated in production)

Scenario 3: Electrode degradation (after 40K wafers)

Electrode aging reduces coupling efficiency:
  Plasma density drops ~10%
  Etch rate drops ~8%
  Selectivity drops ~5% (worse efficiency)
  
Adaptation:
  Increase coil power +100 W (restore plasma density)
  Increase bias power +100 W (restore etch rate)
  Increase Step 3 O₂ additive from 2% → 3% (restore selectivity)
  
Cost: 15-min power/gas adjustment
Value: Extends electrode life by ~5-10% (1,000-2,000 extra wafers)
ROI: High (avoids $7K electrode replacement 1000-2000 wafers early)

Scenario 4: Contamination event (moisture in chamber)

If RGA detects H₂O > 1 mTorr:
  Chamber leak or moisture ingress
  
Response:
  Stop production immediately (yield risk)
  Pump down to <0.1 mTorr (remove moisture)
  Run bake-out: 100°C × 2 hours (drive off H₂O)
  Run dummy wafers (sacrifice 5 wafers to recondition)
  Resume production
  
Cost: 2-3 hour downtime, 5 wafers scrap, $2-5K impact
Value: Prevents 100% yield loss (100+ wafers at risk if continued)
ROI: Essential (non-negotiable)

Recipe versioning:

Maintain version control:
  v1.0: Baseline (first qualification)
  v1.1: Summer thermal offset applied
  v1.2: After 40K wafers, electrode aging compensation
  v2.0: Major revision after 3 months (customer feedback + yield data)
  
Track:
  Which wafers ran which recipe version
  Yield per recipe version
  SEM/electrical data per version
  Enable process improvement over time
```

---

## 16.6 Summary & Key Takeaways

1. **OES Endpoint ±2 sec Accuracy** — Cl intensity drop at 50% detects W→SiO₂ transition; stops over-etch (<1 nm SiO₂ damage); vs. preset time ±10 sec (risky); prevents 80% over-etch failures.

2. **In-Situ Monitoring Real-Time** — RF power/impedance, pressure, temperature, MFC feedback; detect drift before yield loss; cost $15-40K sensors/controllers; enables adaptive power tuning.

3. **SEM Characterization $500-1000/Wafer** — Cross-section profile (scalloping, undercut), residue thickness, corner rounding; 1-2 wafers per 50-100 sampled; high-resolution yield gate.

4. **TLM Measures Contact Resistivity** — ρ_c <1 Ω·µm² target (0.3-0.8 typical); >5 scrap; feedback on damage/residue/oxidation; cost $200-300, 1-2 day turnaround.

5. **Leakage <100 pA Specification** — Parameter analyzer measures contact-to-adjacent-metal current; rapid screening (<1 hour); detects D_it increase or breakdown risk.

6. **Closed-Loop Feedback Every 1-2 Hours** — Sample 5-10 wafers, measure CD/depth, adjust recipe (power/time/gas); typical convergence 3-5 wafers; prevents drift; ROI <1 year high-volume.

7. **Recipe Adaptation Scenarios** — Conservative for qualification (low risk), thermal offsets (seasonal), electrode aging (extend life), contamination (prevent catastrophic loss); versioning critical for traceability.

---

**End of Part IV: Production Scale (Chapters 15-16) COMPLETE**

**Chapter 16 Development Status:** Complete metrology and process control framework  
**Version:** 1.0

