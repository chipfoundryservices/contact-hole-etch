# Chapter 12: Profile & Residue Formation

## Overview

Profile defects (scalloping, undercut, corner rounding) and residue (metal fluorides) are primary yield killers. This chapter quantifies formation mechanisms and designs mitigation strategies.

---

## 12.1 Scalloping at High Aspect Ratio

```
Scalloping mechanism:

Ion-induced surface rippling creates periodic sidewall roughness
Wavelength λ ~ √(E_ion × t_etch) = 10-50 nm
Amplitude grows over time: A(t) ~ 5-20 nm peak-to-valley

Formation rate (100:1 via):

Initial roughness: <1 nm
After 100 nm Si etch (20 sec): ~5-10 nm scallops
After 300 nm Si etch (60 sec): ~15-20 nm scallops (saturates)

Relative to feature width:

5 nm feature with 20 nm scallops = 400% of width! (catastrophic)
50 nm feature with 20 nm scallops = 40% of width (problematic)
100 nm feature with 20 nm scallops = 20% of width (acceptable)

Impact on leakage:

Scallop-induced interface area increase ~30%
Trap density increases proportionally
Leakage current: ~20-30% increase
Yield spec <100 pA: Met (usually) but margin erodes

Reduction strategies:

1. Pulsed plasma (50% duty): Scallop amplitude -50%
2. Low pressure: Shorter wavelength λ, smaller amplitude
3. Lower E_ion: Reduces ripple growth rate
4. Higher temp: Thermal smoothing (marginal, -10-20%)
5. Post-etch ashing: Remove scallop-roughened polymer (if any)

Practical mitigation:

Use pulsed plasma for 3D NAND (critical AR)
Multi-step recipe for logic (less critical)
Specification: <20 nm acceptable, <15 nm preferred, >25 nm FAIL
```

---

## 12.2 Undercut & Corner Rounding

```
Undercut (lateral etch):

Anisotropic etch (ions directional) → minimal undercut
But at high AR, lateral radical access from sides creates some undercut

Typical: 2-5 nm undercut (small)
Specification: <10 nm acceptable

Corner rounding:

From mask diffraction (photolithography limit):
  50 nm corner radius from mask fabrication
  
Plus plasma corner rounding:
  Over-etch at corner → additional 50 nm rounding
  
Total: ~100 nm corner radius on 50 nm feature (huge!)

Impact:
  Effective opening widens: 50 nm → 100 nm (doubled)
  Capacitive coupling increases
  Device performance degraded

Reduction:
  Tight selectivity control (minimal over-etch)
  Low E_ion (less sputter at corner)
  OPC (optical proximity correction) at design stage
```

---

## 12.3 Residue Formation & Removal

```
Metal fluoride byproducts:

WCl₂, WCl₃ (partially volatile at room T, can deposit)
WCl₆ (mostly escapes, but some deposits on sidewalls)
CuCl₂ (non-volatile, sticks to surfaces)
TiCl₂ (very non-volatile, heavy residue)

Deposition rate:

Typical during etch: 1-10 nm residue per contact
On electrode: <1 nm (mostly escapes up)
On sidewalls: 5-10 nm possible (bad!)
On floor: 10-50 nm possible (catastrophic!)

Post-etch removal:

Plasma ashing (O₂ plasma):
  Oxidizes metal fluorides → oxides (easier to remove)
  Polymerizes organic residue → CO₂ + H₂O (escapes)
  Duration: 30-60 sec
  Temperature: 50-100°C (warm, not hot)
  
Result: >90% residue removal
Cost: +30-60 sec per wafer, +$1K process equipment
ROI: Prevents 100% yield loss (residue → open circuits)

Specification:

Residue thickness <1 nm: Excellent (restored ρ_c ~0.3 Ω·µm²)
Residue 1-3 nm: Good (ρ_c ~0.5-1 Ω·µm², acceptable)
Residue >5 nm: Fail (ρ_c >5 Ω·µm², device fails)

Production adoption:

Post-etch ashing MANDATORY in all modern fabs
Failure to ash = 100% yield loss (visible failure)
Standard process step (non-negotiable)
```

---

## 12.4 Summary & Key Takeaways

1. **Scalloping Scales with Feature Size** — 20 nm scallops on 5 nm feature = 400% (fails); 20 nm on 100 nm feature = 20% (OK); pulsed plasma reduces amplitude 50%.

2. **Undercut Minor** — 2-5 nm typical (<10 nm spec); high AR reduces directivity slightly; controlled via E_ion and selectivity tuning.

3. **Corner Rounding 100 nm Typical** — Mask 50 nm + plasma 50 nm = 100 nm total; widens opening, increases parasitic coupling; OPC at design can mitigate.

4. **Residue Catastrophic if Not Removed** — WCl₂/CuCl₂ deposits 5-50 nm; even 5 nm → 10× resistance increase; post-etch O₂ ashing removes >90%, enables process.

5. **Ashing Mandatory Every Etch** — +30-60 sec per wafer; cost <$1K amortized; prevents 100% yield loss; non-negotiable production step.

---

**Next Chapter:** [Chapter 13 - Post-Etch Damage & Oxidation](./13-postetch-damage.md)

**Chapter 12 Development Status:** Complete profile & residue framework  
**Version:** 1.0

