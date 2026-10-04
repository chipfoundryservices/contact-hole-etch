# Chapter 13: Post-Etch Damage & Oxidation

## Overview

Ion bombardment creates substrate damage; metal oxidation during and after etch degrades contact resistance. This chapter quantifies damage mechanisms and designs protective strategies.

---

## 13.1 Ion Implantation & Interface Traps

```
Ion damage mechanism:

High-energy ions (100+ eV) penetrate substrate
Displace Si atoms, create defects and vacancies
Oxygen vacancies act as electron traps

Damage depth:

Ion range R ~ √(E_ion) in Si
At E_ion = 100 eV: R ~ 50 nm penetration
At E_ion = 200 eV: R ~ 70 nm penetration

Trap creation:

Interface trap density D_it increase:

Undamaged oxide (high-quality thermal SiO₂): D_it ~ 10¹⁰ cm⁻² eV⁻¹
After low-E_ion etch (50 eV, light damage): D_it ~ 10¹¹ cm⁻² eV⁻¹ (10× increase)
After high-E_ion etch (200 eV, heavy damage): D_it ~ 10¹²-10¹³ cm⁻² eV⁻¹ (100-1000× increase)

Leakage consequence:

TAT (trap-assisted tunneling) current:
J_TAT ∝ D_it × exp(−E_trap / kT)

High-quality contact: 10 pA/contact (excellent)
Light damage: 100 pA/contact (at spec limit)
Heavy damage: 1-10 nA/contact (FAIL, 100-1000× higher)

Mitigation:

Lower E_ion (50-70 eV vs. 100-200 eV):
  Damage depth shallower (~30 nm vs. 70 nm)
  D_it increase smaller (10× vs. 100×)
  Leakage stays 50-100 pA (acceptable)
  Cost: Slower etch rate (10-20% penalty)

Post-etch anneal (low-temperature):
  150-200°C, 30 min in N₂
  Removes some oxygen vacancies
  D_it reduces ~50%
  Cost: Additional process step, +30 min/wafer

Production approach:

Use low-E_ion for contact etch (selectivity + damage protection)
Higher E_ion for bulk oxide etch (not contact-critical)
Minimal post-anneal (if contact leakage spec tight)
```

---

## 13.2 Metal Oxidation During Etch

```
Oxidation rate:

Simultaneous etch (Cl•) and oxidation (O•) when O₂ additive used

100% Cl₂: Minimal oxidation <0.5 nm
Cl₂ + 3% O₂: Moderate oxidation 1-2 nm
Cl₂ + 5% O₂: Higher oxidation 2-5 nm

WO₃ layer consequence:

Resistivity 10¹⁴ Ω·cm (insulating)
Even 1 nm barrier: Contact resistance increases ~5-10×
5 nm layer: >1000× increase (near-open circuit)

Selectivity benefit vs. oxidation cost:

No O₂ option:
  Selectivity: 50:1 (tight window)
  Oxidation: Minimal (~0.5 nm)
  Contact resistance: 0.3 Ω·µm² (good)
  Risk: Over-etch into oxide (yield loss)

With 3% O₂:
  Selectivity: 150:1 (comfortable margin)
  Oxidation: 1-2 nm WO₃ forms
  Contact resistance: 0.5-1.0 Ω·µm² (acceptable)
  Risk: Reduced (large selectivity margin)

Overall: O₂ benefit (selectivity) > cost (modest oxidation)
Production choice: Use O₂ additive for most processes

Post-etch recovery:

H₂ plasma reduction (optional):
  WO₃ + 2H• → W + H₂O
  Removes oxidation layer
  Duration: 30 sec
  Restores ρ_c to pristine value

Cost: Additional step, but perfect recovery
Value: Used when contact spec very tight
```

---

## 13.3 Summary & Key Takeaways

1. **Ion Damage Depth Scales with E_ion** — Range R ~ √(E_ion); at 200 eV penetrates 70 nm; D_it increase 10-1000× depending on energy; low E_ion protection strategy.

2. **Low Ion Energy Reduces Leakage** — 50 eV vs. 200 eV: D_it 10× vs. 100× increase; leakage 100 pA vs. 1 nA; cost: 10-20% slower etch (acceptable trade).

3. **O₂ Additive Oxidation Trade-off** — 3% O₂: selectivity 150:1 (gain); oxidation 1-2 nm (cost); contact resistance 0.5-1.0 Ω·µm² (acceptable); overall benefit positive.

4. **WO₃ Barrier Severely Increases Resistance** — 1 nm oxide: 5-10× increase; 5 nm: >1000× (fails); H₂ plasma post-etch can recover (remove oxide).

5. **Damage Annealing Partially Recovers** — 150-200°C anneal reduces D_it ~50% via vacancy healing; cost +30 min; effective only for light damage (low-E_ion etch).

---

**Next Chapter:** [Chapter 14 - Wafer Temperature Effects](./14-temperature-effects.md)

**Chapter 13 Development Status:** Complete post-etch damage framework  
**Version:** 1.0

