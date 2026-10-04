# Appendix E: Thermal Calculations & Cooling System Design

Detailed thermal modeling, heat transfer calculations, and cooling system sizing for contact-hole etch chambers.

---

## E.1 Substrate Temperature Model

```
Basic heat balance equation:

P_in = P_out + dQ/dt

where:
  P_in = RF power delivered to substrate (watts)
  P_out = Thermal power dissipated to cooler (watts)
  dQ/dt = Rate of temperature change (W = J/s)

At steady state (dQ/dt = 0):

P_in = P_out

Thermal resistance model:

ΔT = T_substrate − T_coolant = P_dissipated × R_th

where R_th is total thermal resistance (K/W)

RF power to substrate:

Bias power input: P_bias = 1000-1500 W (typical)
Conversion efficiency to heat: η ≈ 80% (rest goes to ion/plasma)
Substrate heat: P_substrate = P_bias × η ≈ 800-1200 W

Example calculation:

Condition: 1000W bias, 80% efficiency, no cooling
  P_substrate = 1000 × 0.80 = 800 W
  R_th (no cooling) = 0.15 K/W
  ΔT = 800 × 0.15 = 120°C above stage temperature
  
  If stage held at 20°C (ambient fab):
    T_substrate = 20 + 120 = 140°C
    
  If stage cooled to 0°C (ice):
    T_substrate = 0 + 120 = 120°C (still hot!)

With helium backside cooling:

R_th (He backside) ≈ 0.05 K/W
ΔT = 800 × 0.05 = 40°C
T_substrate = 20 + 40 = 60°C (much better)
```

---

## E.2 Thermal Resistance Breakdown

```
Total thermal resistance path (no cooling):

R_th_total = R_contact + R_substrate + R_stage + R_chuck

Component                    | Resistance (K/W) | Notes
-----------------------------|------------------|------------------------------
Wafer-chuck contact (air)    | 0.05-0.10        | Poor contact, thermal gap
Substrate (300mm, 0.75mm)    | ~0.001           | Si conductor, negligible
Chuck material (Al, 5mm)     | ~0.01            | Aluminum, moderate
Chuck-stage interface        | 0.02-0.05        | Mechanical contact, limited
Stage-chamber (radiation)    | 0.05-0.10        | Radiative + conduction
Air gap to cooling loop      | 0.02-0.03        | If no active cooling

Total (no cooling):          | 0.15-0.20        | Typical measured

With helium backside:

He thermal conductivity (25°C): κ = 0.142 W/m·K (very good)
He pressure: 10-20 mTorr
He gap: 0.5-1 mm

R_He ≈ gap / (κ × A_contact) × (pressure factor)

For 300mm wafer:
  A_contact ≈ 70,000 cm² (nearly full wafer)
  R_He ≈ (0.0005 m) / (0.142 W/m·K × 0.07 m²) × (correction factor)
  R_He ≈ 0.05 K/W

Total (with He):             | 0.05-0.08        | 3-4× improvement

With liquid cooling loop:

Chiller output: 1-2 kW @ 20°C
Loop flow: 2-5 GPM
Heat transfer: h = 1000-5000 W/m²·K (forced convection)

R_cooler ≈ 1 / (h × A_contact) ≈ 0.02-0.04 K/W

Total (with chiller):        | 0.04-0.06        | 3-4× improvement

With LN₂ loop:

Liquid N₂ at -196°C (77 K)
Heat transfer: h = 5000-10000 W/m²·K (very high, boiling)

R_LN₂ ≈ 0.02-0.03 K/W

Total (with LN₂):           | 0.02-0.03         | 5-10× improvement
```

---

## E.3 Temperature Ramp-Up During Etch

```
Time-dependent substrate temperature:

T(t) = T_coolant + (P_in × R_th) × [1 − exp(−t / τ)]

where τ = C × R_th (thermal time constant)

C = thermal capacitance (J/K) of substrate + chuck assembly

Example calculation (no cooling):

Substrate + chuck mass: 5 kg (typical)
Heat capacity c ≈ 500 J/kg·K (aluminum average)
Total C ≈ 2500 J/K

R_th = 0.15 K/W
τ = 2500 × 0.15 = 375 sec ≈ 6 minutes

Temperature vs. time during etch:

Time (sec) | T(t) - T_coolant (°C) | Substrate T (at 20°C ambient)
-----------|------------------------|---------------------------
0          | 0                      | 20°C
30         | 20                     | 40°C (15 min into etch)
60         | 35                     | 55°C
120        | 62                     | 82°C
180        | 85                     | 105°C
300        | 115                    | 135°C (steady state)

Production implication:

Etch time 160 sec → substrate reaches ~95°C
Not steady state (still ramping)
Temperature varies during etch steps
Selectivity varies throughout etch (worst at end = over-etch risk!)

Multi-step recipe benefit (revisited):

Step 1 (0-60 sec): T rises from 20°C to 55°C
  Selectivity: 110:1 → 90:1 (acceptable, bulk etch)
  
Step 2 (60-100 sec): T rises 55°C to 82°C
  Selectivity: 90:1 → 70:1 (transition, still OK)
  
Step 3 (100-160 sec): T rises 82°C to 95°C (capped by Step 3 lower power)
  Actually, Step 3 uses only 300W bias (not 1000W)
  T rise much slower: 82°C + (300W × 0.15 K/W) = 82 + 45 = 127°C theoretical
  But starts at 82°C, reaches ~105°C in 60 sec (slower ramp due to lower power)
  Selectivity at 95°C: ~75:1 (adequate for finishing)

With cooling (He backside):

τ = 2500 × 0.05 = 125 sec (much shorter time constant)
Step 3 temperature stabilizes much faster → stays near 40-50°C
Selectivity maintained ~100-120:1 throughout
Much better process control
```

---

## E.4 Chiller/Cooling System Sizing

```
Cooling system capacity calculation:

Design requirement:
  Maintain substrate <50°C during 160 sec etch
  Ambient fab temperature: 20°C
  Power dissipated: 800 W average (over multi-step)

Target ΔT: 50°C - 20°C = 30°C
Required R_th: 30°C / 800W = 0.0375 K/W (requires active cooling)

Chiller sizing:

Heat removal rate = (T_substrate − T_chiller_output) / R_cooler

Assume T_chiller_output = 15°C (chiller setpoint)
T_substrate target = 50°C
ΔT across cooler = 50 − 15 = 35°C

Heat flow: Q = 800W (dissipation rate)
Cooler capacity needed ≥ 800W continuous

Industrial chiller specifications:

Small chiller (lab grade):
  Capacity: 500-1000 W @ 20°C
  Footprint: 1m × 0.5m
  Cost: $40-50K
  Adequate for single tool
  
Large chiller (fab grade):
  Capacity: 2-5 kW @ 20°C
  Footprint: 2m × 1m
  Cost: $60-100K
  Can cool multiple tools (3-5 chambers)
  
LN₂ system (alternative):

Liquid nitrogen container: 50-100 L capacity
Supply: Daily delivery, ~$100-200/delivery
Heat exchange: Cryogenic coil
Capacity: Effectively unlimited (can reach -50°C if needed)
Cost: $70-80K installed + $5K/year gas
Advantage: Lowest substrate temperature (stability)
Disadvantage: Consumable (ongoing cost), safety procedures
```

---

## E.5 Heat Transfer in Chamber

```
Substrate heat transfer pathways:

1. Conduction through stage/chuck:
   Q_cond = k × A × ΔT / d
   
   Example (Al chuck, 10mm thick):
   k = 237 W/m·K (aluminum)
   A = 0.07 m² (wafer contact area)
   ΔT = 50°C (substrate to chuck backside)
   d = 0.01 m (chuck thickness)
   
   Q_cond = 237 × 0.07 × 50 / 0.01 = 83 kW (?!)
   
   In reality:
   - Contact area incomplete (not full 70k cm²)
   - Effective area ~30% = 0.021 m²
   - Q_cond ≈ 25 kW (still large, but only ~3% of total)

2. Radiation from substrate surface:

   Q_rad = ε × σ × A × (T_substrate^4 − T_chamber^4)
   
   ε = emissivity (W surface, ε ≈ 0.3)
   σ = Stefan-Boltzmann (5.67×10⁻⁸ W/m²·K⁴)
   
   Example (substrate 350K, chamber 300K):
   Q_rad = 0.3 × 5.67e-8 × 0.07 × (350^4 − 300^4)
   Q_rad ≈ 40 W (very small, negligible at high temps)

3. Convection (chamber gas):

   Minimal in CCP chamber (low pressure, low gas velocity)
   Q_conv ≈ 10-20 W (negligible)

4. Evacuation (cooling loop):

   Q_loop = C_p × ṁ × ΔT
   
   where:
   ṁ = mass flow rate (kg/s)
   C_p = heat capacity (J/kg·K)
   ΔT = temperature change across cooler
   
   Example (He loop, 10 mTorr, small flow):
   He conductivity dominates
   Effective heat removal ~800 W possible with correct design

Production design:

- Most heat removed via He backside diffusion or chiller loop
- Radiation and convection negligible at CCP pressures
- Focus cooling design on backside interface
- He backside = best bang-for-buck (low cost, effective)
- Chiller = more control (active feedback possible)
```

---

## E.6 Thermal Stress & CTE Mismatch

```
Coefficient of thermal expansion (CTE):

Material            | CTE (ppm/K) | Notes
--------------------|-------------|----
Silicon wafer       | 2.6         | Low, stable
Al chuck            | 23          | High (9×Si)
SiO₂ dielectric     | 0.5         | Very low
Tungsten via        | 4.5         | Moderate

During 80°C temperature swing (room to etch):

Si wafer 300mm:
  Length change: 300mm × 2.6e-6 /K × 80K = 0.062 mm (negligible)
  
Al chuck:
  Length change: 300mm × 23e-6 /K × 80K = 0.55 mm (significant!)
  Radial expansion: ~0.55mm/2 = 0.28 mm at edge (wafer eccentricity possible!)

Consequence:

Thermal expansion mismatch can cause:
  - Wafer tilt (±1°, reduces contact area)
  - Air gap growth (reduces He cooling effectiveness)
  - Edge vs. center temperature differential
  
Mitigation:

1. Use low-CTE chuck materials:
   Invar (Fe-Ni alloy): CTE = 2 ppm/K (matches Si closely)
   Cost: 2-3× more expensive than Al
   Benefit: Eliminates thermal mismatch
   
2. Active wafer centering:
   Adjust chuck pins during etch
   Compensate for thermal expansion
   Cost: $10-20K retrofit
   Benefit: Maintains tight contact
   
3. Controlled temperature ramp:
   Slow heating (Step 1 gradual, not step increase)
   Allows mechanical stress to equalize
   Benefit: Reduces transient stresses

Production practice:

High-volume fabs: Often use Invar chucks (cost justified by uniformity)
R&D/low-volume: Accept slight thermal drift (use recipe compensation)
Advanced nodes: Invar + active centering (margin critical)
```

---

## E.7 Thermal Gradient Across Wafer

```
Radial temperature variation:

Center of wafer:
  Farthest from edge, most isolated
  Receives 1000W bias RF power
  Temperature highest at center
  
Edge of wafer:
  Closer to chamber wall (radiation to wall, cooler)
  Better heat dissipation (air circulation)
  Temperature 5-20°C lower than center
  
Typical ΔT center-to-edge: 15-25°C

At 40 mTorr pressure, selectivity strongly temperature-dependent:
  S ∝ exp(13/RT)
  
Selectivity variation:

Center (T_max = 95°C): S ≈ 75:1
Edge (T_min = 75°C): S ≈ 95:1
Difference: +27% selectivity at edge

Consequence:

Edge under-etches (lower etch rate due to lower temp AND lower plasma)
Center over-etches (higher temp, more etch)
Radial uniformity ±15-20% (unacceptable for advanced nodes)

Mitigation strategies:

1. Active substrate cooling (He backside or chiller):
   Flatten temperature gradient (smaller ΔT)
   Reduces selectivity variation to ±10%
   
2. Thermal compensating chuck:
   Insulate center, cool edge preferentially
   Complex, rarely used
   
3. Showerhead/gas distribution optimization:
   Flow more gas to edge (cooler, more radicals)
   Compensate etch rate difference
   Effective, standard approach
   
4. Multi-zone plasma heating:
   Different bias at center vs. edge
   Very expensive (separate RF systems)
   Rarely implemented
   
5. Recipe adaptation:
   Shorten total etch time (less temperature ramp)
   Accept ±10% uniformity (live with it)
   Low cost, often used
```

---

**Appendix E Development Status:** Complete thermal modeling and calculations  
**Version:** 1.0

