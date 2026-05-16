# Research Notes: Chapter 11 — Maxwell's Equations and Electromagnetic Waves

**Source:** TIKTOC.md chapter entry (Chapter 11)
**Notes file:** 11-maxwells-equations_notes.md
**Corresponding chapter:** chapters/11-maxwells-equations.md (not yet written)
**Generated:** 2026-05-14

---

## Chapter summary (from TIKTOC.md)

The payoff chapter. Maxwell adds the displacement current to Ampère's law, completing the four equations. The consequence, derived in the same paper: oscillating EM solutions exist, propagating at c = 1/√(μ₀ε₀) = 3 × 10⁸ m/s. Light is an electromagnetic wave. Plane wave solutions, transverse geometry, **E** ⊥ **B** ⊥ **k**, energy density, Poynting vector, radiation pressure, the EM spectrum. Simulation: transverse EM wave visualizer with **E** and **B** oscillating in perpendicular planes.

---

## A. Conceptual foundations

### The asymmetry Maxwell noticed (and the displacement current)

Going into 1861, the four laws were:

1. Gauss's law for **E**: ∮**E**·d**A** = Q_enc/ε₀
2. Gauss's law for **B**: ∮**B**·d**A** = 0
3. Faraday's law: ∮**E**·d**ℓ** = −dΦ_B/dt
4. Ampère's law: ∮**B**·d**ℓ** = μ₀ I_enc

Notice the asymmetry between (3) and (4):
- (3): a *changing magnetic flux* drives circulation of **E**
- (4): a steady current drives circulation of **B**, but a *changing electric flux* does nothing

Maxwell found this troubling. The asymmetry was also *inconsistent* in a specific case: the charging capacitor. Imagine an Amperian loop encircling a wire that carries current into a capacitor plate. Choose two surfaces bounded by this loop: surface 1 is the flat disk pierced by the wire; surface 2 is a "bag" that detours around the wire and passes *between the capacitor plates*. By Ampère's law (4), the integral ∮**B**·d**ℓ** should equal μ₀ I_enc for either surface — but I_enc is I through surface 1 and zero through surface 2 (no wire goes through it). Same left-hand side, different right-hand side. Contradiction.

Maxwell's fix (1861, formalized 1865): add a new term so the right-hand side counts the changing electric flux *as if it were a current*:

∮**B**·d**ℓ** = μ₀ I_enc + μ₀ε₀ dΦ_E/dt

The new term μ₀ε₀ dΦ_E/dt is the **displacement current**. Between the capacitor plates, no conduction current flows, but the electric field grows as charge builds on the plates — so dΦ_E/dt is nonzero, and the displacement current through surface 2 exactly equals the conduction current through surface 1. Consistency restored.

**The four complete Maxwell equations:**

Integral form:
1. ∮**E**·d**A** = Q_enc/ε₀
2. ∮**B**·d**A** = 0
3. ∮**E**·d**ℓ** = −dΦ_B/dt
4. ∮**B**·d**ℓ** = μ₀ I_enc + μ₀ε₀ dΦ_E/dt

Differential form (in vacuum, with charge density ρ and current density **J**):
1. ∇·**E** = ρ/ε₀
2. ∇·**B** = 0
3. ∇×**E** = −∂**B**/∂t
4. ∇×**B** = μ₀**J** + μ₀ε₀ ∂**E**/∂t

**Source:** Maxwell, "A dynamical theory of the electromagnetic field," Phil. Trans. R. Soc. 155, 459–512 (1865). https://royalsocietypublishing.org/doi/10.1098/rstl.1865.0008

**Common misconception:** "Maxwell invented the displacement current to save his equations from inconsistency." This puts the cart before the horse. The motivating issue was *charge conservation at a capacitor*; the consistency was a consequence. Maxwell was looking for the right physical equation, and the displacement current was the missing physics, not a mathematical patch.

**Common misconception #2:** "The displacement current is a real current." It is not a flow of charge. It is a *term in Ampère's law* with units of current that captures the magnetic effect of a changing electric field. Some books call it a "pseudo-current"; the name is unfortunate, but the formula does the work.

### Deriving the wave equation from Maxwell

In a source-free region (ρ = 0, **J** = 0):

3. ∇×**E** = −∂**B**/∂t
4. ∇×**B** = μ₀ε₀ ∂**E**/∂t

Take the curl of (3):
∇×(∇×**E**) = −∂/∂t (∇×**B**) = −μ₀ε₀ ∂²**E**/∂t²

Using the vector identity ∇×(∇×**E**) = ∇(∇·**E**) − ∇²**E**, and ∇·**E** = 0 in source-free region:
−∇²**E** = −μ₀ε₀ ∂²**E**/∂t²

So:

∇²**E** = μ₀ε₀ ∂²**E**/∂t²

This is the **wave equation**. Comparing to the standard wave equation ∇²f = (1/v²) ∂²f/∂t², the wave speed is

v = 1/√(μ₀ε₀)

Plug in μ₀ = 4π × 10⁻⁷ T·m/A and ε₀ = 8.854 × 10⁻¹² C²/(N·m²):

v = 1/√(4π × 10⁻⁷ × 8.854 × 10⁻¹²) ≈ 2.998 × 10⁸ m/s

This is the speed of light. Maxwell did the calculation himself in 1862 and immediately recognized the implication. From his 1864 paper: *"We can scarcely avoid the inference that light consists in the transverse undulations of the same medium which is the cause of electric and magnetic phenomena."*

The realization that light is an electromagnetic wave is the single greatest unification in 19th-century physics. Before 1864: optics, electricity, and magnetism were three separate subjects. After 1864: one set of equations covers all three.

The same derivation works for **B** (take curl of (4), substitute (3)). **E** and **B** both satisfy the same wave equation with the same speed.

### Plane wave solutions

The simplest solutions to the wave equation are plane waves propagating in one direction (take +x without loss of generality):

**E**(x, t) = E₀ cos(kx − ωt) ŷ
**B**(x, t) = B₀ cos(kx − ωt) ẑ

with constraints from Maxwell's equations:
- ω = ck (dispersion relation; equivalently, λf = c)
- E₀ = c B₀ (amplitude ratio)
- **E** ⊥ **B** ⊥ direction of propagation (transverse wave)
- **E** × **B** points in the direction of propagation (right-hand triad)

**Why transverse:** because ∇·**E** = 0 in source-free vacuum, the wave's longitudinal **E** component must vanish. The wave's spatial variation must be perpendicular to its direction of propagation.

**Polarization** refers to the direction of **E** in the transverse plane. Linear polarization (constant direction), circular polarization (rotating direction), elliptical (general).

### Energy and the Poynting vector

The energy density of an electromagnetic field is the sum of electric and magnetic contributions:

u = ½ε₀E² + B²/(2μ₀)

In a plane wave, these are equal at every instant: u_E = u_B. The wave carries equal energy in **E** and **B**.

The **Poynting vector** is the energy flux:

**S** = (1/μ₀) **E** × **B**

Direction: along the propagation direction (for a plane wave). Magnitude: power per unit area (W/m²) carried by the wave. For a plane wave with amplitudes E₀, B₀:

|S| = E₀B₀/μ₀ · cos²(kx − ωt)

Time-averaging cos² to ½:

I = ⟨|S|⟩ = E₀²/(2μ₀c) = (cε₀/2) E₀²

I is the **intensity** of the wave. Sunlight at Earth's surface: I ≈ 1000 W/m². Corresponding peak E ≈ 870 V/m, peak B ≈ 2.9 µT.

### Radiation pressure

EM waves carry momentum. For a wave with energy density u, momentum density is u/c. For a wave absorbed by a surface at intensity I:

P_radiation = I/c (absorbing surface)
P_radiation = 2I/c (perfectly reflecting surface)

Solar radiation pressure at Earth: ~9 × 10⁻⁶ N/m² absorbing, ~9 × 10⁻⁶ × 2 ≈ 2 × 10⁻⁵ N/m² for a solar sail. Small, but cumulative over a long mission — the basis of solar-sail propulsion.

The first detection of radiation pressure: P. N. Lebedev (1900), Nichols & Hull (1901).

### The electromagnetic spectrum

All EM waves obey the same wave equation; they differ only in frequency (and equivalently wavelength: λ = c/f). The spectrum:

| Region | Frequency | Wavelength | Photon energy | Sources, uses |
|---|---|---|---|---|
| Radio | <10⁹ Hz | >30 cm | <4 µeV | Broadcast, mobile, radar |
| Microwave | 10⁹–10¹² Hz | 30 cm–0.3 mm | 4 µeV–4 meV | Ovens, WiFi, radar, satellite, CMB |
| Infrared | 10¹²–4×10¹⁴ Hz | 0.3 mm–700 nm | 4 meV–1.7 eV | Heat, night vision, fiber optics |
| Visible | 4×10¹⁴–8×10¹⁴ Hz | 700–400 nm | 1.7–3.1 eV | Sight, photosynthesis, illumination |
| Ultraviolet | 8×10¹⁴–10¹⁶ Hz | 400–10 nm | 3.1–124 eV | Sunburn, vitamin D, sterilization |
| X-ray | 10¹⁶–10¹⁹ Hz | 10 nm–0.01 nm | 124 eV–124 keV | Medical imaging, crystallography |
| Gamma | >10¹⁹ Hz | <0.01 nm | >124 keV | Nuclear decay, particle physics, cosmic |

The 10²² range from FM radio to the highest gamma rays is *the same wave* with the same speed and the same equations. Only the frequency changes.

---

## B. Domain examples and cases

### Case 1: Hertz's 1887–1888 experiments
Heinrich Hertz, at the Technische Hochschule Karlsruhe, built the first apparatus to *generate and detect electromagnetic waves on purpose*. A spark-gap oscillator (capacitor discharged through an inductor) produced ~100 MHz oscillations; a small wire loop on the other side of the lab developed sparks when the oscillator fired, even with the receiver shielded from the transmitter's light. The wavelength (~3 m) was demonstrable by reflection and standing-wave measurements. Hertz confirmed:
- The waves propagate at c (within experimental error)
- They are reflected, refracted, polarized — same as light
- They are transverse (polarization can be filtered)

Maxwell's prediction (1864) became experimental fact (1887–1888). Hertz himself said: "It's of no use whatsoever... this is just an experiment that proves Maestro Maxwell was right." Marconi (1895–1901) commercialized it as radio.

**Source:** Bryant, J. H. "Heinrich Rudolph Hertz: The Beginning of Microwaves." Discovery of Electric Waves and Their Use in Communication, IEEE Press (1988). Revisiting the 1888 Hertz experiment, Am. J. Phys., DOI:10.1119/1.2238886.

### Case 2: Radio communication
Radio antennas oscillate currents at fixed frequencies; the resulting EM waves propagate and induce currents in distant receiver antennas. Modulation (AM, FM, digital) encodes information on a carrier. Every wireless device — phone, WiFi, GPS, satellite TV — is applied Maxwell.

### Case 3: Light is an electromagnetic wave (Michelson, 1879+)
Before Maxwell's prediction, the speed of light had been measured (Fizeau 1849, Foucault 1862). After Maxwell, the agreement between measured c and the value of 1/√(μ₀ε₀) was overwhelming evidence for the EM nature of light. Michelson refined measurements through the 1880s; the agreement convinced the physics community. The luminiferous-ether hypothesis (a medium for the wave to oscillate in) lasted until the Michelson-Morley 1887 null result; this is the bridge to special relativity.

### Failure case (deeper than intro): point-particle radiation
Maxwell's equations are linear and cover continuous **E**, **B**, ρ, **J**. They break down for point charges: the self-energy of a point electron diverges, the Abraham-Lorentz radiation reaction is non-causal in some regimes, and any sufficiently small structure gets quantum corrections. The chapter need not address these, but should mention that classical EM is a *limit* of a quantum theory (QED) — which is itself the most precisely tested theory in physics.

---

## C. Connections and dependencies

**Prerequisites (what reader must already know):**
- All four pre-Maxwell laws (Chs 3, 9, 10) plus Faraday — so the chapter has something to add to
- Vector calculus operationally: curl and divergence as differential operators acting on vector fields. The chapter introduces these via Stokes' and divergence theorems if not already known.
- Wave equation: that ∇²f = (1/v²) ∂²f/∂t² is a wave with speed v. (May need a brief reminder.)

**Unlocks (what this chapter makes possible):**
- Ch 12 (capstone): optics, antennas, photoelectric effect, special relativity — all consequences
- Modern physics: photons (E = hf for the EM quantum), the photoelectric effect (where classical EM breaks down), special relativity (Maxwell's equations are Lorentz-covariant)
- Engineering: antennas, transmission lines, optical fibers, waveguides — all start from Maxwell

**Adjacent chapter connections:**
- Ch 10 (Faraday): the third Maxwell equation; the changing-flux insight that opens the door to wave solutions
- Ch 12 (capstone): the consequences for the physical world — light, antennas, the EM spectrum

---

## D. Current state of the field

**Settled:**
- Classical Maxwell's equations are mature, complete, and exact in their domain of applicability
- The wave equation derivation and prediction of c are taught essentially the same way in every text from Halliday/Resnick to Jackson
- Hertz's experimental confirmation is settled physics history
- The 1865 Maxwell paper is on the Royal Society's open archive

**Contested or emerging:**
- *None at the intro level.* The chapter is unambiguous mature physics.
- *At advanced levels:* QED corrections to classical EM (vacuum polarization, light-by-light scattering); these are real but enormously small at intro scales.

**Key references:**
1. Maxwell, J. C. "A dynamical theory of the electromagnetic field." Phil. Trans. R. Soc. 155, 459 (1865). https://royalsocietypublishing.org/doi/10.1098/rstl.1865.0008
2. Maxwell, J. C. *A Treatise on Electricity and Magnetism.* Oxford (1873). The book-length treatment. https://archive.org/details/electricandmag02maxwrich
3. Hertz, H. *Electric Waves.* (English translation, Macmillan, 1893). The experimental confirmation, written by the experimenter.
4. Griffiths, *Introduction to Electrodynamics*, Ch. 9 (electromagnetic waves). Cleanest undergraduate treatment of plane waves and Poynting.
5. Jackson, *Classical Electrodynamics*, 3rd ed., Ch. 6–7. The graduate treatment for reference.
6. "A paper I hold to be great guns: a commentary on Maxwell (1865)." Phil. Trans. R. Soc. A 373, 20140473 (2015). Modern reassessment of Maxwell's 1865 paper. https://royalsocietypublishing.org/rsta/article/373/2039/20140473

**Recent developments (last 3 years):**
- *Computational EM* (FDTD simulation methods) increasingly accessible in browsers; the chapter's D3 transverse-wave simulation is a baby version of these
- *Metamaterials* enable manipulation of EM waves in ways inaccessible with natural materials (negative refractive index, cloaking). Beyond intro scope but worth a sentence in Ch 12.

---

## E. Teaching considerations

**Where students get stuck:**
- *The displacement current's physical motivation.* Students see it as an arbitrary patch. The chapter must spend real prose on the charging-capacitor inconsistency and the surface-choice problem.
- *Vector curl in the wave-equation derivation.* The identity ∇×(∇×**E**) = ∇(∇·**E**) − ∇²**E** is unmotivated for many students. The chapter should derive or accept it explicitly.
- *The transverse-wave structure.* That **E**, **B**, and the propagation direction form a right-handed triad is non-obvious; students often draw waves with **E** and **B** parallel. The simulation can fix this visually.
- *The wave equation's "v² = 1/(μ₀ε₀)" punchline.* Many students compute the number without recognizing it as c. The chapter should make this discovery explicit and dramatic — Maxwell's own surprise is the model.

**Analogies and framings that work:**
- *Domino chain* — Faraday: changing B kicks E; Maxwell's addition: changing E kicks back, kicking B. Once started, the kickback chain propagates as a wave. The image is loose but the structural insight is right.
- *Light is just radio waves you can see* — collapses the EM spectrum into one phenomenon with one set of equations. The most useful single sentence in the chapter.
- *c shows up in the equations whether you ask it to or not* — the Maxwell discovery framed as inevitable consequence rather than coincidence.

**Exercises that build the target skill:**
- *Displacement current at a capacitor* (Bloom: Apply) — given dV/dt across a capacitor, find I_d, verify it equals the conduction current I. Tests displacement-current arithmetic in the canonical case.
- *Wave-equation derivation walked through* (Bloom: Apply + Analyze) — guide the student through taking curl of (3), applying the vector identity, arriving at v² = 1/(μ₀ε₀). Then compute v. Tests both the calculus and the recognition of c.
- *Plane wave intensity from amplitude* (Bloom: Apply) — given E₀ = 100 V/m, find B₀, find I = (cε₀/2)E₀². Standard.
- *Solar sail* (Bloom: Apply + Synthesize) — given solar I ≈ 1366 W/m² at 1 AU, compute radiation pressure on a perfect reflector. Discuss whether a 100 m² sail could accelerate a 10 kg payload meaningfully. Tests P = 2I/c and force/mass reasoning.
- *Power dissipation in a resistor as Poynting flux into the resistor* (Bloom: Synthesize) — the energy enters the resistor through its surface; compute the Poynting vector at the surface and verify Σ S · dA = I²R. A surprising and beautiful result that the chapter should include if there's room.

---

## F. Library files relevant to this chapter

None directly relevant.

---

## G. Gaps and flags

- FLAG: The vector identity ∇×(∇×**E**) = ∇(∇·**E**) − ∇²**E** must be either derived or stated. The intro audience may not have seen it. Recommend: state it, point to a one-paragraph derivation in an appendix, demonstrate it on a worked example.
- FLAG: The chapter must commit on whether to use SI or Gaussian units. SI is the modern intro standard; the chapter should be SI throughout but mention that older papers (including Maxwell's) use Gaussian.
- GAP: The chapter is dense; the TIKTOC asks for both the displacement-current argument and the wave-equation derivation and the EM spectrum. Recommend splitting into clear sub-sections to avoid cognitive overload.
- FLAG: Hertz's 1887–1888 confirmation deserves at least a paragraph; it's the most dramatic confirmation in 19th-century physics and is often skipped in intro texts.
