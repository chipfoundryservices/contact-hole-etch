# Glossary: Technical Terms & Definitions

## A–G

**ARDE** (Aspect Ratio Dependent Etching)
Variation in etch rate as a function of feature aspect ratio. At high AR (50-200:1 in contact etch), radicals deplete deep in features, creating 10-100× etch rate variation from top to bottom. See Chapter 10.

**Aspect Ratio**
Ratio of etch depth to width. Contact-hole etch: 50-200:1 typical (vs. 5-20:1 for STI). Determines radical depletion severity.

**Arrhenius Equation**
k(T) = A × exp(−E_a / RT)  
Describes temperature dependence of chemical reaction rates. E_a (activation energy) typically 8-20 kcal/mol for etch reactions. See Chapter 3.

**Backside Cooling**
Transfer of heat from wafer to chuck via He or N₂ gas at backside. Improves thermal conductance by 10-50× vs. vacuum. Critical for contact etch thermal management (Chapter 8).

**Bias Power**
RF power applied to wafer electrode to accelerate ions. Higher bias → higher E_ion → faster etch, lower selectivity. Typical 500-2000 W for metal etch. See Chapter 6.

**Breakdown (Field)**
Electric field at which insulator (SiO₂, SiN) becomes conductive. ~5-10 MV/cm typical. Avoid during etch design to prevent oxide damage.

**Capacitance**
Storage of electric charge. Parasitic capacitance between vias increases interconnect RC delay. Proportional to via area, inversely to spacing.

**Chlorine (Cl₂)**
Gas used for metal etch (W, Cu). More selective to metals than to dielectrics than F₂. Primary chemistry in contact-hole etch. See Chapter 3.

**Coil Power**
RF power applied to induction coil surrounding chamber. Controls plasma density and radical generation. Typical 1500-2500 W for metal etch. See Chapter 6.

**Contact Resistance**
Resistance at interface between metal and silicon or metal-to-metal. Specified as specific contact resistivity (Ω·µm²). W: 0.1-1; Cu: 0.05-0.5. See Chapter 4.

**Corrosion**
Chemical reaction degrading material surface. Tungsten oxidation (W → WO₃), copper oxidation (Cu → CuO, Cu₂O) are key failure modes. See Chapter 7.

**CTE** (Coefficient of Thermal Expansion)
Change in size per unit temperature. Si: 2.6 ppm/°C, SiO₂: 0.5 ppm/°C, W: 4 ppm/°C. CTE mismatch creates stress during thermal cycling. See Chapter 14.

**Cryogenic**
Very low temperature operation. Contact etch cannot use −140°C (would freeze water/residue in vias) unlike STI etch. Operates at 20-100°C.

**Current Crowding**
Concentration of current in localized regions rather than uniform distribution. In high-AR vias, current crowding at via corners/floor increases local current density.

**Dissociation**
Molecular bond breaking. e⁻ + Cl₂ → e⁻ + 2Cl• (electron-impact dissociation). Primary step creating reactive radicals.

**Endpoint Detection**
Method to determine when etch reaches target material (typically oxide stop layer). Optical reflectance common for metal etch. See Appendix F.

**Etch Rate**
Speed of material removal during etch, typically nm/min. W: 50-200 nm/min; SiO₂: 5-50 nm/min (depending on selectivity mode).

**Etching**
Controlled removal of material via chemical/physical reactions in plasma. Anisotropic (directional, high AR) vs. isotropic (lateral, low AR). See Chapters 10-14.

**Fluoride**
Compound of fluorine with another element. WF₆ (tungsten fluoride), CuF₂ (copper fluoride) are byproducts and residue sources. See Chapter 3.

**Fluorine (F₂)**
Gas used primarily for dielectric etch, not metal. More selective to dielectrics; less used in contact etch. See Chapter 3.

**Flux**
Number of particles (ions or radicals) arriving at surface per unit area per unit time. Units: cm⁻² s⁻¹. Higher flux → faster etch.

---

## H–N

**Hard Mask**
Resistant etch mask deposited before photoresist. Typically Si₃N₄ or amorphous carbon. Transfers pattern after photoresist strip.

**Halogen**
Family of reactive elements: F, Cl, Br, I. Used in plasma etching due to high reactivity.

**Heat of Reaction**
Energy released or absorbed during chemical reaction. Exothermic (releases heat) reactions generate temperature rise in chamber.

**Impedance**
Resistance to RF power delivery in circuit. Chamber/plasma impedance typically 10-50 Ω; matching network transforms to 50 Ω standard. See Chapter 9.

**Implantation** (Ion)
Deep incorporation of ions into substrate during etch. High-energy ions (>100 eV) penetrate Si, creating defects and interface traps. See Chapter 13.

**Interface Trap Density** (D_it)
Defects at Si/SiO₂ interface created during plasma etch. Increases leakage and reduces device performance. High-quality thermal oxide: 10¹⁰ cm⁻² eV⁻¹; plasma-etch degraded: 10¹² cm⁻² eV⁻¹.

**Interconnect**
Metallic wiring connecting transistor elements. Multiple metal layers (M1, M2, etc.) separated by dielectrics, connected by vias.

**Ion Energy Distribution** (IED)
Spread of ion energies in plasma. Gaussian-like distribution centered on E_ion. FWHM typically 20-40 eV. See Chapter 6.

**Kinetics**
Study of reaction rates and mechanisms. Etch kinetics determine how fast material is removed. See Chapter 3.

**Leakage**
Unwanted current flowing through insulator or reverse-biased junction. Increases power consumption, limits device functionality. Via contact etch must minimize.

**Local Interconnect** (LI)
Metal layer connecting transistor source/drain within a cell. Densest contact array; highest aspect ratio vias.

**Low-K Dielectric**
Insulator with low dielectric constant (κ <3) to reduce capacitance. SiOC, SiLK are fragile; easily damaged by etch. See Chapter 2.

**Mass Flow Controller** (MFC)
Device that measures and controls gas flow rate in sccm (standard cubic centimeters per minute). Precision ±2% typical.

**Mean Free Path**
Average distance a particle travels between collisions. λ ∝ T / P (higher temp, lower pressure → longer λ). At 1 mTorr: λ ~1 mm.

**Microloading**
Effect of feature density on etch rate—dense features etch slower than isolated features due to radical depletion. Extreme case: 100× rate variation across wafer.

**Molar Mass**
Mass in grams of one mole (6.02×10²³) of atoms/molecules. Cl₂: 71 g/mol, W: 184 g/mol.

**Nitride** (Silicon Nitride)
Si₃N₄ compound used as etch barrier. More selective than SiO₂ (etch rate 5-10× lower). See Chapter 2.

**Notching**
Localized undercut at interfaces between different materials. Caused by plasma reflection or ion scattering. Increases leakage at via corners. See Chapter 12.

---

## O–Z

**Oxide** (Silicon Dioxide)
SiO₂ compound used as dielectric and etch stop layer. Thermal oxide (grown on Si) vs. CVD oxide (deposited). See Chapter 2.

**Oxidation**
Chemical reaction with oxygen. Tungsten oxidation (W + O₂ → WO₃) during etch increases contact resistance. Rate typically 0.1-1 nm/wafer. See Chapter 7.

**Passivation**
Protective layer on surface reducing etch rate. Polymer passivation in STI etch (not used in contact etch). SiO₂ formation on SiN (low-K protection).

**Plasma**
Ionized gas containing electrons, ions, and radicals. Created by RF or DC discharge. Provides reactive species for etch.

**Polymer**
Large organic molecule formed from smaller units. In contact etch, minimal polymer; in STI etch, CF_x polymer protects SiO₂. See Chapter 11 (STI book).

**Pulsed Plasma**
Etch performed with plasma ON/OFF cycling (e.g., 5 sec ON, 5 sec OFF). Allows radical diffusion, reduces ARDE. See Chapter 10.

**Quantum Yield**
Number of atoms sputtered per incident ion. Depends on ion energy and material. W: ~0.1-0.3 at 100 eV.

**Radical** (Free Radical)
Atomic or molecular species with unpaired electron (•). Cl• is primary etch species in metal etch. Highly reactive, short-lived (<1 ms typical).

**Residue**
Unwanted material remaining after etch. Metal fluorides (WF₆, CuF₂) in contact etch; polymers in STI. Requires post-etch cleaning. See Chapter 12.

**Resistance**
Opposition to electrical current flow. Contact resistance at via/metal interface; sheet resistance of thin film; total resistance of interconnect.

**RGA** (Residual Gas Analyzer)
Mass spectrometer measuring plasma species composition during etch. Identifies radicals, ions, byproducts. See Chapter 9.

**RF** (Radio Frequency)
Oscillating electromagnetic field at MHz frequencies (13.56 MHz standard). Accelerates ions, creates plasma.

**Scalloping**
Periodic surface roughness on sidewalls. Wavelength 10-50 nm, amplitude 5-20 nm (at high AR, more severe). Caused by ion-induced rippling. See Chapter 12.

**Selectivity**
Ratio of etch rates between two materials. W etch / SiO₂ etch; typical 100-500:1. Determines how long oxide stop layer survives. See Chapter 11.

**Sheet Resistance**
Resistance of thin film material measured in ohms per square. ρ/t where ρ is resistivity, t is thickness. Controls delay in interconnect. See Chapter 4.

**Shadowing**
Geometric effect where ions cannot reach recessed surfaces due to line-of-sight angles. Severe at high AR; creates ARDE. See Chapter 10.

**Sputtering**
Physical removal of material by ion bombardment. Yield Y (atoms/ion) typically 0.1-1 at 100 eV ion energy.

**Stress** (Mechanical)
Force per unit area. CTE mismatch creates tensile or compressive stress. Cumulative over thermal cycles can cause delamination.

**Substrate**
Base material on which device is built. Silicon in most processes.

**TDDB** (Time-Dependent Dielectric Breakdown)
Long-term degradation of insulator under electrical stress. Trap accumulation eventually causes breakdown. Lifetime depends on field and temperature. See Chapter 4.

**Thermal Budget**
Total temperature exposure during all processing steps. High thermal budget increases defects, changes dopant profiles, causes stress.

**Thermal Gradient**
Spatial variation in temperature across wafer. At high bias power, center hotter than edge by 10-20°C. Creates selectivity and etch rate variation. See Chapter 14.

**Thermalization**
Loss of high kinetic energy ions through collisions, thermalizing to plasma temperature. Shifts IED toward lower energy.

**Throughput**
Number of wafers processed per unit time. Contact etch tool: 4-8 wafers/hour typical (slow due to high AR and multi-layer stacks).

**TLM** (Transmission Line Model)
Measurement technique to extract specific contact resistivity from resistor array test structure. Used to characterize via/metal interface.

**Tool**
Equipment system performing etch. Includes chamber, RF generators, gas delivery, vacuum pump, control electronics.

**Torr**
Pressure unit. 1 Torr = 1/760 atmosphere. Typical etch: 5-100 mTorr (0.005-0.1 Torr). See Chapter 5.

**Tungsten** (W)
Metal used for contact, local interconnect, via fill. Excellent electrical properties, easily oxidized. See Chapter 2.

**Undo-Ability**
In plasma processing, reversibility of process. Once oxidation or damage occurs, difficult to reverse. Design prevents damage rather than fixing after.

**Undercut**
Lateral etching under mask or interface. High-AR contact etch more prone to undercut due to radical access from sides. See Chapter 12.

**Uniformity**
Consistency of etch rate, selectivity, or profile across wafer diameter. Specifications: ±5-10% typical. Challenged by ARDE at high AR. See Chapter 10.

**Valence**
Number of electrons available for bonding. Cl (valence 1) in Cl₂; W (valence 6) in tungsten. Determines bonding and reactivity.

**Vapor Pressure**
Pressure of gaseous form at equilibrium with solid/liquid. Important for estimating gas concentrations in chamber.

**Voltage** (Bias)
Electrical potential applied to substrate. Determines ion energy (E_ion ≈ 0.3 × V_bias). Typical 500-2000 V in metal etch.

**Wafer**
Silicon disk (200-300 mm diameter) on which semiconductor devices are fabricated.

**Xerox Effect**
Plasma-induced pattern distortion mimicking original photoresist shape even after hard mask transfer. Due to local ion/radical flux variation.

**Yield**
Percentage of functional devices after processing. Target >95% for contact etch (typically 90-98% depending on defect sources).

**Zoning**
Spatial division of wafer (center, middle, edge) for analysis. Thermal gradient creates zoning effects (center hotter, etch faster).

---

## Abbreviations & Symbols

| Term | Meaning |
|------|---------|
| **E_a** | Activation energy (kcal/mol) |
| **E_ion** | Ion kinetic energy (eV) |
| **P** | Pressure (mTorr, Torr) |
| **T** | Temperature (°C or K) |
| **k** | Reaction rate constant |
| **Y** | Sputtering yield (atoms/ion) |
| **φ** | Particle flux (cm⁻² s⁻¹) |
| **λ** | Mean free path (cm) |
| **S** | Selectivity (ratio) |
| **V_bias** | Bias voltage (volts) |
| **P_coil** | Coil power (watts) |
| **P_bias** | Bias power (watts) |
| **AR** | Aspect ratio (dimensionless) |
| **ρ** | Resistivity (Ω·cm) |
| **κ** | Dielectric constant |
| **CTE** | Coefficient of thermal expansion (ppm/°C) |
| **ΔE** | Energy difference (eV, kcal/mol) |
| **ΔT** | Temperature difference (°C, K) |
| **ΔP** | Pressure difference (Torr, mTorr) |

---

**GLOSSARY Version:** 1.0  
**Total Terms:** 65 definitions  
**Cross-references:** Terms linked to relevant chapters and appendices

