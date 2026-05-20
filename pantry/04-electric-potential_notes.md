# Research Notes: Chapter 04 — Electric Potential

**Source:** TIKTOC.md chapter entry (Chapter 04)
**Notes file:** 04-electric-potential_notes.md
**Corresponding chapter:** chapters/04-electric-potential.md (not yet written)
**Generated:** 2026-05-16

---

## Chapter summary (from TIKTOC.md)

Electric potential is the scalar companion to the vector electric field. It is defined through work: the potential difference between two points is the work per unit charge done against the electric force in moving a test charge between them. Because the electrostatic force is conservative, this work is path-independent — a fact with bite, because it is *not* derivable from Gauss's law alone. The potential is always easier to compute than the field (sum N scalars, not N vectors), and **E** can be recovered from V by taking the gradient. This chapter establishes V for point charges, dipoles, and continuous distributions, and introduces equipotential surfaces. The simulation renders equipotential lines and the electric field as their orthogonal gradient — making the V↔E relationship visually immediate.

**Where Ch 04 sits in Act One:** Ch 03 (Gauss's law) gave us the *divergence* equation ∇·**E** = ρ/ε₀ and the integral flux law. Ch 04 gives us the *curl* equation ∇×**E** = 0 — equivalent, in electrostatics, to "**E** is the gradient of a scalar." Both are needed to fully specify electrostatics; neither implies the other. Ch 05 (Capacitance) will use V = Q/V on the conductors at fixed potential to define C, and will use V differences to motivate why energy ½CV² is stored in the field.

---

## A. Conceptual foundations

### Why a scalar potential exists at all: conservative forces

The single fact this chapter rests on is: **the electrostatic force on a test charge is conservative.** That means the work done moving a charge from point A to point B is independent of the path between them. Equivalently, the work done around any closed loop is zero. Equivalently — and this is the form that connects to Ch 03 — the curl of the electrostatic field vanishes everywhere:

∇ × **E** = 0    (electrostatics)

The proof for a point charge is geometrically clean. The field of a point charge points radially outward and depends only on r. Any path from A to B can be decomposed into radial steps (which contribute **E**·d**l** = E_r dr) and tangential steps (which contribute zero, because **E** ⊥ d**l** there). The radial contributions integrate to k q (1/r_A − 1/r_B), which depends only on the endpoints. Done.

By superposition, the field of any static distribution of charges is a sum of point-charge fields, each of which is conservative. The sum of conservative vector fields is conservative. So *every* electrostatic field is conservative.

**The crucial pedagogical point:** ∇·**E** = ρ/ε₀ (Gauss) and ∇×**E** = 0 (curl-free) are *independent* statements about **E**. Gauss tells you about the sources; curl-free tells you about path-independence. Both are needed. A field with the right divergence but the wrong curl (a field that "rotates" in some region) is not an electrostatic field. The two equations together, with appropriate boundary conditions, uniquely determine **E** (Helmholtz decomposition).

Once you have a curl-free vector field on a simply-connected region, a theorem of vector calculus (the Poincaré lemma, or the fundamental theorem for gradients) guarantees that the field is the gradient of a scalar function. We give that scalar function a name:

**E** = −∇V

The sign is conventional but consequential: with the minus sign, V is the potential energy per unit charge, and a positive charge "rolls downhill" in V toward lower potential — toward smaller U.

**Common misconception (PER-documented):** that ∇×**E** = 0 follows from Gauss's law. It does not. Gauss is one of Maxwell's four equations; the curl-free condition (in electrostatics) is a separate fact that comes from the inverse-square radial form of the Coulomb force. In magnetostatics, ∇·**B** = 0 (a divergence statement) and ∇×**B** = μ₀ **J** (a curl statement) together play the same dual role. The book's Act Two will make this parallel explicit.

**Source:** Griffiths, *Introduction to Electrodynamics*, 4th ed., §2.3.1; Jackson, *Classical Electrodynamics*, 3rd ed., §1.5.

### Electric potential: definition through work

The work done by the electric force on a test charge q₀ moving from A to B is

W_{A→B} = ∫_A^B **F** · d**l** = q₀ ∫_A^B **E** · d**l**

Because the force is conservative, define the **electric potential energy** U such that W_{A→B} = −ΔU = −(U_B − U_A) = U_A − U_B.

Divide by q₀ to get a property of *the field*, not the test charge:

**Electric potential** V at a point is the potential energy per unit charge:

V = U / q

Equivalently, the **potential difference** between two points:

V_A − V_B = −∫_A^B **E** · d**l** = ∫_B^A **E** · d**l**

Units: J/C = volt (V). One volt is one joule of work per coulomb of charge moved between the two points.

**Reference point.** Only differences are physically meaningful. The constant of integration ("zero of V") is conventional. For isolated finite charge distributions, the natural choice is V(∞) = 0. For circuit problems, the natural choice is "ground." For an infinite line charge (where V → ∞ at infinity), pick a finite reference radius. The chapter must hammer this point: changing the reference shifts V everywhere by a constant but changes no observable.

**Common misconception:** that V at a point has absolute physical meaning. It does not — only ΔV does. The chapter should propose: "If I add 1,000,000 V to V everywhere in this room, what changes about the physics?" Answer: nothing. The fields are the same. The forces are the same. The currents are the same.

**Source:** Griffiths §2.3.2; Serway & Jewett Ch. 25; Halliday-Resnick-Walker Ch. 24.

### Potential from a point charge: V = kq/r

For a point charge q at the origin, integrate **E** = (kq/r²) **r̂** from infinity radially inward:

V(r) = − ∫_∞^r (kq/r'²) dr' = kq/r

(with V(∞) = 0). The result falls off as 1/r, not 1/r² like the field. This is the energetic analogue of the gravitational potential −GM/r and emerges from the same mathematical fact: integrating an inverse-square law along a radial path gives an inverse-linear function.

For a system of point charges, **V superposes as a scalar**:

V_total(**r**) = Σ_i k q_i / |**r** − **r**_i|

This is the chapter's central computational selling point. For N point charges, you compute N scalars (each a distance, a divide, a multiply) and add them. To get the field at the same point you would compute N vectors (each a distance, a divide, a multiply, *plus* three components to track), and add them vectorially. Scalars are easier than vectors at every step. Then differentiate V to get **E** if you actually need the field.

**Worked example reasoning — N=2 dipole-like check:** Two equal positive charges +q at (±a, 0). At the midpoint between them, V = 2kq/a (just sum two scalars). The field at the midpoint is zero by symmetry. The two facts are not contradictory: V is high (positive contribution from both charges), but its gradient is zero at the saddle point of the V landscape, so **E** = −∇V = 0. *Potential and field at the same point have no fixed relationship beyond the derivative.*

**Common misconception:** that V is a vector. The phrase "potential field" sometimes leads students to imagine V as having a direction. It does not. V is a scalar function of position. The vector quantity is **E**, which is the negative gradient of V.

### Equipotential surfaces

An **equipotential surface** is the locus of points where V takes a single value. Three properties follow immediately:

1. **Work done moving a charge along an equipotential is zero.** No ΔV, so no ΔU. (Useful for orbit-energy arguments and for understanding why a sliding conductor doesn't dissipate against the electric force.)

2. **Field lines are perpendicular to equipotentials.** The gradient of a scalar is perpendicular to its level sets — geometric fact from multivariable calculus. So **E** = −∇V is perpendicular to surfaces of constant V.

3. **The surface of a conductor in electrostatic equilibrium is an equipotential.** Inside a conductor in equilibrium, **E** = 0 (Ch 03), so V is constant throughout the conductor. The surface of the conductor is part of that constant-V region.

Concrete equipotential geometries the chapter should sketch:

- **Single point charge:** concentric spheres centered on the charge. Closer spheres → higher |V|. Spacing tightens near the charge (V ~ 1/r → equally-spaced V values give tighter geometric spacing).
- **Two equal positive charges:** at large distance, nearly spherical around the centroid (the pair looks like a single 2q). Close in, two egg-like surfaces around each charge that merge through a "neck" between them. The saddle point between the charges is a critical point of V where **E** = 0.
- **Two opposite charges (electric dipole):** hyperbolic-like equipotentials. One family wraps around the positive charge, one around the negative. The plane perpendicular to the dipole axis through the midpoint is the V = 0 equipotential (by symmetry — equal contributions of opposite sign cancel).
- **Parallel plates (uniform field region):** planes parallel to the plates. V varies linearly between them: V(z) = V_plate − E z.
- **Conducting sphere of radius R, charge Q:** spheres outside (V = kQ/r); the conductor itself, including its surface, at constant V = kQ/R.

**Source for visual catalog:** Griffiths Figure 2.34 (equipotential maps for dipole and parallel plates); Serway & Jewett §25.4 figures.

### Recovering **E** from V: the gradient

In one dimension, **E** = −dV/dx. In three dimensions:

**E** = −∇V = −(∂V/∂x **x̂** + ∂V/∂y **ŷ** + ∂V/∂z **ẑ**)

In spherical coordinates with spherical symmetry (V depends only on r):

E_r = −dV/dr

For the point-charge potential V = kq/r:

E_r = −d(kq/r)/dr = kq/r²

— recovering Coulomb's law for the field. The fact that −d(1/r)/dr = 1/r² is the algebraic reason V drops one power slower than E.

**Numerical gradient (used by the simulation):** central differences,

∂V/∂x ≈ [V(x+h, y) − V(x−h, y)] / (2h)

Accuracy: second-order in h. Trade-off: smaller h → more truncation accuracy but more roundoff from cancellation, and finer grid → more memory. For the simulation, h is the grid spacing — typically a fraction of the canvas size.

### Potential of continuous distributions: V = ∫ k dq / r

For a continuous distribution with charge density λ (line), σ (surface), or ρ (volume), the potential at a field point **r** is

V(**r**) = k ∫ dq / |**r** − **r**'|

where **r**' is the source point and the integral runs over the entire distribution. This is a scalar integral — one number to evaluate at each field point — and is the computational workhorse for distributions that don't have the high symmetry Gauss's law needs.

Two canonical evaluations the chapter will work through:

1. **Uniformly charged ring of radius R, total charge Q, on the symmetry axis (x-axis):**

   Every element dq of the ring is at the same distance √(x² + R²) from the field point (x, 0, 0). The integral collapses to scalar multiplication:

   V(x) = kQ / √(x² + R²)

   Differentiate to get the on-axis field:

   E_x(x) = −dV/dx = kQx / (x² + R²)^(3/2)

   — exactly the result Ch 02 obtained by direct vector integration of dE_x = (k dq / r²) cos θ. Two routes, same answer. The potential route is shorter because the cos θ vector projection that complicated the Ch 02 integral is gone — it has been absorbed into the gradient.

2. **Uniformly charged disk of radius R, total charge Q, on the symmetry axis:**

   Decompose into nested rings, integrate the ring result over R from 0 to R_disk:

   V(x) = (Q / 2πε₀ R²) [√(x² + R²) − |x|]

   (where R here means R_disk in the bracket). At x = 0 the result reduces to V = σR/(2ε₀) where σ = Q/πR². As R_disk → ∞ at fixed σ, this becomes a result for an infinite plane (after some care about reference points).

The deep point: many cases that are hard with vector integration become tractable with scalar integration plus a gradient. This is the chapter's payoff.

### Potential energy of a system of charges

The energy required to assemble a configuration of charges, bringing them in one at a time from infinity, is

U = Σ_{i < j} k q_i q_j / r_{ij}

The sum is over distinct pairs (each pair counted once, hence i < j). For three charges, three pairs; for N charges, N(N−1)/2 pairs.

This is the *interaction energy* of the configuration. It is positive when charges of the same sign are brought close (work was done against repulsion); negative when opposite charges are brought close (the field did work on you).

**Worked example reasoning — three charges in a triangle:** Three charges q_1, q_2, q_3 at the vertices of a triangle with sides r_{12}, r_{13}, r_{23}.

U = k (q_1 q_2 / r_{12} + q_1 q_3 / r_{13} + q_2 q_3 / r_{23})

Equilateral triangle with three +q charges at side a: U = 3kq²/a. All terms positive — net repulsive configuration; you had to do positive work to assemble it. That energy can be recovered, e.g., as kinetic energy if the charges are released.

**Common misconception:** double-counting pairs. Students sometimes write Σ_i Σ_j (sum over all i and all j), then either forget to divide by 2 or include i = j (which is nonsensical). The clean prescription is "sum over pairs, each pair once."

**Source:** Griffiths §2.4; Serway & Jewett §25.3.

### The electron-volt

When ε is the natural energy scale (work done on an electron crossing 1 V of potential), use the eV. The exact conversion (2019 SI redefinition fixed e):

1 eV = 1.602176634 × 10⁻¹⁹ J

(CODATA; the elementary charge is now defined to be this value exactly.)

**Scale chart for eV across physics:**

| Domain | Energy scale | In eV |
|---|---|---|
| Brownian / thermal at 300 K | k_B T | 0.026 eV (~25 meV) |
| Visible photon | hν, 400–700 nm | 1.8–3.1 eV |
| Hydrogen ionization (Rydberg) | 13.6 eV | 13.6 eV |
| Chemical bond | ~few eV | 1–10 eV |
| X-ray photon | hν | keV |
| Nuclear binding per nucleon | ~8 MeV | 8 × 10⁶ eV |
| Pion mass-energy | m_π c² | ~140 MeV |
| Proton mass-energy | m_p c² | 938 MeV |
| LHC beam (each, 2022 Run 3) | per particle | 6.8 TeV = 6.8 × 10¹² eV |
| Highest cosmic ray observed (Amaterasu, 2023) | 244 EeV ≈ 2.4 × 10²⁰ eV | ~10²⁰ eV |

The eV spans roughly 22 orders of magnitude in physics. The unit's usefulness is exactly that: a single scalar that names the relevant energy in any domain where one charged particle is doing one job.

**Sources:**
- CODATA 2018 values, fixed in 2019 SI redefinition: BIPM, *The International System of Units (SI)*, 9th ed. (2019).
- LHC operational parameters: CERN, "LHC Run 3" (2022), https://home.cern/news/news/accelerators/lhc-run-3-physics-record-energy
- Amaterasu cosmic ray: Telescope Array Collaboration, Fujii et al., *Science* 382, 903 (2023). https://doi.org/10.1126/science.abo5095

### Connection to Ch 03 (Gauss's law) and Poisson's equation

Combine the divergence of **E** = −∇V with Gauss's law:

∇·**E** = −∇·(∇V) = −∇²V = ρ/ε₀

→ **Poisson's equation:**

∇²V = −ρ/ε₀

In charge-free regions (ρ = 0):

**Laplace's equation:** ∇²V = 0

This is the workhorse of mid-level E&M: every boundary-value problem (specify V on conductor surfaces, solve for V in the empty region) reduces to solving Laplace's equation with boundary conditions. Method of images, separation of variables, conformal mapping — all are techniques for solving Laplace's equation. Out of scope for an intro chapter, but the chapter should *name* Poisson/Laplace and locate the territory.

**Source:** Griffiths §2.3.4 and Ch. 3 entire.

---

## B. Domain examples and cases

### Case 1: ECG and the body as a leaky volume conductor

An electrocardiogram measures potential differences on the skin produced by the depolarization-repolarization cycle of cardiac muscle. The heart generates a time-varying electric dipole (vector cardiogram); the body, as a conducting medium, transmits potential changes from the heart to the skin where electrodes pick them up. Limb leads (I, II, III) and chest leads together produce the standard **12-lead ECG**, each lead a different "view" of the cardiac dipole vector.

Voltage scale: ECG peaks (R wave) are typically 0.5–2 mV at the skin. The QRS complex represents ventricular depolarization; the T wave, repolarization. The clinical interpretation maps changes in the dipole vector (axis deviation, ST elevation/depression) to physical events in cardiac tissue.

The physics: at the skin, you are measuring V_A − V_B between two electrodes. The heart-as-dipole approximation (Einthoven triangle) treats the limb leads as forming an equilateral triangle whose projection of the cardiac dipole gives the lead voltages. The 12-lead clinical standard goes further with augmented and precordial leads, but every reading is a potential difference at a moment in time.

**Source:** Malmivuo & Plonsey, *Bioelectromagnetism: Principles and Applications of Bioelectric and Biomagnetic Fields*, Oxford University Press (1995), Ch. 15–18 (open online: http://www.bem.fi/book/).

### Case 2: EEG and brain potentials at the scalp

EEG (electroencephalography) records the same kind of potential difference, but the source is now extracellular currents from synchronized pyramidal-neuron populations in the cortex. Voltage scale at the scalp: 10–100 μV — roughly 100× smaller than ECG, because the source dipoles are smaller, deeper, and partially canceled by the skull's low conductivity.

The scalp signal is a smoothed, distance-attenuated projection of cortical V differences. Standard 10–20 electrode placement; clinical EEG has been a workhorse since Berger's first recording in 1924. Modern brain-computer interfaces (BCIs) extract motor imagery and attention signals from EEG with millisecond timing — at the cost of poor spatial resolution (~cm at best). The trade-off between EEG (excellent time, poor space) and fMRI (poor time, mm space) is itself a clean illustration of measurement physics.

**Source:** Niedermeyer & Lopes da Silva, *Electroencephalography: Basic Principles, Clinical Applications, and Related Fields*, 7th ed. (2018); Hari & Puce, *MEG-EEG Primer*, Oxford (2017).

### Case 3: Cell membrane potential and the Nernst equation

Every cell maintains a potential difference across its membrane, with the inside negative relative to the outside. The resting potential of a neuron is about −70 mV (cell interior negative). This is *not* a static-electric phenomenon in the Ch 01–Ch 04 sense — it is sustained by metabolically driven ion pumps and selective membrane permeability.

The physics that connects to this chapter: at electrochemical equilibrium for a single permeable ion species, the membrane potential is given by the **Nernst equation:**

E_ion = (RT / zF) ln([ion]_out / [ion]_in)

where R is the gas constant, T temperature, z the ion's charge, F the Faraday constant. The derivation: balance the electrical work qE_ion against the chemical work of moving an ion against a concentration gradient (kT ln(c_out/c_in) per particle, scaled by Avogadro's number).

For K⁺ at body temperature (310 K), with [K⁺]_in ≈ 140 mM, [K⁺]_out ≈ 5 mM:

E_K = (8.314 × 310 / (1 × 96485)) ln(5/140) ≈ 0.0267 × (−3.33) ≈ −89 mV

So the K⁺ equilibrium potential is about −89 mV — the membrane potential at which K⁺ flux is zero. Real resting potential (−70 mV) is offset because the membrane is partially permeable to other ions (Na⁺, Cl⁻); use the Goldman-Hodgkin-Katz equation for the full multi-ion result.

**The bridge to Ch 04 physics:** a 70 mV potential across a ~7 nm membrane is a field of ~10⁷ V/m. That is within an order of magnitude of dielectric breakdown for typical insulators — biology runs membranes at extreme field strengths because the membrane is engineered (lipid bilayer plus protein channels) to handle it without breakdown.

**Source:** Hille, *Ion Channels of Excitable Membranes*, 3rd ed., Sinauer (2001), Ch. 1–2; Hodgkin & Huxley, *J. Physiol.* 117, 500 (1952) — the original action-potential paper.

### Case 4: Battery terminals as a maintained ΔV

A 1.5 V AA battery, by definition, maintains 1.5 J of work per coulomb of charge moved through an external circuit from the + terminal to the − terminal. Chemistry maintains the potential difference; the battery is *not* a charge reservoir in the capacitor sense, but a controlled-ΔV source that pumps charges against the external load's field.

Useful translation: a fresh AA delivers ~2,500 mAh of capacity at ~1.5 V → ~13,500 J of stored chemical energy. Compare to the 200 J of an AED capacitor: a single AA holds ~70× more energy. But the AA cannot release it in milliseconds — its internal resistance limits the rate. The AED's value is the speed of delivery, not the total stored energy. This is the same trade-off as supercapacitor vs. battery (Ch 05).

### Case 5: Particle accelerators — voltage as energy currency

The cleanest demonstration of "voltage is energy per charge" is a linear accelerator. Apply a potential difference ΔV across a gap; an electron (charge −e) crossing the gap gains kinetic energy eΔV. Stack many such gaps with synchronized RF and you get arbitrary kinetic energies, limited by the practical engineering of voltage and length.

- **CRT TV electron gun (historical):** electrons gain ~25 keV. Speeds ~30% c (relativistic corrections start to matter).
- **Cathode-ray oscilloscope:** ~1–10 kV. Below 1% relativistic correction.
- **Medical X-ray tube:** ~50–150 keV. Bremsstrahlung off a tungsten anode gives the X-ray spectrum.
- **Linear accelerator (linac) for radiation therapy:** ~6–25 MeV electrons. Highly relativistic.
- **Stanford Linear Accelerator (SLAC):** 50 GeV electrons before shutdown in 2008. The world's first linac at GeV scale.
- **LHC beam energy (2022 Run 3):** 6.8 TeV per proton. Center-of-mass collision energy 13.6 TeV — the highest controlled energy per particle ever produced on Earth.

In all cases, the formula is the same: ΔKE = q ΔV. The eV is the energy unit because the relevant ΔV (per gap or per acceleration stage) is what physics talks in. Particle physicists describe particles by their energy in eV because that energy was *given to them* by potential differences. The unit is literally a record of how the particle was made.

**Source:** CERN, *LHC machine* (2022 Run 3 operational parameters), https://home.cern/topics/large-hadron-collider; Wille, *The Physics of Particle Accelerators*, Oxford (2000).

### Case 6: HVDC transmission and grid potential

Modern long-distance electric transmission increasingly uses **high-voltage DC (HVDC)** at megavolt scale. The Changji–Guquan UHVDC line in China (commissioned 2019) operates at ±1100 kV (2.2 MV terminal-to-terminal) over 3,300 km. Why DC at such high V? Because power transmitted = V × I and resistive losses go as I² R. For a given P, doubling V halves I and cuts resistive losses by 4×. The trade-off is the cost of DC-AC conversion at each end (massive thyristor or IGBT converter stations).

The physics is the same as in this chapter — ΔV drives current through a load, and energy = q ΔV per coulomb delivered. The engineering complication is the megavolt scale, which forces real attention to dielectric breakdown of air (Ch 03 limits) and the failure modes of insulators in real weather.

**Source:** Andersen, B. R., "Topologies for VSC transmission," IEEE PES (2019); for Changji–Guquan: Liu et al., *IEEE Trans. Power Delivery* 34, 1685 (2019).

### Failure case 1: equipotential on a finite rod's end

Students who learn "conductor surfaces are equipotentials" sometimes generalize to "any charged surface is an equipotential." A *charged insulator* (e.g., a uniformly charged plastic rod) is not an equipotential surface — charges cannot rearrange to equalize V on it. The rod's potential varies along its length because the geometry of distances to other parts of the rod varies. Only when charges are *free to move* does the equilibrium argument force V to be constant. The clean rule: **conductor in equilibrium → equipotential. Insulator → no such guarantee.**

### Failure case 2: a uniformly polarized sphere — V is not what you guess

A common student trap: treat a polarized (not charged) sphere as if it were a uniformly charged sphere. The polarization gives rise to bound surface charges, but the volume bound charge density is zero for uniform polarization. The resulting V outside is a pure dipole field (V = k p cos θ / r²), not 1/r. The geometry of the source matters. This case shows up in Ch 05 (dielectrics) but is worth flagging here.

---

## C. Connections and dependencies

**Prerequisites (what reader must already know):**

- Ch 01–02: Coulomb's law, electric field of a point charge, superposition principle, field-line picture
- Ch 03: Gauss's law in integral form, the divergence picture, conductors in equilibrium (E = 0 inside)
- Calculus: line integrals, gradient operator, partial derivatives. The chapter introduces ∇ as "gradient of a scalar field" — if the student has not seen ∇ outside a math class, the chapter must define it.
- Mechanics (prior course): work-energy theorem, potential energy for conservative forces (the gravitational analogue −GMm/r).

**Unlocks (what this chapter makes possible):**

- Ch 05 (Capacitance and Dielectrics): C is defined as Q/V; energy ½CV² uses V from this chapter; the energy density ½ε₀E² is recoverable by translating V into E via the gradient
- Ch 06 (Current and Resistance): Ohm's law V = IR uses ΔV directly; the chapter on circuits assumes the student is fluent in V differences across components
- Ch 07 (DC Circuits): Kirchhoff's voltage law is V around any loop = 0, which is just ∮**E**·d**l** = 0 — the curl-free statement of this chapter dressed in circuit-engineering clothes
- Ch 10 (Faraday): ∮**E**·d**l** ≠ 0 when **B** changes — Faraday's law is precisely the *breakdown* of this chapter's curl-free condition when fields are time-varying. The framing must be in place for the breakdown to mean something.
- Ch 11 (Maxwell): Poisson's equation ∇²V = −ρ/ε₀ is the static special case; the full wave equation for V in a gauge is its generalization

**Adjacent chapter connections:**

- Ch 03 (Gauss): divergence side of electrostatics; this chapter is the curl side. The two are complementary, not redundant. The simulation in this chapter explicitly shows ∇V on the same canvas as the equipotentials — making the gradient relation concrete.
- Ch 05 (Capacitance): the chapter immediately downstream. The capacitor formula C = ε₀ A/d is derived by computing V for a known σ on parallel plates, using exactly the techniques of this chapter.

---

## D. Current state of the field

**Settled:**

- The mathematics of the scalar potential and gradient relation is exact and uncontested at the intro level
- Equipotential-surface visualizations are a standard pedagogical tool; computational rendering (D3 contour generators, MATLAB contour plots) is mature and the methods have not changed materially in decades
- The eV as energy unit: redefined exactly in 2019 SI as 1 eV = 1.602176634 × 10⁻¹⁹ J, no longer subject to measurement uncertainty
- Volta's historical priority for the voltaic pile (1800) and the volt being named after him (1881, at the International Electrical Congress in Paris) — confirmed in primary historical sources

**Contested or emerging:**

- Brain–computer interfaces (BCI): rapid progress over the last 3 years in EEG and intracortical-electrode-based decoding (Neuralink first human implant 2024; non-invasive BCIs at sub-millivolt scalp resolution have crossed thresholds for typing applications). The voltage physics is settled; the engineering is the news.
- Cosmic-ray energies: the Amaterasu particle (244 EeV, observed 2021, reported 2023) is at the upper edge of observed cosmic-ray energies. The "energy" here is exactly the kind defined by a potential-difference traversal — though no human-built accelerator could produce such a particle. Source unknown; one of the major open questions in astroparticle physics.
- Optogenetic and voltage-sensitive-dye recording (subcellular): allows measurement of neural membrane potentials at single-cell, sub-millisecond resolution using fluorescent probes whose emission depends on local V. This is changing neuroscience; the underlying physics is the same membrane potential covered in Case 3.
- HVDC transmission: ±1100 kV is the current commercial maximum; multi-megavolt systems under design. Limits set by dielectric breakdown engineering, not by physics principles.

**Key references:**

1. Griffiths, D. J. *Introduction to Electrodynamics*, 4th ed. (2017), §2.3. The cleanest undergraduate treatment of potential, with the curl-free derivation and Poisson/Laplace setup. The book this chapter is in lockstep with.
2. Serway, R. & Jewett, J. *Physics for Scientists and Engineers*, 10th ed., Ch. 25 (Electric Potential). The intro-physics presentation; worked examples are well-engineered.
3. Halliday, D., Resnick, R. & Walker, J. *Fundamentals of Physics*, 11th ed., Ch. 24. The clearest pedagogical worked examples; sets the standard for "scalar superposition" framing.
4. Singh, C. "Student understanding of symmetry and Gauss's law of electricity." *Am. J. Phys.* 74, 923 (2006). Touches on V/E confusion; arXiv:1602.07376.
5. Pollock, S. J. & Singh, C. "Student difficulties with the electric field and electric potential in introductory physics." *Phys. Rev. Phys. Educ. Res.* (various 2008–2023). The PER literature on the V/U/E confusion is large and consistent.
6. BIPM, *The International System of Units (SI)*, 9th ed. (2019). The eV is now derived from the exactly-defined e.
7. Volta, A. "On the Electricity excited by the mere Contact of conducting Substances of different kinds." *Philosophical Transactions of the Royal Society of London* 90, 403 (1800). The original voltaic-pile paper. https://doi.org/10.1098/rstl.1800.0018
8. Pancaldi, G. *Volta: Science and Culture in the Age of Enlightenment*, Princeton University Press (2003). The definitive Volta biography.

**Recent developments (last 3 years):**

- Telescope Array Collaboration, *Science* 382, 903 (2023): the Amaterasu cosmic-ray observation pushing the upper end of the eV-scale chart.
- LHC Run 3 began July 2022; per-beam energy 6.8 TeV. Source: CERN news, https://home.cern/news/news/accelerators/lhc-run-3-physics-record-energy
- Neural recording at the single-cell level with voltage-sensitive fluorescent indicators: see Adam et al., *Nature* 569, 413 (2019) and subsequent papers — pushing the spatial resolution of "V at a point in biology" by orders of magnitude.

---

## E. Teaching considerations

**Where students get stuck (PER-documented):**

1. **V vs. U confusion.** Potential V is intensive (J/C, per unit charge — a property of the field at a point). Potential energy U is extensive (J, depends on which test charge sits at that point). The relation is U = qV. Students who treat the two as synonyms make sign errors and units errors throughout. The chapter must commit, early and explicitly: *V is a property of the field; U is a property of a charge in the field.*

2. **V treated as a vector.** Because students see "electric potential" alongside "electric field" (which is a vector), they import vectorness into V. The cure is repetition: V is a *scalar*. Equipotential surfaces are the visual cure — they make V look like an altitude map, and altitudes are scalars.

3. **Reference point confusion.** "Is V positive or negative at this point?" only has an answer relative to a chosen reference. Students who treat V as having an absolute value get tangled when problems shift the reference. The chapter's framing: only ΔV matters; the reference is just a bookkeeping choice.

4. **Sign confusion between W, ΔU, ΔV, q.** The cascade W_{field on q} = −ΔU = q(V_A − V_B) = −qΔV with ΔV = V_B − V_A has four sign-bearing quantities. A negative test charge "rolls uphill" in V to lower U. The cleanest cure: never memorize signs in the abstract; always check on a single physical setup (e.g., a positive charge released between parallel plates) and reason from energy conservation.

5. **"If V is positive, must E be positive?"** No — V and E have no fixed sign relationship at a point. **E** is the *gradient* of V, not V itself. A point can have high positive V and zero E (the midpoint between two equal positive charges; the center of a uniformly charged sphere). A point can have zero V and large E (the V = 0 plane between a dipole's two charges). The chapter must hammer this with worked counterexamples.

6. **Path-independence is invisible in symbolic notation.** Students see ∫**E**·d**l** and don't notice that the integral assumes path. They write the integral, evaluate it on a chosen path, and don't appreciate that the value is path-independent. The chapter should walk one example (point charge field, two different paths from A to B, same answer) to make path-independence visible.

7. **Scalar superposition vs. vector superposition.** Students who learned to add E-vectors sometimes forget to drop the vector machinery when adding V-scalars. They write V_total = (kq₁/r₁) **r̂**₁ + ... — wrong. *V is a scalar; no unit vectors.*

**Analogies and framings that work:**

- **Altitude / topographic map.** V is altitude; equipotentials are contour lines; **E** is the negative gradient (downhill direction, steepest). Hikers experience the analogy: high-altitude points have lots of gravitational potential energy per unit mass (= per unit "test mass" 1 kg); ridges are equipotentials. The analogy is exact for the V-U-E triad of electrostatics with gravitational potential, gravitational PE, gravitational field. The chapter should use this analogy and *name where it breaks down*: charges can be positive or negative (no "negative mass" in practice), so V can be positive or negative even when gravitational potential is bounded.

- **Water in a network of tanks.** ΔV is the pressure head between two tanks; current is the flow. Capacitance is the tank's cross-section. Useful for circuits in Ch 06–07 but the seed is here.

- **Energy bank account.** V is a quoted exchange rate (J per C); U is the actual balance for a specific account (with q coins in it). The reference V(∞) = 0 is "the exchange rate at the far-away reference market."

- **Field lines + equipotentials together = topographic map with arrows.** This is the simulation's framing. Once students see equipotentials and field arrows on the same canvas (and notice the arrows are always perpendicular to the contours), the gradient relation goes from abstract to immediate.

**Exercises that build the target skill:**

- **Scalar superposition** (Bloom: Apply) — given N point charges at known positions, compute V at K test points. No vectors. This is the chapter's bread-and-butter computational exercise.
- **Differentiate to get E** (Bloom: Apply) — given V(x) on a symmetry axis (e.g., the ring V = kQ/√(x²+R²)), find E_x = −dV/dx. Tests the gradient relation in one dimension.
- **Equipotential sketching** (Bloom: Analyze) — given a charge configuration, sketch equipotential surfaces and field lines. Tests the perpendicularity property and the "Where are the saddle points?" geometry.
- **Reference-shift test** (Bloom: Evaluate) — "Two students compute V at a point; one gets 50 V, the other gets −150 V. They are both correct. Explain how this is possible." Tests the meaning of the reference.
- **Three-charge assembly energy** (Bloom: Apply + Analyze) — compute U for three charges at triangle vertices; predict whether the configuration is bound or will fly apart on release. Tests the pair-sum and the energy-conservation linkage.

---

## F. Library files relevant to this chapter

None directly relevant. Shared MD library is non-physics.

---

## G. Gaps and flags

- **FLAG (curl-free decision).** The chapter has a choice: state ∇×**E** = 0 explicitly as a separate axiom from Gauss, or fold it into "the work is path-independent because the force is radial inverse-square." The latter is more concrete and probably right for intro level. The former is necessary for Ch 10 (Faraday) to make sense as a *modification* of this rule when fields change. Recommend: state path-independence in plain language in this chapter; flag a single sentence: "We will see in Ch 10 that this path-independence is broken when magnetic fields change with time. For now, electrostatic." Plant the seed without making it formal.

- **FLAG (Poisson/Laplace).** Naming Poisson's equation ∇²V = −ρ/ε₀ is honest and ties Ch 03 and Ch 04 together cleanly. But solving it is well out of intro scope. Recommend: name it in one sentence as the unifying equation, defer all solutions to later courses. Do not attempt method of images at this level.

- **FLAG (dipole potential V = k p cos θ / r²).** The TIKTOC lists this as a worked example. The derivation involves Taylor-expanding V = k[(q/r_+) − (q/r_−)] for a small dipole at large distance. This is doable but requires comfort with binomial expansion. Recommend: present the result and verify it numerically against a direct computation for one geometry, rather than derive it fully. The student should know the *form* (1/r² for a dipole, vs. 1/r for a monopole, vs. 1/r³ for a quadrupole) and what that means physically (higher multipoles fall off faster).

- **GAP (simulation accuracy at point charges).** A numerical contour plot of V near a point charge produces a singular spike. The simulation must either (a) cap V at some maximum for visualization, (b) use log-scale color mapping, or (c) exclude a small radius around each charge. Recommend (a) or (b); document the choice in the chapter so students see it as a *visualization* limit, not a physical claim about V at the singularity.

- **GAP (numerical gradient at the grid edge).** Central differences fail at the edges of the simulation canvas (no neighbor on one side). Use one-sided differences at edges or pad the grid. Worth noting in passing: real numerical work always has to handle boundaries.

- **GAP (eV-to-J conversion teaching).** The chapter should *explicitly* practice converting between eV and joules in both directions and across the scale chart. Students who memorize "1 eV ≈ 1.6 × 10⁻¹⁹ J" but never compute 13.6 eV in joules lose the scale intuition. Recommend at least one exercise that walks through "what is the kinetic energy in J of a 6.8 TeV LHC proton?" — answer: 1.09 × 10⁻⁶ J = ~ 1 μJ — about the energy of a mosquito in flight, concentrated in one proton.

- **FLAG (Volta historical dates).** Volta announced the voltaic pile in a letter to Joseph Banks, President of the Royal Society, dated 20 March 1800 (published in *Phil. Trans.* later that year). The "volt" was formally adopted as the unit of EMF at the 1881 International Electrical Congress in Paris. Both dates are well-established. No `[verify]` needed.

- **FLAG (Amaterasu cosmic ray).** The 244 EeV figure is from Telescope Array's reported 2021 detection, published 2023. Use this number, not the older ~3 × 10²⁰ eV figures from earlier "Oh-My-God" particles (Fly's Eye 1991). Both are real; use the more recent one for the upper end of the eV chart.

- **GAP (potential energy sign conventions in chemistry vs. physics).** Chemists report ionization energies as positive (13.6 eV for hydrogen — the energy you must add). Physicists writing V = kq/r and U = qV for a bound electron get U = −13.6 eV (negative because bound). Both are correct; they label different things. The chapter should briefly acknowledge this if it mentions chemistry-side numbers.

---

## Verified facts (used in chapter prose)

- **Volta and the voltaic pile:** Alessandro Volta announced the pile in a letter to Sir Joseph Banks, Royal Society, dated 20 March 1800. Published as Volta, A., "On the electricity excited by the mere contact of conducting substances of different kinds," *Philosophical Transactions of the Royal Society* 90, 403–431 (1800). DOI: 10.1098/rstl.1800.0018. ✓
- **Naming of the volt:** the volt was adopted as the SI unit of EMF/potential difference at the International Electrical Congress in Paris, 1881. (Confirmed: Pancaldi 2003; BIPM history.) ✓
- **1 eV = 1.602176634 × 10⁻¹⁹ J exactly** (2019 SI redefinition, where e is defined to be 1.602176634 × 10⁻¹⁹ C exactly). ✓
- **Rydberg / hydrogen ionization energy:** 13.605693 eV. ✓
- **LHC Run 3 per-beam energy:** 6.8 TeV (started July 2022). Source: CERN. ✓
- **Amaterasu cosmic ray:** 244 EeV ≈ 2.44 × 10²⁰ eV; Telescope Array, *Science* 382, 903 (2023). ✓
- **Resting membrane potential:** ~−70 mV typical for neurons. (Range −40 to −90 mV depending on cell type.) ✓
- **Nernst formula at body temperature for K⁺:** E_K ≈ −89 mV given typical intracellular/extracellular concentrations. ✓
- **ECG scale:** R-wave 0.5–2 mV typical at skin. ✓
- **EEG scale:** 10–100 μV typical at scalp. ✓
- **HVDC at ±1100 kV:** Changji–Guquan UHVDC line, commissioned 2019, China. ✓
