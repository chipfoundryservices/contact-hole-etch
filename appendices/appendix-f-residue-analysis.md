# Appendix F: Residue Formation & Analysis Procedures

Detailed characterization methods for post-etch residue, failure modes, and SEM/EDS analysis standards.

---

## F.1 Residue Formation Mechanisms

```
Formation process during etch:

Phase 1 (Active W etch, 0-50% of etch time):

Cl• + W → WCl₂, WCl₃, ... WCl₆ (gas phase production)
Most products escape as gas
Some WCl₂/WCl₃ condense on cooler surfaces (sidewalls, floor)
Typical deposition rate: <1 nm per minute
Volume: Mainly escapes (~95%)

Phase 2 (Transition, 50-90% of etch time):

Still etching W (bulk going down)
Competing reactions:
  - Remaining W continues producing WCl_x
  - SiO₂ surface now approaching (but protected by O₂ if present)
  
Residue accumulation accelerates (~2 nm/min)
Some WCl₂ deposited earlier oxidizes slightly (WOCl_x intermediate)

Phase 3 (SiO₂ exposure, 90-100% of etch time):

W fully consumed
SiO₂ now in contact with Cl•
New byproducts:
  - SiCl₂, SiCl₃ (from SiO₂ + Cl•)
  - WOCl₂, WOCl₃ (oxidized tungsten residue)
  - Possible WO₃ (if O₂ additive present)
  
Residue rate changes (depends on SiO₂ selectivity)

Post-etch residue thickness:

W etch: Typical 1-10 nm deposited
  (Depends on pressure, additives, dielectric distance)
Cu etch: Higher, 3-20 nm (more non-volatile chlorides)
TaN etch: Moderate, 1-8 nm (TaCl₅ semi-volatile)
```

---

## F.2 SEM Characterization Standards

```
Sample preparation:

1. Cross-section preparation:
   - Wafer cleaved or cored (for TEM sample area)
   - Argon ion milling or mechanical polishing
   - Final polish: <0.1 µm roughness (ultra-smooth)
   - Light C coating (5 nm, for conductivity)

2. Setup:
   - SEM: FEI Helios or JEOL equivalent
   - Acceleration voltage: 5-15 kV (trade-off: resolution vs. charging)
   - Working distance: 4-5 mm (standard for EDS)
   - Chamber vacuum: <1e-6 Torr

Measurement locations (300mm wafer):

Standard sampling: 5 locations minimum

Location      | Position              | Reason
--------------|----------------------|----------------------------------
1             | Center (wafer center)| Baseline, plasma-coupled region
2             | Inner edge (150mm R) | Transition region
3             | Edge (145mm from center) | Edge plasma effects
4, 5          | Quadrants at 150mm R | Azimuthal variation check

SEM imaging settings:

Parameter           | Value/Range      | Purpose
--------------------|------------------|----
Magnification       | 10,000-50,000×   | Profile details, residue thickness
Tilt angle          | 45-52°            | Cross-section view (maximize depth info)
Brightness/contrast | Auto-level        | Standardize image intensity
Scan direction      | Horizontal        | Minimize charging artifacts
Frame averaging     | 8-16 frames       | Noise reduction for measurements
```

---

## F.3 Residue Thickness Measurement (SEM)

```
Measurement procedure:

1. Identify W/SiO₂ interface:
   - W appears bright (high Z, tungsten ~74)
   - SiO₂ appears dim (low Z, silicon ~14)
   - Interface sharp (W etched cleanly) or blurred (residue/oxidation)

2. Measure residue layer:
   - Light-colored layer on top of Si: Residue (WCl₂ etc.)
   - If visible: Measure thickness directly (caliper tool in SEM software)
   - If not visible: Use EDS to confirm composition

3. Record measurements:
   - Top residue thickness (floor of via)
   - Sidewall residue thickness (contact walls)
   - Corner residue thickness (via corners)
   - Record at each location

4. Statistical analysis:
   - Calculate mean, std dev, min, max
   - Residue spec: <3 nm acceptable, >5 nm fail

Example measurement report:

Location | Top (nm) | Sidewall (nm) | Corner (nm) | Category
---------|----------|---------------|------------|----------
Center   | 1.5      | 2.0           | 2.5        | Good
IR       | 2.0      | 2.5           | 3.0        | Good
Edge     | 2.5      | 3.0           | 3.5        | Marginal
Quad1    | 1.8      | 2.2           | 2.8        | Good
Quad2    | 2.1      | 2.6           | 3.2        | Good
─────────|----------|---------------|------------|----------
Average  | 2.0      | 2.5           | 3.0        | PASS (all <3.5nm)
```

---

## F.4 EDS (Energy Dispersive Spectroscopy) Analysis

```
EDS principle:

X-ray fluorescence when SEM e-beam strikes sample
Element-specific X-ray energies
Count rates → elemental composition

Setup:

Detector: Silicon drift detector (SDD), 130 eV resolution
Live time: 30-60 seconds (accumulate sufficient counts)
X-ray intensity: Related to elemental concentration (qualitative)

Residue composition analysis:

Typical residue (W etch with 2% O₂):

Element | X-ray (keV) | Expected source | Relative intensity
--------|-------------|-----------------|-------------------
Si      | 1.74        | Substrate       | Very high
O       | 0.53        | Oxide + oxidized residue | High
W       | 8.4 (Kα)    | Residual tungsten | Moderate (1-5%)
Cl      | 2.62        | Chlorine residue | Low-moderate
C       | 0.28        | Contamination   | Low

Point analysis:

Select 5 points across residue layer
Measure composition at each point
Plot depth profile (if residue layered)

Example result:

Point 1 (top surface): W 2%, Cl 3%, O 10%, Si 85%
  Interpretation: Oxidized residue (WOCl_x) with substrate showing
  
Point 2 (mid-residue): W 8%, Cl 8%, O 5%, Si 79%
  Interpretation: WCl₂ dominated layer
  
Point 3 (residue-substrate interface): W 2%, Cl 1%, O 0.5%, Si 96.5%
  Interpretation: Mostly substrate, residue <0.1 nm at interface

Line scan:

Draw line across residue → composition vs. position
Shows layer structure and thickness
Standard for quality control
```

---

## F.5 XPS (X-ray Photoelectron Spectroscopy) - Optional

```
More sensitive than EDS, but destructive:

Principle:

X-ray photon ejects core electrons
Electron kinetic energy determined by element + orbital
Binding energy = photon energy - kinetic energy
Highly element-specific and chemically-sensitive

Capabilities:

- Elemental composition (0.1-10 nm depth)
- Chemical state identification (e.g., W vs. WO₃ vs. WCl₂)
- Oxidation state analysis (W⁴⁺ vs. W⁶⁺)
- Depth profiling (layer-by-layer analysis)

Typical residue analysis:

Measurement mode: Survey scan (all elements)
Then high-resolution scans: W 4f, Cl 2p, O 1s

W residue chemistry:

W 4f peak at 31.4 eV: Metallic W (rare in residue)
W 4f peak at 32.8 eV: W⁴⁺ (WCl₂, WOCl)
W 4f peak at 34.5 eV: W⁶⁺ (WO₃)

Post-ashing residue signature:

After O₂ ashing: W oxidizes (W⁴⁺ → W⁶⁺ dominant)
O 1s high intensity (mostly oxide)
Cl drops dramatically (chlorine volatilizes)

Production use:

Not routine (cost $500-1000 per wafer, slow)
Used for root-cause analysis
E.g., "Why is residue thickness high after ashing?"
Answer: XPS shows chlorine still present (ashing incomplete)
```

---

## F.6 Residue Removal Efficiency Standards

```
Before/after ashing comparison:

Sample 1 (Pure Cl₂, no additive):

Before ashing: 8-12 nm residue (WCl₂ heavy)
SEM measurement: 10 nm average
EDS: W 5%, Cl 8%, O 2%

After 60 sec O₂ ashing at 80°C:

SEM measurement: 0.8 nm residue (barely visible)
EDS: W 0.5%, Cl <0.2%, O 8%
Removal efficiency: (10 - 0.8) / 10 = 92%

Sample 2 (Cl₂ + 3% O₂):

Before ashing: 1-3 nm residue (lighter, pre-oxidized)
After 30 sec ashing:
SEM: <0.5 nm (not measurable)
Removal: >95% (essentially complete)

Specification:

Residue after ashing: <1 nm acceptable
Removal efficiency: >90% required

Failure modes:

Residue >3 nm after ashing:
  Cause 1: Incomplete ashing (insufficient time/temperature)
  Cause 2: Over-thick residue from etch (>20 nm before)
  Cause 3: Ashing gas contamination
  Fix: Increase ashing time +30 sec, check gas

Residue >5 nm before ashing:
  Cause 1: High pressure during etch (>80 mTorr)
  Cause 2: Insufficient selectivity (ate into oxide, generated secondary WCl)
  Cause 3: Temperature too high (sidewall deposition)
  Fix: Lower pressure, add O₂ additive, cool substrate
```

---

## F.7 SEM Analysis Checklist (Quality Control)

```
Routine inspection (per wafer sampled):

□ Profile shape (should be nearly vertical, slight taper OK)
  Expected: V-shaped or rectangular
  Failure: Severe undercut (>10 nm), large scallops (>20 nm)
  
□ Residue visibility (should be minimal or non-visible)
  Acceptable: <0.5 nm invisible, 0.5-3 nm faint gray layer
  Failure: Thick dark layer (>5 nm, opaque)
  
□ Interface definition (W/SiO₂ boundary should be clear)
  Good: Sharp transition (interface <2 nm)
  Bad: Blurred transition (oxidation or residue blending)
  
□ Scallop amplitude (measure peak-to-valley)
  Spec: <20 nm amplitude
  Failure: >25 nm (catastrophic for 5 nm features)
  
□ Corner radius (measure via opening corners)
  Acceptable: <100 nm (photolithography limited)
  Failure: >150 nm (over-etch indication)
  
□ Uniformity across wafer (compare center vs. edge)
  Spec: ±10% depth variation
  Failure: >±15% (radial non-uniformity)

Pass criteria (all must be met):

✓ Residue <3 nm (post-ashing)
✓ Scallops <20 nm
✓ Interface sharp (<2 nm blurring)
✓ Depth ±10% across wafer
✓ Profile nearly vertical (undercut <5 nm)
✓ No particles, no voids

If any fails: 

→ Debug etch recipe (pressure, power, time, temperature)
→ Verify gas flow (additives present)
→ Check equipment health (OES, thermal control)
→ Re-run test wafers with adjusted recipe
```

---

**Appendix F Development Status:** Complete residue analysis procedures  
**Version:** 1.0

