# Appendix D: Reference Tables & Data

Production reference tables, process windows, and look-up data for contact-hole etch optimization.

---

## D.1 Selectivity vs. Temperature & Pressure

```
Table: W/SiO₂ selectivity (S) across process parameter space

Temperature | 10 mTorr | 20 mTorr | 30 mTorr | 40 mTorr | 50 mTorr | 80 mTorr | 100 mTorr
------------|----------|----------|----------|----------|----------|----------|----------
0°C         | 85:1     | 110:1    | 130:1    | 140:1    | 145:1    | 150:1    | 148:1
20°C        | 75:1     | 95:1     | 110:1    | 120:1    | 125:1    | 130:1    | 128:1
40°C        | 65:1     | 80:1     | 90:1     | 100:1    | 105:1    | 110:1    | 108:1
60°C        | 55:1     | 70:1     | 80:1     | 85:1     | 90:1     | 95:1     | 93:1
80°C        | 50:1     | 60:1     | 70:1     | 75:1     | 80:1     | 85:1     | 83:1
100°C       | 45:1     | 55:1     | 60:1     | 65:1     | 70:1     | 75:1     | 73:1

Reading example:
  At 20°C and 40 mTorr: S = 120:1 (good process window)
  At 80°C and 10 mTorr: S = 50:1 (minimum safe selectivity, risky)
  
Key insights:
  Low pressure (10 mTorr) selective but ARDE poor
  High pressure (100 mTorr) uniform but selectivity erodes
  Optimal balance: 30-50 mTorr (110-120:1 selectivity)
  Temperature control critical (±20°C → ±10% selectivity change)
```

---

## D.2 ARDE vs. Aspect Ratio & Pressure

```
Table: ARDE (Aspect Ratio Dependent Etch) ratio across feature types

Feature AR | 10 mTorr | 20 mTorr | 30 mTorr | 40 mTorr | 50 mTorr | 80 mTorr
-----------|----------|----------|----------|----------|----------|----------
5:1        | 2:1      | 1.8:1    | 1.6:1    | 1.5:1    | 1.4:1    | 1.3:1
10:1       | 4:1      | 3.5:1    | 3:1      | 2.8:1    | 2.5:1    | 2:1
20:1       | 8:1      | 7:1      | 5.5:1    | 5:1      | 4:1      | 3:1
50:1       | 20:1     | 15:1     | 12:1     | 10:1     | 8:1      | 5:1
100:1      | 50:1     | 35:1     | 25:1     | 20:1     | 15:1     | 8:1

Reading example:
  50:1 via at 40 mTorr: ARDE = 10:1 (manageable with multi-step)
  100:1 via at 10 mTorr: ARDE = 50:1 (severe, needs pulsed plasma)
  
Trend:
  Higher pressure → lower ARDE (better uniformity)
  But pressure also reduces selectivity
  Trade-off optimization critical
```

---

## D.3 Etch Rate vs. Power Settings

```
Table: W etch rate (nm/min) at 40 mTorr, 30°C substrate, 300 sccm Cl₂

Coil Power | 500 W bias | 800 W bias | 1000 W bias | 1200 W bias | 1500 W bias
-----------|------------|------------|-------------|-------------|----------
1000 W     | 45 nm/min  | 65 nm/min  | 75 nm/min   | 85 nm/min   | 95 nm/min
1500 W     | 50 nm/min  | 75 nm/min  | 90 nm/min   | 105 nm/min  | 120 nm/min
2000 W     | 55 nm/min  | 85 nm/min  | 105 nm/min  | 125 nm/min  | 150 nm/min
2500 W     | 60 nm/min  | 95 nm/min  | 120 nm/min  | 145 nm/min  | 170 nm/min
3000 W     | 65 nm/min  | 105 nm/min | 135 nm/min  | 165 nm/min  | 200 nm/min

Reading example:
  2000W coil + 1000W bias: 105 nm/min (bulk etch typical)
  1500W coil + 500W bias: 50 nm/min (selective finish typical)
  
Selectivity impact:
  Higher bias → more ion sputtering → selectivity degrades
  But faster etch enables multi-step recipes
  Trade-off: Use high power for bulk, low power for finish
```

---

## D.4 O₂ Additive Effect on Selectivity & Etch Rate

```
Table: Selectivity vs. O₂ fraction (at 40 mTorr, 20°C, 2000W coil, 1000W bias)

O₂ percent | Selectivity | W etch rate | SiO₂ rate | Impact
-----------|-------------|-------------|-----------|----------
0%         | 50:1        | 100%        | 2%        | Baseline
0.5%       | 75:1        | 96%         | 1.5%      | Slight improvement
1.0%       | 100:1       | 92%         | 1%        | Good margin
1.5%       | 120:1       | 88%         | 0.8%      | Better
2.0%       | 135:1       | 85%         | 0.7%      | Excellent
3.0%       | 150:1       | 80%         | 0.65%     | Best
4.0%       | 145:1       | 75%         | 0.7%      | Saturation
5.0%       | 140:1       | 70%         | 0.8%      | Over-addition

Production choice: 2-3% O₂ optimal (150:1 selectivity, only -15 to -20% W rate penalty)
```

---

## D.5 Endpoint Timing (OES) Reference

```
Table: Endpoint time vs. step and target depth (Single-step selective finish)

Target     | Pure Cl₂  | Cl₂+1% O₂ | Cl₂+2% O₂ | Cl₂+3% O₂ | Notes
depth (nm) | time (s)  | time (s)  | time (s)  | time (s)  |
-----------|-----------|-----------|-----------|-----------|----------
100        | 30        | 32        | 34        | 36        | Shallow
200        | 60        | 65        | 70        | 75        | Typical contact
300        | 90        | 98        | 105       | 113       | Deep via
400        | 120       | 131       | 140       | 151       | Very deep
500        | 150       | 163       | 175       | 188       | 3D NAND

Margin strategy:
  To reach 500 nm with 3% O₂: Set endpoint trigger at 160-170 sec
  Over-etch window: 20-30 sec (safety margin for SiO₂ break-through)
  Actual etch time via OES: 188 - 160 = 28 sec margin (safe)
```

---

## D.6 Thermal Properties & Cooling System Sizing

```
Table: Thermal resistance (R_th) vs. cooling configuration

Configuration              | R_th (K/W) | ΔT at 800W | Substrate T
---------------------------|------------|------------|----------
No cooling (air gap)       | 0.15-0.20  | 120-160°C  | 140-160°C
He backside 10 mTorr       | 0.05-0.08  | 40-64°C    | 60-84°C
Mechanical chiller 2 GPM   | 0.04-0.06  | 32-48°C    | 52-68°C
LN₂ loop                   | 0.02-0.03  | 16-24°C    | 36-44°C

Chiller sizing:

Heat load during etch: 800 W (RF bias power → substrate)
Target substrate: 40°C (or lower)
Ambient fab: 20°C

Cooling capacity needed:
  Q = (T_substrate − T_ambient) / R_th = (40 − 20) / 0.05 = 400 W minimum
  Recommended chiller: 500+ W cooling capacity
  Typical industrial chiller: 1-2 kW (oversized for margin)

Cost estimate:
  Mechanical chiller: $40-50K installed
  LN₂ supply system: $70-80K + $5K/year gas
  He backside loop: $15-25K installed
```

---

## D.7 Residue Thickness After Etch (Production Range)

```
Table: Residue thickness (nm) by metal, additive, and plasma conditions

Metal | No O₂  | 1% O₂ | 2% O₂ | 3% O₂ | Post-ashing removal
------|--------|-------|-------|-------|-------------------
W     | 8-12   | 4-8   | 2-5   | 1-3   | >90% (0.3-1 nm remains)
Cu    | 15-20  | 8-12  | 5-8   | 3-5   | 80-90% (1-2 nm remains)
TaN   | 5-10   | 3-5   | 1-3   | 1-2   | >90% (0.2-1 nm remains)
Ti    | 10-15  | 6-10  | 3-6   | 2-4   | 85-95% (0.5-1.5 nm remains)

Reading example:
  W etch with 2% O₂: 2-5 nm residue (post-etch)
  After O₂ ashing: <1 nm residue (acceptable)
  ρ_c recovery: 0.3-0.8 Ω·µm² (good)
```

---

## D.8 Contact Resistivity (ρ_c) Yield Specifications

```
Table: ρ_c specification limits and yield impact

ρ_c range     | Category  | Fab action           | Yield impact
--------------|-----------|----------------------|-------------
<0.3 Ω·µm²   | Excellent | Use in production    | 100% pass
0.3-0.8       | Good      | Standard spec        | 99-100%
0.8-1.5       | Marginal  | Monitor, tighter QC  | 95-99%
1.5-5         | Poor      | Fail wafer, debug    | 50-90% (risky)
>5            | Fail      | Scrap wafer          | <50% (unacceptable)

Correlation with defects:

Residue >5 nm → ρ_c >5 (nearly open)
Oxidation layer >2 nm WO₃ → ρ_c 2-10 Ω·µm²
Implant damage D_it 10¹² → ρ_c 1-5 Ω·µm²
Scallops >20 nm → ρ_c 0.8-1.5 (secondary effect)

Production strategy:
  Target: <0.5 Ω·µm² median
  Spec: <1.0 with 99% yield
  Margin: Residue removal, cooling, low-E_ion etch
```

---

**Appendix D Development Status:** Complete reference tables  
**Version:** 1.0

