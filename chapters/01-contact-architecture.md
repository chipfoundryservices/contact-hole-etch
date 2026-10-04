# Chapter 1: Contact-Hole Architecture & Electrical Requirements

## Overview

Contact holes (vias) are the interconnects connecting silicon transistors to metal and connecting metal layers to each other. This chapter quantifies via requirements, electrical specifications, and how aspect ratio scaling drives process complexity.

**Learning Objectives:**
- Understand via hierarchy and placement in device stack
- Quantify electrical specifications (resistance, capacitance, leakage)
- Trace aspect ratio evolution across technology nodes
- Correlate process defects to electrical yield
- Design via arrays for uniformity

---

## 1.1 Via Hierarchy in VLSI

### 1.1.1 Layer Sequence & Via Types

```
Typical interconnect stack (28 nm logic node):

Layer         | Material  | Purpose                    | Via to next
------------------------------------------------------------------
Si substrate  | Silicon   | Active transistors         |
              |           |                            |
Contacts (C)  | W (TiN)   | Si→M1 connection          | C-to-M1
              |           | ~40 nm diameter, 8:1 AR    |
              |           |                            |
Metal 1 (M1)  | Cu/W      | Local interconnect         |
              |           | ~50 nm pitch               |
              |           |                            |
Via 1 (V1)    | W (TiN)   | M1→M2 connection          | V1-to-M2
              |           | ~50 nm diameter, 5:1 AR    |
              |           |                            |
Metal 2 (M2)  | Cu        | Routing layer              |
              |           | ~80 nm pitch               |
              |           |                            |
Via 2 (V2)    | W (TiN)   | M2→M3 connection          | V2-to-M3
              |           | ~60 nm diameter, 4:1 AR    |
              |           |                            |
...higher metal layers... | Progressively wider, lower AR

3D NAND stack (same concept, extreme AR):

Layer         | Aspect Ratio | CD (nm) | Depth (nm) | Material
---------------------------------------------------------------
Contacts      | 50-100:1     | 5-10   | 500-800   | W + Barriers
Via 0-5       | 20-50:1      | 10-15  | 200-400   | W + Barriers
Higher vias   | 5-10:1       | 20-40  | 100-200   | Cu/W + TaN
```

### 1.1.2 Electrical Properties of Via Types

```
Contact (C) - Si to M1:

Typical diameter: 40-50 nm (28 nm node)
Depth: 300-400 nm (through oxide + metal)
Aspect ratio: 8:1 typical

Electrical:
  Resistance spec: <1 Ω·µm² specific contact resistivity
  For 45 nm contact: R ≈ (ρ_c / (π × r²))
                   = 1 / (π × (22.5 nm)²) ≈ 0.6 Ω per contact
  Capacitance: ~0.5-1 fF (small, but critical in dense arrays)
  Leakage: <1 pA/contact (junction leakage to substrate)

Via 1/2/3 - Metal to Metal:

Typical diameter: 50-80 nm (for M1-M2 and higher)
Depth: 100-300 nm (through oxide barrier only)
Aspect ratio: 3-5:1 typical

Electrical:
  Resistance spec: <0.1 Ω (for single via)
  Specific contact resistivity: 0.5-2 Ω·µm² (metal-to-metal)
  Capacitance: ~0.1-0.5 fF
  Leakage: Negligible (metal-to-metal, no junction)

Stacked Vias:

Multiple vias in parallel to reduce RC delay
Example (M1-M2 connection):
  Single via: R = 0.2 Ω, parasitic C = 0.3 fF
  4-via stack: R = 0.05 Ω, C = 1.2 fF (slightly higher total C, much lower R)
  RC product: 0.05 × 1.2 = 0.06 (vs. 0.2 × 0.3 = 0.06, same but R dominates delay)
```

---

## 1.2 Via Aspect Ratio Evolution

### 1.2.1 Technology Node Scaling

```
Historical aspect ratio growth:

Node  | Year | Contact AR | Via1 AR | Contact CD | via depth | Challenge
------|------|-----------|---------|-----------|-----------|----------
90nm  | 2004 | 2:1       | 1:1     | 100 nm    | 150 nm    | Simple etch
65nm  | 2006 | 3:1       | 1.5:1   | 80 nm     | 180 nm    | Growing ARDE
45nm  | 2008 | 4:1       | 2:1     | 65 nm     | 200 nm    | Selectivity
28nm  | 2011 | 8:1       | 2.5:1   | 40 nm     | 300 nm    | Radical depletion
20nm  | 2014 | 12:1      | 3:1     | 30 nm     | 300 nm    | Uniformity critical
14nm  | 2015 | 14:1      | 3:1     | 25 nm     | 300 nm    | Profile sensitivity
10nm  | 2017 | 16:1      | 4:1     | 22 nm     | 300 nm    | ARDE compensation
7nm   | 2018 | 20:1      | 5:1     | 16 nm     | 300 nm    | Extreme ARDE
5nm   | 2020 | 25:1      | 6:1     | 12 nm     | 300 nm    | Sub-nm precision
3nm   | 2022 | 30:1      | 7:1     | 10 nm     | 300 nm    | Metal corrosion critical

3D NAND (stacked cells):

Generation | Year | Cell height | Via AR | Contact AR | Challenge
-----------|------|-------------|--------|------------|----------
1st Gen    | 2013 | 20 cells    | 10:1   | 20:1       | High AR new
2nd Gen    | 2015 | 32 cells    | 16:1   | 30:1       | Profile control
3rd Gen    | 2017 | 48 cells    | 25:1   | 50:1       | Residue critical
4th Gen    | 2019 | 64 cells    | 32:1   | 80:1       | Metal damage risk
5th Gen+   | 2022 | 100+ cells  | 50:1   | 100+:1     | Extreme ARDE, selectivity
```

### 1.2.2 Aspect Ratio Impact on Etch

```
Aspect ratio drives four fundamental challenges:

1. Radical Depletion
   
   Flux conservation at depth:
     φ(z) = φ₀ × (1 − α × z / AR_total)
     
   where α ≈ 0.3-0.5 (depletion factor)
   
   At 50% depth (AR = 50:1):
     φ(50nm) / φ₀ ≈ 1 − 0.4 × 0.5 = 0.8 (20% depletion)
   
   At 90% depth (AR = 50:1):
     φ(90nm) / φ₀ ≈ 1 − 0.4 × 0.9 = 0.64 (36% depletion)
   
   Etch rate ratio (bottom-to-top):
     R_bottom / R_top = φ_bottom / φ_top ≈ 64% / 100% = 0.64
     (Bottom etches 36% slower!)
     
   For 100:1 aspect ratio (3D NAND):
     At 50% depth: 50% depletion
     At 90% depth: 90% depletion
     Etch rate bottom/top ≈ 10% / 100% = 0.1 (10× slower!)

2. Shadowing (Ion View Factor)

   Ions travel nearly vertically from plasma
   At high AR, sidewalls create shadow zones
   View factor F = solid angle / 2π
   
   For 50:1 AR, width w, depth d:
     F ≈ w / (2 × d) = (w) / (2 × 50w) = 0.01 (1% view factor)
     Ions barely see sidewalls, mostly see bottom
   
   For 100:1 AR:
     F < 0.005 (sub-percent view factor)
     Ions almost entirely focused on bottom, sidewalls shielded

3. Scalloping Growth at High AR

   Surface rippling wavelength λ ~ √(E_ion × t_etch)
   Wavelength independent of AR, but ripple amplitude grows
   
   After full etch time:
     Amplitude = initial defect × exp(growth_rate × t)
     Relative to feature width: A/w increases with AR
   
   At 10:1 AR with 50 nm feature:
     Scallop amplitude 5-10 nm (tolerable, 5-10% of width)
   
   At 100:1 AR with 5 nm feature:
     Scallop amplitude 5-10 nm (catastrophic, 100-200% of width!)
     Creates complete feature disruption

4. Temperature Gradient

   High RF power creates substrate heating
   Heat dissipates radially (slower outward)
   Center-to-edge temperature difference:
     ΔT ≈ 10-20°C at 1000 W bias power
     ΔT ≈ 50-100°C at 1500 W bias power (for via etch)
   
   Selectivity temperature coefficient: ~1%/°C
   Total selectivity variation across wafer: ±5-10%
   
   Combined with radical depletion:
     Center (warm, full radicals) ~100% nominal rate
     Edge (cool, depleted radicals) ~60% nominal rate
     Total within-wafer variation: 40-50%
```

---

## 1.3 Electrical Specifications & Yield

### 1.3.1 Contact Resistance Budgets

```
Specific Contact Resistivity (ρ_c):

Tungsten contact (W on Si):
  Ideal (TiN/W/TiN barrier): ρ_c ≈ 0.1-0.3 Ω·µm²
  Typical (with native oxide): ρ_c ≈ 0.5-1.0 Ω·µm²
  With interface issues: ρ_c > 2 Ω·µm² (fail spec)

Copper contact (Cu on barriers):
  Cu/TaN interface: ρ_c ≈ 0.05-0.3 Ω·µm²
  Cu/SiN interface: ρ_c ≈ 0.2-0.5 Ω·µm²
  With interfacial reactions: ρ_c > 1 Ω·µm² (fail)

Defect impact on ρ_c:

Undercut (10 nm at via edge):
  Effective area reduction: ~20%
  Resistance increase: ~25% (not linear, due to current crowding)

Residue (5 nm thick oxide on floor):
  Creates insulating layer
  Resistance increase: >100× (near-open circuit)

Surface oxidation (1-2 nm WO₃ on W contact):
  Small but measurable increase: ~10-20%
  Cumulative after multiple wafers: becomes problematic
```

### 1.3.2 Leakage Specification

```
Contact Leakage Sources:

1. Junction Leakage (Si contacts only)

   Reverse bias leakage (diode equation):
     I = I_0 × (exp(qV / nkT) − 1)
     I_0 ≈ q × n_i² × (D_p / N_A + D_n / N_D) / L
   
   For W contact on p-Si, reverse bias:
     I_0 ≈ 10⁻¹³ A (excellent)
     At V = −0.5 V: I ≈ 10⁻¹³ A (near ideal)
   
   Specification: <100 pA/contact typical
   Production target: <50 pA/contact

2. Trap-Assisted Tunneling (TAT)

   Interface traps D_it created during etch:
     J_TAT ∝ D_it × exp(−E_t / kT)
   
   High-quality contact (minimal etch damage):
     D_it ≈ 10¹⁰ cm⁻² eV⁻¹
     J_TAT negligible
   
   Damaged contact (ion implantation, oxidation):
     D_it ≈ 10¹² cm⁻² eV⁻¹
     J_TAT increases 100× (becomes dominant)

3. Gate-Induced Drain Leakage (GIDL)

   High-field tunneling at junction edge
   Occurs when gate biased, drain reversed
   Less relevant for simple contact; more for junction contacts

Total leakage spec:
  Excellent process: <10 pA/contact
  Acceptable: <100 pA/contact
  Failing: >1 nA/contact (indicates defect)
```

### 1.3.3 Yield Correlation to Process Defects

```
Defect → Electrical Failure Mapping:

Defect Type | Frequency | Resistance Impact | Leakage Impact | Yield Loss
------------|-----------|-------------------|----------------|----------
High ρ_c    | 5%        | 100-500% increase | Modest         | 2-5%
Undercut    | 3%        | 20-50% increase   | Minor          | 1-3%
Residue     | 8%        | >1000% increase   | Major          | 4-8%
Oxidation   | 2%        | 10-20% increase   | Minor          | 1-2%
Profile issues| 4%      | Modest            | Increases      | 2-4%
  (scallops)

Total defect yield loss: ~10-22% (typical production)
Target for mature process: <5% (excellent control)

Cumulative yield loss (multiple defect types):

Assume independent probabilities:
  Y_total = (1 − P_ρc) × (1 − P_undercut) × (1 − P_residue) × ...
          = (1 − 0.05) × (1 − 0.03) × (1 − 0.08) × (1 − 0.02) × (1 − 0.04)
          ≈ 0.95 × 0.97 × 0.92 × 0.98 × 0.96
          ≈ 0.8 (80% yield, 20% loss)

Process improvement priorities:
  1. Residue (8% impact): Ashing recipe, plasma composition
  2. High ρ_c (5% impact): Interface cleaning, oxidation control
  3. Profile issues (4% impact): ARDE compensation, thermal control
  4. Undercut (3% impact): Selectivity tuning, process window
```

---

## 1.4 Via Array Design & Uniformity

### 1.4.1 Via Pitch & Density

```
Typical via pitches (minimum feature = CD):

Node  | Contact CD | Via CD | Via pitch | Vias per cell
------|-----------|--------|-----------|---------------
28nm  | 40 nm     | 50 nm  | 100 nm    | 2-4 per cell
20nm  | 30 nm     | 40 nm  | 80 nm     | 4-8
14nm  | 25 nm     | 35 nm  | 70 nm     | 6-12
10nm  | 22 nm     | 30 nm  | 60 nm     | 8-16
7nm   | 16 nm     | 24 nm  | 50 nm     | 12-24
5nm   | 12 nm     | 18 nm  | 40 nm     | 20-40
3nm   | 10 nm     | 15 nm  | 35 nm     | 30-60

3D NAND contact array (vertical):

Generation | Contacts per cell | Array pattern | Spacing
-----------|------------------|---------------|----------
1st Gen    | 1-2              | Single center | 500+ nm
2nd Gen    | 2-4              | Linear        | 300-500 nm
3rd Gen    | 4-8              | 2×2, 2×3      | 200-300 nm
4th Gen    | 8-16             | 2×4, 3×4      | 150-200 nm
5th Gen+   | 16-32            | Dense grid    | 100-150 nm

Array pitch scaling challenges:

As pitch shrinks:
  Etch time per contact increases (same depth, smaller width)
  Radical depletion worsens (denser features consume more radicals)
  ARDE variation increases (outer features starved vs. center)
  Temperature rise increases (more RF power for smaller features)
  Profile uniformity becomes critical for yield
```

### 1.4.2 Across-Wafer Uniformity Targets

```
Contact Resistance Uniformity:

Specification: ρ_c center-to-edge <±10% variation (typical)

Sources of variation:
  1. Radical depletion gradient (radial): ±5%
  2. Temperature gradient (center hotter): ±3-5%
  3. Pressure uniformity (edge lower pressure): ±2%
  4. Showerhead/electrode gap (non-uniform distance): ±1-2%

Total achievable: ±8-12% (difficult to better without tuning)

Production acceptance:
  Excellent: <±5%
  Good: ±5-10%
  Acceptable: ±10-15%
  Failing: >±15%

Leakage Uniformity:

Specification: Leakage variation <±20% (less strict than resistance)
Reason: Leakage dominated by process-corner device variation, less by via uniformity

Profile Uniformity:

Scallop amplitude: <±30% (relative to mean)
Undercut: <±20% edge-to-center
These are looser specs (device design has margin for variation)
```

---

## 1.5 Summary & Key Takeaways

1. **Via Hierarchy Critical** — Contacts (Si to M1) highest AR and tightest spec; higher vias progressively lower AR and wider tolerance; all must meet resistance and leakage budgets.

2. **Aspect Ratio Driving Complexity** — 28 nm (8:1 AR) manageable; 7 nm (20:1) challenging; 3D NAND (100:1) extreme; radical depletion, shadowing, scalloping all scale with AR.

3. **Radical Depletion Severe at High AR** — Bottom of 100:1 via etches 10× slower than top; requires aggressive ARDE compensation (multi-step recipes, pressure tuning, pulsed etch).

4. **Yield Loss Multi-Sourced** — Residue (8%), high ρ_c (5%), profile issues (4%), undercut (3%); cumulative loss 15-25% typical; mature process targets <5%.

5. **Temperature Gradient Degrades Uniformity** — 50-100°C rise from high bias power creates 5-10% etch rate variation across wafer; cooling strategies essential.

6. **Residue Most Damaging** — Metal fluoride residue increases contact resistance >1000×; post-etch ashing critical; residue control determines process viability.

7. **Profile Sensitivity at High AR** — 100:1 feature with 5-10 nm scallops becomes nearly unusable (scallops are 100-200% of width); process window tight, control essential.

---

**Next Chapter:** [Chapter 2 - Metal & Dielectric Materials](./02-metal-dielectric-materials.md)

**Chapter 1 Development Status:** Complete contact architecture and electrical specification framework  
**Version:** 1.0

