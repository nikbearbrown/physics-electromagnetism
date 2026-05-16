# Research Notes: Chapter 09 — Sources of Magnetic Fields

**Source:** TIKTOC.md chapter entry (Chapter 09)
**Notes file:** 09-sources-magnetic-fields_notes.md
**Corresponding chapter:** chapters/09-sources-magnetic-fields.md (not yet written)
**Generated:** 2026-05-14

---

## Chapter summary (from TIKTOC.md)

The magnetic analogue of Chs 2+3 combined. Biot-Savart law (magnetic Coulomb's law); Ampère's law (magnetic Gauss's law). Canonical results: infinite straight wire, circular loop, solenoid. Force between parallel wires → definition of the ampere. Differential form ∇×**B** = μ₀**J** as a Maxwell-equation preview. Gauss for magnetism: ∇·**B** = 0 (no monopoles). Simulation: field-line visualizer for configurable current sources.

---

## A. Conceptual foundations

### Biot-Savart: the magnetic field from a current element

For a current I flowing through a wire element d**ℓ** (vector along current direction), the magnetic field d**B** at a point displaced by **r** from the element is

d**B** = (μ₀/4π) · I (d**ℓ** × r̂) / r²

where μ₀ = 4π × 10⁻⁷ T·m/A is the **permeability of free space**.

This is the magnetic analogue of d**E** = k dq r̂ / r² from Coulomb. Notice three differences:
1. The source is *current* (I dℓ), not charge.
2. The cross product makes d**B** *perpendicular* to both d**ℓ** and r̂. The field curls around the current.
3. The constant μ₀/4π plays the role of k = 1/(4πε₀) — note the inversion: ε₀ is "permittivity" (electric); μ₀ is "permeability" (magnetic). They satisfy c² = 1/(μ₀ε₀), preparing Chapter 11's wave-speed punchline.

**Right-hand rule for the direction of B around a current:** point thumb along the current; fingers curl in the direction of **B**. For a straight wire, **B** is in circles around the wire, counterclockwise when viewed in the direction the current flows.

**Common misconception:** "Magnetic field lines start on north poles and end on south poles." They don't. They form closed loops. The closed-loop topology is the deep difference from electric field lines. There is no "source" of B in the way charge is a source of E.

**Worked example: B on the axis of a circular current loop of radius R.**
Take loop in xy-plane, current I counterclockwise viewed from +z. Compute B at point P = (0,0,z) on the axis.
- Each current element d**ℓ** is in the xy-plane; r̂ from the element to P has both a horizontal component (back toward axis) and a vertical component (toward P).
- d**B** = (μ₀I/4π) (d**ℓ** × r̂)/r²; the cross product gives d**B** perpendicular to d**ℓ** and to r̂. Decompose into axial (z) and radial components.
- By symmetry: integrating around the loop, all radial contributions cancel; only the axial component survives.
- The axial component of dB is dB · (R/r) where r = √(R² + z²). Integrate around the loop (∫dℓ = 2πR):
  
  B_z = (μ₀ I R²) / (2(R² + z²)^(3/2))

At center (z=0): B = μ₀I/(2R). On the axis far away (z ≫ R): B ≈ μ₀IR²/(2z³) — a dipole field, falling as 1/z³. Just like the electric dipole far field falling as 1/r³.

The 1/r³ dipole far-field tells you something deep: even though current loops have a different microscopic origin than electric dipoles, their *far fields share the same angular and radial structure*. The magnetic moment **m** = I A n̂ is the magnetic analogue of the electric dipole moment **p** = qd.

### Infinite straight wire: B = μ₀I/(2πr)

The cleanest Biot-Savart integral. For a long straight wire carrying current I, the field at perpendicular distance r is

B = μ₀I / (2πr)

with direction circular around the wire (right-hand rule). Falls off as 1/r (not 1/r²), because the wire is infinite — adding more length adds more contribution from elements at larger angles.

For two parallel wires separated by distance d, carrying currents I₁ and I₂ in the same direction: the field from wire 1 at the location of wire 2 is B₁ = μ₀I₁/(2πd), perpendicular to wire 2. Force per unit length on wire 2: F/L = I₂ B₁ = μ₀I₁I₂/(2πd). Parallel currents *attract*; antiparallel currents *repel*. This is the inverse of the Coulomb situation for like charges — and historically it's how the ampere was defined.

### Ampère's law: ∮ **B** · d**ℓ** = μ₀ I_enc

The magnetic analogue of Gauss's law. The integral form: the line integral of **B** around any closed loop equals μ₀ times the current piercing the loop.

**Derivation sketch:** For an infinite wire, B = μ₀I/(2πr); on a circle of radius r centered on the wire, **B** is parallel to d**ℓ**, |**B**| is constant. ∮**B**·d**ℓ** = B(r) · 2πr = (μ₀I/(2πr))(2πr) = μ₀I. The result is independent of r, so it generalizes: for any closed loop encircling the current once, ∮**B**·d**ℓ** = μ₀ I_enc.

For computational use, choose **Amperian loops** the way you chose Gaussian surfaces in Ch 3 — to exploit symmetry. The three useful symmetries:

1. **Long straight wire** → circular Amperian loop concentric with the wire. Gives B(r) = μ₀I/(2πr).
2. **Solenoid** (long, n turns/length) → rectangular Amperian loop with one side inside, one outside, two perpendicular sides. Outside ≈ 0; perpendicular sides give zero; inside side gives B·L = μ₀nIL → **B = μ₀nI** (uniform inside, zero outside).
3. **Toroid** (N turns wrapped around a doughnut) → circular Amperian loop inside the toroid concentric with the toroid axis. ∮B·dℓ = B(2πr) = μ₀NI → **B = μ₀NI/(2πr)** (inside the toroid).

**Common misconception:** "Ampère's law only works for infinite symmetric currents." Like Gauss's law, Ampère's law is *always true*; symmetry only determines whether it's *computationally useful*.

### Gauss's law for magnetism: ∇·**B** = 0 (no monopoles)

The magnetic analogue of Gauss's law for **E** would read ∇·**B** = (magnetic charge density)/μ₀. But no magnetic charges have ever been observed. So:

∮ **B** · d**A** = 0 for any closed surface

Equivalently: magnetic field lines form closed loops. Every field line that enters a region must exit it. This is one of the four Maxwell equations.

Dirac (1931) showed that *if* a single magnetic monopole existed, it would explain the quantization of electric charge. The hypothesis remains live in some grand-unified theories. Experimental searches (MoEDAL at LHC, others) have not found one as of 2026. The cleanest negative result: no isolated magnetic charges in the universe at present detection limits.

### Magnetic flux and the definition of the ampere

**Magnetic flux** Φ_B = ∫∫**B**·d**A** through a surface. Units: weber (Wb) = T·m². Important for Chapter 10 (Faraday's law uses Φ_B).

**The ampere — old vs. new definition.**

*Old definition (pre-2019, the "1948 definition"):* The ampere is the constant current that, when maintained in two straight parallel infinite conductors 1 m apart in vacuum, produces a force per unit length of 2 × 10⁻⁷ N/m between them. This is exactly the F/L = μ₀I₁I₂/(2πd) formula with I₁ = I₂ = 1 A, d = 1 m, giving F/L = 2 × 10⁻⁷ N/m. The definition *fixes* μ₀ = 4π × 10⁻⁷ T·m/A exactly. This is why the constant has its odd numerical value.

*New definition (May 20, 2019):* The ampere is defined by *fixing the value of the elementary charge* e = 1.602 176 634 × 10⁻¹⁹ C (exact). 1 ampere = 1 coulomb / second; the coulomb is the charge of 1/e ≈ 6.241509 × 10¹⁸ elementary charges. As a consequence, μ₀ is no longer exact — it must now be measured, though its value is still very close to 4π × 10⁻⁷.

The 2019 SI redefinition is a milestone worth a paragraph in the chapter: the ampere went from being defined by a mechanical thought experiment (infinite parallel wires, infinite vacuum) to being defined by a fundamental quantum constant.

**Source:** NIST "Ampere: History" https://www.nist.gov/si-redefinition/ampere-history ; BIPM SI Brochure 9th ed. (2019), Appendix 2.

### Magnetic materials: diamagnets, paramagnets, ferromagnets

When a material is placed in an external **B**, internal currents respond:

- **Diamagnets** (most materials): induced atomic currents oppose B; small negative susceptibility. Bismuth, water, copper (technically). Relative permeability μ_r slightly < 1.
- **Paramagnets** (some materials): atoms have permanent magnetic moments that partially align with B; positive susceptibility but small. Aluminum, oxygen (liquid). μ_r slightly > 1.
- **Ferromagnets** (iron, nickel, cobalt, neodymium alloys): atomic moments align cooperatively over large *domains*; below the Curie temperature, the material can be permanently magnetized. μ_r in the hundreds to thousands. Hysteresis: B(H) loop shows memory of past field exposure.

For intro purposes: most circuits assume μ ≈ μ₀ (air, copper, etc.); inductor cores use ferromagnetic material to boost L by μ_r.

---

## B. Domain examples and cases

### Case 1: MRI solenoid
Modern MRI scanners use superconducting solenoids producing 1.5 T, 3 T, or 7 T in clinical use; up to 11.7 T in research scanners. Field uniformity required: parts per million across the imaging volume. Built as multiple coaxial solenoids with carefully engineered current distributions. The base formula B = μ₀nI for the ideal infinite solenoid is the conceptual anchor; real MRI magnets are far more sophisticated, but the principle is exactly this chapter's content.

Useful number: a 3 T MRI field is about 60,000× Earth's magnetic field. The Earth's field at the surface is ~50 µT.

### Case 2: Electric motor and the force between currents
Every electric motor exploits F = I**L** × **B** (Ch 8) on current-carrying conductors in a magnetic field. The B field is produced by either permanent magnets (DC motors, brushless motors) or coils (universal motors, induction motors — see Ch 10). The torque on a current loop in B is τ = NIA × B sin θ; integrating over rotation gives mechanical work. Industrial motors push hundreds of kW; the largest electric motors push megawatts (ship propulsion).

### Case 3: Earth's magnetic field
Earth's magnetic field is generated by convective currents of liquid iron in the outer core — a self-sustaining dynamo. Approximated as a dipole with magnetic moment ~8 × 10²² A·m², slightly tilted from the rotation axis. Surface strength ~25–65 µT depending on location. The field reverses on geological timescales (~hundreds of thousands of years); the magnetic poles drift continuously. The Biot-Savart picture (currents → field) is the framework; the dynamo physics is beyond intro scope.

### Failure case: ignoring fringing fields at solenoid ends
The B = μ₀nI formula is for the *infinite* solenoid. Real solenoids have ends where the field drops. At the geometric end of a long solenoid, B ≈ ½μ₀nI (half the interior value). Students who use the infinite-solenoid formula at the ends of a real coil get wrong answers by a factor of 2. The chapter should explicitly call this out.

---

## C. Connections and dependencies

**Prerequisites (what reader must already know):**
- Cross products (and the right-hand rule)
- Line integrals (used in Ampère's law)
- Ch 8 (magnetism and magnetic force): the Lorentz force and force on current-carrying conductors are needed for the parallel-wires derivation
- Ch 3 (Gauss's law) and Ch 4 (potential): the *method* of choosing surfaces/loops by symmetry is the cross-chapter conceptual move

**Unlocks (what this chapter makes possible):**
- Ch 10 (Faraday): magnetic flux through a coil from a configurable B field — the source side of induction
- Ch 11 (Maxwell): the differential form ∇×**B** = μ₀**J** is Maxwell pre-displacement-current; adding ∂**E**/∂t completes it
- Energy density of the magnetic field u_B = B²/(2μ₀) is introduced in Ch 10 but its computational ground (the solenoid as the canonical B-field container) is here

**Adjacent chapter connections:**
- Ch 8: force on charges and conductors in given B. Here, we compute B from currents.
- Ch 10: changing B creates E. Here, currents produce static B.
- Ch 11: Ampère + displacement current → Maxwell's fourth equation; this chapter prepares the ground.

---

## D. Current state of the field

**Settled:**
- Biot-Savart law and Ampère's law in classical magnetostatics: exact, mature
- All worked applications (wire, loop, solenoid, toroid, parallel-wires force) are universal across intro texts
- The post-2019 SI definition of the ampere via elementary charge

**Contested or emerging:**
- *Magnetic monopole searches.* Theoretical motivation exists (Dirac quantization, grand unification); no experimental detection. Current limits from MoEDAL at LHC and IceCube cosmic-ray searches.
- *Antiferromagnetic spintronics:* manipulating spin without net magnetic moment for high-density memory; physics is beyond intro scope but worth a mention.

**Key references:**
1. Griffiths, *Introduction to Electrodynamics*, Ch. 5. The definitive intro Biot-Savart and Ampère treatment.
2. Serway & Jewett, Ch. 30 (Sources of B). Standard intro presentation.
3. NIST, "Ampere: History" and "Ampere: The Present" — https://www.nist.gov/si-redefinition/ampere-history. The story of the 2019 redefinition.
4. BIPM SI Brochure, 9th ed. (2019), Appendix 2 on the ampere. The legal definition.
5. Ampère, A.-M. *Mémoire sur la théorie mathématique des phénomènes électrodynamiques.* (1820–1827). Original derivations of the force between currents.
6. Biot, J.-B. & Savart, F. Ann. Chim. Phys. 15, 222 (1820). Original report of the law.

**Recent developments (last 3 years):**
- 2019 SI redefinition (ampere now defined via fixed e) is still being absorbed into pedagogy; many texts still teach the 1948 definition. The chapter should teach the new definition explicitly.
- Improvements in MRI field strength (commercial 7 T scanners increasingly available 2022–2025).

---

## E. Teaching considerations

**Where students get stuck:**
- *Cross products and the right-hand rule.* The geometry of d**ℓ** × r̂ is the chapter's hardest pure-math hurdle. Students who can multiply numbers can fail at choosing the correct direction. Practice with 3D vector arrows is essential.
- *Ampère's law symmetry choice.* Just like Gauss's law, the symmetry-recognition skill is harder than the calculation. Students apply Ampère in inappropriate geometries.
- *Infinite-vs-finite solenoid.* B = μ₀nI for the interior of an ideal infinite solenoid only. Real solenoids have ends; students forget.
- *Force between parallel wires direction.* "Parallel currents attract; antiparallel repel." The intuition is the *opposite* of Coulomb (like charges repel). The reason: the cross-product structure of the magnetic force. Worth slow explanation.

**Analogies and framings that work:**
- *Magnetic field lines as river currents around the source* — for circular B around a straight wire, the river-around-a-rock image works.
- *Biot-Savart as 'crumbs from the current trail'* — each d**ℓ** contributes a crumb of field at distant points, and you sum the crumbs.
- *Ampère's law as a 'circulation thermometer'* — the integral around a loop measures how much current threads the loop, exactly the way Gauss's law measured how much charge is enclosed.

**Exercises that build the target skill:**
- *Field at the center of a square loop* (Bloom: Apply) — use Biot-Savart with four straight segments. Tests integration and symmetry.
- *Force per length between two wires* (Bloom: Apply) — derive 2 × 10⁻⁷ N/m for 1 A each at 1 m. Tests the pre-2019 ampere definition.
- *Solenoid inside vs. end* (Bloom: Analyze) — given a finite solenoid, find B at center and at one end, compare to μ₀nI. Tests the finite-vs-infinite distinction.
- *Toroid for a fusion reactor* (Bloom: Apply + Synthesize) — given a toroid with major radius R and minor radius r, find B at the center of the cross-section, and compute the volume integral of u_B = B²/(2μ₀). A nice gateway to plasma confinement.

---

## F. Library files relevant to this chapter

None directly relevant.

---

## G. Gaps and flags

- FLAG: The chapter must explicitly handle the 2019 SI ampere redefinition. Many older textbooks still teach only the 1948 definition. Recommend: present both, explain why the change happened, point to NIST.
- FLAG: Magnetic monopoles — the chapter should mention the search briefly but not dwell. ∇·**B** = 0 is empirically true to extraordinary precision; the chapter teaches this as a foundational fact while acknowledging it's "the experimental result of no monopole detection."
- GAP: A worked example of B-field computation by *direct Biot-Savart integration* in a geometry that lacks Ampère-friendly symmetry (e.g., a half-infinite wire, a finite straight segment). The chapter should include this to show that Biot-Savart is the general-purpose tool when Ampère doesn't work.
