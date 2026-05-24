# TIKTOC.md — Physics +1: Electromagnetism
## A Simulation-First Calculus-Based Electromagnetism Textbook

**Working title:** Physics +1: Electromagnetism — Interactive Field Simulations with Claude and D3
**Series:** Physics +1 Series (Volume 3)
**Author:** Humanitarians AI · ni.brown@neu.edu · Bear Brown & Company
**Repo:** physics-plus-one-electromagnetism
**Version:** 1.0
**Status:** TIKTOC complete — ready for research gathering and chapter drafting

---

## Book Concept

This book teaches calculus-based electromagnetism — from Coulomb's law through Maxwell's equations and electromagnetic waves — to intro-physics students who have completed classical mechanics, by pairing each conceptual chapter with LLM-generated D3.js simulations that make invisible fields visible. It fills the gap left by Serway/Jewett and Halliday/Resnick (rigorous but static) and YouTube demos (visual but non-rigorous) by giving students interactive field visualizations they built themselves, governed by physics they understand, that they can modify at 11pm without asking anyone.

**The narrative arc is the one Maxwell completed.** The book begins with two apparently separate phenomena — electric charge at rest and magnetic compass needles — and ends with a single set of four equations whose consequence is that light is an electromagnetic wave. Every chapter is a step toward that unification. The student who finishes this book understands not just what Maxwell's equations say but why they are surprising.

**The +1 is the field visualization layer.** Every chapter ends with copy-paste-ready Claude prompts that produce interactive D3 visualizations: field line plotters, potential surface renderers, circuit animators, induction simulators. The fields are the point. An intro-physics student who has watched field lines bunch near a sharp conductor, seen how a changing magnetic flux drives current in a loop, and rendered a transverse EM wave has physical intuition that no amount of static diagrams can supply.

**Central thesis:** Electromagnetism is not hard because the math is hard. It is hard because the objects — electric and magnetic fields — have no direct sensory analogue, and students have no way to develop intuition for them without seeing them move and respond. Interactive field simulation closes that gap.

---

## Book Type and Deployment

**Primary type:** Course textbook — adopted for a semester, chapter = roughly one week, read in sequence.

**Target course:** Second semester of calculus-based introductory physics. Sophomore level. Physics, engineering, and pre-med majors. Pairs with a mechanics first semester.

**Prerequisites assumed:** Calculus through multivariable (partial derivatives, line integrals, surface integrals — used but not derived from first principles), classical mechanics (Newton's laws, energy, momentum), algebra and trigonometry fluent.

**Prerequisite explicitly not assumed:** Vector calculus at the level of a dedicated math course. Gradient, divergence, and curl are introduced as needed, operationally, in the chapters where they appear.

**Semester format:** 15 weeks. Chapter 0 is assigned Week 1 alongside Chapter 1. Chapters 1–12 map to Weeks 1–12. Weeks 13–15 are review, lab integration, and final exam.

**What this book is not:** A graduate electrodynamics text. A pure computation course. A physics-free simulation course. A circuits/electronics course beyond the basics.

---

## The +1 System: How Simulations Work in This Book

Each chapter ends with an **LLM Exercise** block containing:

1. **The simulation prompt** — a copy-paste-ready four-move prompt (Show / Say / Constrain / Verify) that produces a working D3 field visualization for that chapter's core concept
2. **Exploration tasks** — specific parameter changes students make and questions they answer by watching the simulation
3. **Extension prompt** — a follow-up that adds one feature or connects to the next chapter's physics

Chapter 0 generates the three Brutalist governing files (`CLAUDE.md`, `DESIGN.md`, `PROJECT.md`) that travel with the student through the entire book.

---

## Three-Act Learning Arc

**ACT ONE — The Electric World (Chapters 1–5)**
*From "I know charge exists" to "I can compute the field and potential for any static charge distribution and understand how energy is stored."*
Coulomb's law → electric field → Gauss's law → electric potential → capacitance. The student builds physical intuition for the electric field as a real object before encountering circuits. The simulations make field lines and equipotential surfaces visible for any charge configuration the student chooses.

**ACT TWO — Current, Magnetism, and Induction (Chapters 6–10)**
*From "I know current flows" to "I understand that changing fields create fields — and that this is what makes a transformer work."*
Current and resistance → DC circuits → magnetism and magnetic force → sources of magnetic fields → electromagnetic induction and Faraday's law. Each chapter's simulation makes the field visible: current distributions, magnetic field lines around wires and loops, the induced EMF responding to a changing flux in real time.

**ACT THREE — Unification (Chapters 11–12)**
*From "I have two separate field theories" to "I understand why Maxwell added the displacement current and what it implies about light."*
Maxwell's equations as the unification of all preceding chapters → electromagnetic waves as their direct consequence → the capstone connecting E&M to modern physics (optics, antennas, wireless communication, quantum electrodynamics preview). The student who completes Act Three understands why the speed of light appears in Maxwell's equations and what that meant for physics.

---

## Chapter List

---

### CHAPTER 00 — How to Use the Simulations
**Filename:** `00-how-to-use-the-simulations.md`
**Arc position:** Pre-chapter / setup

**One-line:** Students build the three Brutalist governing files and produce their first E&M simulation — electric field lines from a point charge — before reading any new physics content.

**Chapter description:**
This chapter has one job: get the student from zero to a working, modifiable D3 electromagnetic field visualization before they encounter any new physics. It introduces Claude, the Brutalist system, and the four-move prompt structure through the simplest possible E&M object: a positive point charge and its electric field lines. By the end, the student has `CLAUDE.md`, `DESIGN.md`, and `PROJECT.md` in their working directory, a working field line simulation they can modify, and a clear mental model of how the LLM exercises in every subsequent chapter will work.

**Core concepts:**
- The Brutalist system: CLAUDE.md (coding constitution), DESIGN.md (visual constitution), PROJECT.md (project state)
- The four-move prompt structure: Show / Say / Constrain / Verify
- D3 v7 for field visualization: SVG canvas, vector field rendering, field line integration, parameter sliders
- The point charge as first simulation object: radial field, 1/r² falloff, field line density proportional to field strength
- The verification stack: format check, physics check (do field lines point away from positive charge?), browser test
- The instruction budget: why CLAUDE.md and DESIGN.md are separate files

**Key vocabulary:** electric field lines, field line density, D3, SVG, CLAUDE.md, DESIGN.md, PROJECT.md, four-move prompt, verification stack

**What the student builds:**
- `CLAUDE.md` — E&M simulation coding constitution (D3 v7, SVG canvas, vector field rendering, field line integration via RK4, slider-driven parameter updates)
- `DESIGN.md` — visual constitution (positive charge in red, negative in blue, field lines in dark gray, equipotentials in light green, field strength encoded in line density, dark-mode support)
- `PROJECT.md` — project state file (tracks simulations built, current chapter)
- `00-point-charge.html` — point charge field line visualizer with sliders for charge magnitude and sign; field lines radiate correctly; density shows field strength

**Simulation physics:**
Electric field of a point charge: **E** = (kq/r²) r̂. Field lines computed by numerical integration (RK4) starting from points on a small circle around the charge, following **E** at each step. Line density proportional to |q|. Sliders: charge magnitude q, number of field lines. Display: field lines as SVG paths, charge as colored circle.

**Color conventions for DESIGN.md (carried through all chapters):**
- Positive charges: red circles
- Negative charges: blue circles
- Electric field lines: dark gray (#444), 1.5px stroke
- Equipotential lines: green (#2a9d8f), 1px stroke, dashed
- Magnetic field lines: purple (#7b2d8b), 1.5px stroke
- Current direction: orange arrows
- Vector field arrows: scaled by magnitude, color-mapped blue→red for low→high
- Dark mode: all backgrounds to #1a1a1a, lines lighten by 40%

**LLM Exercise structure:**
Part 1: Generate CLAUDE.md (prompt provided)
Part 2: Generate DESIGN.md (prompt provided)
Part 3: Generate PROJECT.md (prompt provided)
Part 4: Build the point charge field line simulation (four-move prompt provided)
Part 5: Exploration tasks — flip the sign of the charge, double the magnitude, observe field line density
Part 6: Extension — add a second charge; watch field lines connect between opposite charges

**Connection to Chapter 1:** The field lines show a qualitative picture. Chapter 1 provides the quantitative law behind them.

---

### CHAPTER 01 — Electric Charge and Coulomb's Law
**Filename:** `01-electric-charge-coulombs-law.md`
**Arc position:** Act One, Chapter 1

**One-line:** Students learn what electric charge is, how like charges repel and opposite charges attract, and how to compute the force between point charges using Coulomb's law — building a simulation that shows the force vectors between multiple charges.

**Chapter description:**
The first physics chapter. It begins with the observation that matter comes in two electrical flavors and that these flavors interact. The historical anchor is Franklin's kite experiment (1752) and Coulomb's torsion balance (1785) — experiments that establish the qualitative and then quantitative law. Coulomb's law is the electric analogue of Newton's gravitational law: force proportional to product of charges, inversely proportional to distance squared. The superposition principle — that the total force on a charge is the vector sum of forces from all other charges — is established here and carries through the entire book. The simulation shows force vectors between a configurable set of point charges, with arrows scaled by magnitude and colored by whether they push or pull.

**Core concepts:**
- Electric charge: quantized, conserved, two signs; elementary charge e = 1.6×10⁻¹⁹ C
- Conductors vs. insulators: charges free to move vs. bound; surface charge on conductors
- Coulomb's law: **F** = k q₁q₂/r² r̂ where k = 8.99×10⁹ N·m²/C²
  - Inverse-square law: same mathematical structure as gravity
  - Vector form: direction along the line connecting charges
  - Superposition: **F**_total = Σ **F**ᵢ
- The permittivity of free space: k = 1/(4πε₀), ε₀ = 8.85×10⁻¹² C²/(N·m²)
- Charge conservation: total charge of an isolated system is constant
- Charge quantization: all charges are integer multiples of e (or e/3 for quarks, not observed free)
- Triboelectric effect, induction, grounding: how charge moves in practice

**Key vocabulary:** electric charge, Coulomb's law, permittivity, superposition principle, conductor, insulator, induction, grounding, triboelectric effect

**Common misconceptions:**
- "Positive charge means more charge, negative means less" — these are labels for two types, not amounts
- "Coulomb's law works for extended objects" — it is exact only for point charges; for distributions, integration is required
- "The force on a test charge is from the field, not from other charges" — both framings are correct; the field is a bookkeeping device for the force

**Worked examples:**
1. Two charges on a line: compute **F** on q₁ due to q₂ and q₃
2. Equilibrium problem: three charges in a line, find the position of q₃ such that the net force on it is zero
3. Continuous charge distribution preview: force on a test charge due to a uniformly charged rod (set up the integral, evaluate)

**What the student builds:**
`01-coulombs-law.html` — Coulomb force simulator. Controls: drag-and-drop point charges on a 2D canvas, set charge magnitudes (positive/negative slider). Display: force vectors on each charge (arrows scaled by magnitude, colored red for repulsion/blue for attraction); numerical force values shown; superposition illustrated by showing individual and total force vectors. Students can verify that equal and opposite charges attract along the connecting line.

**Simulation physics:**
For N charges at positions **r**ᵢ with charges qᵢ: force on charge j is **F**ⱼ = Σᵢ≠ⱼ k qᵢqⱼ (**r**ⱼ - **r**ᵢ)/|**r**ⱼ - **r**ᵢ|³. Render arrows at each charge position, scaled by |**F**|, direction along **F**. Color: repulsive (same sign) in warm red, attractive (opposite sign) in cool blue.

**Key references for research agent:**
- Serway & Jewett, *Physics for Scientists and Engineers*, Chapter 23
- Halliday, Resnick & Krane, *Physics*, Chapter 26
- History of Coulomb's torsion balance experiment (1785)
- Franklin's kite experiment: historical accuracy (was it really a kite?)
- Physics Education Research on student misconceptions about charge

**Bridge to Chapter 2:** Coulomb's law gives the force between charges. Chapter 2 introduces a cleaner way to think about how one charge influences space — the electric field — and shows how to compute it for any charge distribution.

---

### CHAPTER 02 — The Electric Field
**Filename:** `02-electric-field.md`
**Arc position:** Act One, Chapter 2

**One-line:** Students learn to think about electric influence as a field filling space, compute the electric field for point charges and simple distributions, and build a vector field visualizer that shows **E** at every point on a 2D grid.

**Chapter description:**
The electric field is the central object of electrostatics. Instead of asking "what force does charge A exert on charge B," the field formulation asks "what field does charge A create at every point in space, and what does that field do to any charge placed there?" This reframing is essential: it separates source from response, makes superposition clean, and sets up Faraday's later insight that the field itself is real and can carry energy. This chapter defines **E**, establishes the superposition of fields, introduces field lines as a visualization tool (with honest acknowledgment of their limitations), and derives the electric field for the most common charge distributions: point charges, dipoles, uniformly charged rings and disks, and the infinite plane. The simulation is a full 2D vector field renderer that draws **E** at every grid point for a user-configurable charge distribution.

**Core concepts:**
- The electric field definition: **E** = **F**/q₀ (force per unit test charge); units N/C = V/m
- Field of a point charge: **E** = kq/r² r̂
- Superposition of fields: **E**_total = Σ **E**ᵢ
- Electric field lines: tangent to **E** everywhere; density proportional to |**E**|; begin on +, end on −
  - Where field lines work: qualitative visualization for smooth distributions
  - Where field lines fail: they do not show field magnitude accurately in 3D projected to 2D
- Electric dipole: **p** = qd (dipole moment); field on axis and on perpendicular bisector; 1/r³ falloff
- Continuous charge distributions: linear (λ), surface (σ), volume (ρ) charge density; **E** = ∫ k dq/r² r̂
  - Uniformly charged ring: field on axis
  - Uniformly charged disk: field on axis; limit → infinite plane: **E** = σ/2ε₀ n̂
- Motion of a charged particle in a uniform **E** field: projectile-like motion

**Key vocabulary:** electric field, test charge, superposition, field lines, electric dipole, dipole moment, linear charge density, surface charge density, volume charge density

**Common misconceptions:**
- "Field lines show the path a charge would follow" — they show the direction of force at each instant; a moving charge follows a curved trajectory only if **E** is uniform
- "Denser field lines mean stronger force everywhere nearby" — only valid quantitatively in 2D; in 3D, field line density in a 2D cross-section is not simply proportional to field strength
- "The electric field exists only where there are charges" — the field exists at every point in space; charges are the sources

**Worked examples:**
1. Electric field on the axis of a uniformly charged ring: integrate λ dℓ contributions; result E = kQx/(x²+R²)^(3/2)
2. Electric dipole on its axis: two-charge superposition; show 1/r³ falloff far from dipole
3. Charged particle in a uniform field: electron enters at angle θ with speed v₀; find deflection (like projectile motion)

**What the student builds:**
`02-electric-field.html` — 2D electric field visualizer. Controls: drag-and-drop charges (positive/negative, adjustable magnitude); toggle between vector field view (arrows at grid points, scaled and color-mapped) and field line view (integrated paths). Display: vector field arrows showing **E** direction and magnitude; field lines from each charge. Students add charges and watch the field rearrange in real time.

**Simulation physics:**
At each grid point (x,y), compute **E** = Σᵢ kqᵢ(**r** - **r**ᵢ)/|**r** - **r**ᵢ|³. Render arrows scaled by log(1 + |**E**|) (log scale to show both weak and strong regions). Color map: blue (weak) to red (strong). Field lines: RK4 integration from starting points near each charge. Arrow density: 20×20 grid minimum.

**Key references for research agent:**
- Serway & Jewett, Chapter 23–24
- Griffiths, *Introduction to Electrodynamics*, Chapter 2
- History of field concept: Faraday's lines of force vs. action-at-a-distance debate
- Physics Education Research: student difficulties with superposition of fields
- Dipole fields in nature: water molecule polarity, antenna radiation

**Bridge to Chapter 3:** Computing **E** by superposition integral works but is laborious for symmetric distributions. Chapter 3 introduces Gauss's law — a much faster route to **E** for any distribution with sufficient symmetry.

---

### CHAPTER 03 — Gauss's Law
**Filename:** `03-gauss-law.md`
**Arc position:** Act One, Chapter 3

**One-line:** Students learn that the total electric flux through any closed surface equals the enclosed charge divided by ε₀, and use this to compute **E** for spherical, cylindrical, and planar symmetry — building a Gaussian surface visualizer.

**Chapter description:**
Gauss's law is the first of Maxwell's four equations, and it is the most powerful computational tool in electrostatics. For charge distributions with spherical, cylindrical, or planar symmetry, it reduces a difficult vector integral to an algebraic equation. This chapter derives Gauss's law from Coulomb's law (for students who want the justification) and then focuses on using it. The key skill is choosing the right Gaussian surface — a skill that requires physical reasoning, not just mathematics. The simulation lets students draw a Gaussian surface around an arbitrary charge distribution and watch the flux computed in real time as they resize and reposition the surface.

**Core concepts:**
- Electric flux: Φ_E = ∫∫ **E** · d**A**; physical meaning as "field lines crossing a surface"
- Gauss's law: Φ_E = Q_enc/ε₀ (integral form)
  - Equivalent to Coulomb's law for static charges (proof via solid angle argument)
  - General: valid for any closed surface, any charge distribution
- Choosing a Gaussian surface: symmetry determines the choice
  - Spherical symmetry → spherical Gaussian surface
  - Cylindrical symmetry → cylindrical Gaussian surface
  - Planar symmetry → pillbox Gaussian surface
- Applications:
  - Uniformly charged sphere (inside and outside): **E** = kQr/R³ r̂ (r<R); **E** = kQ/r² r̂ (r>R)
  - Infinite line charge: **E** = λ/(2πε₀r) r̂
  - Infinite plane: **E** = σ/(2ε₀) n̂ (confirms Chapter 2 result)
  - Conducting sphere: **E** = 0 inside; surface charge only
- Conductors in electrostatic equilibrium: **E** = 0 inside; charge on surface; **E** ⊥ surface outside
- Faraday cage: shielding by a conductor

**Key vocabulary:** electric flux, Gauss's law, Gaussian surface, enclosed charge, permittivity, conducting shell, Faraday cage, electrostatic shielding

**Common misconceptions:**
- "Gauss's law only works for symmetric distributions" — it is always true; symmetry only determines whether it is useful for computing **E**
- "The Gaussian surface must be a physical surface" — it is a mathematical construct; it need not coincide with any material boundary
- "E = 0 inside a conductor means there is no charge inside" — there can be charge inside a cavity; the field is zero inside the conductor material itself

**Worked examples:**
1. Field inside and outside a uniformly charged solid sphere: choose spherical Gaussian surface, apply Gauss's law at r<R and r>R
2. Field of an infinite line charge: cylindrical Gaussian surface, compute flux through end caps and curved surface
3. Conducting shell with internal point charge: field in three regions (r<a, a<r<b, r>b); charge distribution on inner and outer surfaces

**What the student builds:**
`03-gauss-law.html` — Gaussian surface flux visualizer. Controls: choose charge distribution (point charge, line charge, sphere); position and resize a Gaussian surface (circle in 2D representing a sphere or cylinder). Display: field lines from the charge distribution; the Gaussian surface shown as a closed curve; field arrows at the surface colored by their dot product with the outward normal (red for outward flux, blue for inward); total flux Φ_E computed numerically and displayed; Q_enc/ε₀ computed analytically and displayed for comparison. Students verify Gauss's law numerically for different surface positions and sizes.

**Simulation physics:**
For a 2D cross-section: compute **E** at N points on the Gaussian surface (circle). Compute Φ_E ≈ Σᵢ **E**ᵢ · n̂ᵢ Δℓᵢ (2D line integral as proxy for 3D surface integral). For a point charge: compare to Q/ε₀. Show that Φ_E is the same regardless of surface size (for a closed surface enclosing the charge) and zero for a surface that does not enclose the charge.

**Key references for research agent:**
- Serway & Jewett, Chapter 24
- Griffiths, Chapter 2 (section 2.2)
- Historical development: Gauss (1835, published 1867); relation to Coulomb
- Faraday cage: practical applications (MRI rooms, microwave ovens, car lightning safety)
- Physics Education Research on Gauss's law: student difficulties selecting Gaussian surfaces

**Bridge to Chapter 4:** Gauss's law gives **E** efficiently. Chapter 4 introduces a scalar quantity — the electric potential V — that is often easier to compute than **E** and from which **E** can be recovered by differentiation.

---

### CHAPTER 04 — Electric Potential
**Filename:** `04-electric-potential.md`
**Arc position:** Act One, Chapter 4

**One-line:** Students learn that the electric field is the gradient of a scalar potential, compute the potential for point charges and distributions, and build a potential surface visualizer showing equipotential lines and the **E** field as their gradient.

**Chapter description:**
The electric potential is the scalar companion to the vector electric field. It is defined through work: the potential difference between two points is the work per unit charge done against the electric force in moving a test charge between them. Because the electric force is conservative, this work is path-independent — a crucial fact. The potential is always easier to compute than the field (sum scalars rather than vectors) and **E** can be recovered from V by taking the gradient. This chapter establishes the potential for point charges, dipoles, and continuous distributions, and introduces the concept of equipotential surfaces. The simulation renders equipotential lines and the electric field as their orthogonal gradient — making the mathematical relationship between V and **E** visually immediate.

**Core concepts:**
- Work done by the electric force: W = q∫**E**·d**l** = q(V_A - V_B)
- Electric potential energy: U = qV
- Electric potential: V = W/q₀; units volts (V) = J/C; reference at infinity: V(∞) = 0
- Potential from a point charge: V = kq/r (scalar, not vector)
- Superposition of potentials: V_total = Σ kqᵢ/rᵢ (scalar sum — easier than vector field sum)
- Potential difference: ΔV = -∫**E**·d**l**; only differences are physically meaningful
- The gradient relationship: **E** = -∇V; **E** points from high V to low V, perpendicular to equipotentials
- Equipotential surfaces: surfaces of constant V; perpendicular to **E** everywhere
- Potential of continuous distributions: V = ∫ k dq/r
- Electric potential energy of a system of charges: U = Σᵢ<ⱼ kqᵢqⱼ/rᵢⱼ
- Electron-volt as energy unit: 1 eV = 1.6×10⁻¹⁹ J

**Key vocabulary:** electric potential, potential difference, equipotential surface, gradient, volt, electron-volt, conservative force, potential energy

**Common misconceptions:**
- "High potential means high field" — the field is the gradient of V; a large, uniform potential has zero field
- "Potential is zero where there is no charge" — potential is a cumulative effect; V at a point depends on all charges everywhere
- "Equipotential lines and field lines are the same" — they are always perpendicular

**Worked examples:**
1. Potential on the axis of a uniformly charged ring: V = kQ/√(x²+R²); differentiate to get E_x; confirm Chapter 2 result
2. Potential of a dipole: V = k p cosθ / r²; gradient to get dipole **E** field
3. Potential energy of three charges in a triangle: U = k(q₁q₂/r₁₂ + q₁q₃/r₁₃ + q₂q₃/r₂₃)

**What the student builds:**
`04-electric-potential.html` — potential surface and equipotential visualizer. Controls: drag-and-drop charges (same interface as Ch01/Ch02 simulations). Display: color-mapped potential V(x,y) as background (red=high, blue=low); equipotential contour lines as green curves; electric field vectors as arrows (should be perpendicular to equipotentials — students verify this). Toggle: show/hide field lines, show/hide potential map. Sliders: color scale range.

**Simulation physics:**
At each grid point: V = Σᵢ kqᵢ/|**r** - **r**ᵢ|. Render as D3 color map. Equipotential contours via D3 contour generator (d3.contours). Gradient **E** = -∇V computed numerically from the V grid using finite differences: E_x ≈ -(V(x+Δx,y) - V(x-Δx,y))/2Δx.

**Key references for research agent:**
- Serway & Jewett, Chapter 25
- Griffiths, Chapter 2 (section 2.3)
- The volt: historical standardization; Volta's pile (1800)
- Electron-volt in particle physics and semiconductor physics
- Physics Education Research: student difficulties with potential vs. potential energy vs. field

**Bridge to Chapter 5:** The potential between two conductors (a capacitor) stores energy. Chapter 5 introduces capacitance — how much charge a given potential difference can store — and what happens when an insulating material (dielectric) is placed between the conductors.

---

### CHAPTER 05 — Capacitance and Dielectrics
**Filename:** `05-capacitance-dielectrics.md`
**Arc position:** Act One, Chapter 5

**One-line:** Students learn how parallel conductors store charge and energy, compute capacitance for standard geometries, understand how dielectrics increase capacitance, and build a capacitor charge/discharge simulator.

**Chapter description:**
Capacitance is the bridge between electrostatics and circuits. A capacitor stores energy in the electric field between two conductors — a physical realization of the field energy concept. This chapter derives the capacitance of parallel plates, cylinders, and concentric spheres; introduces the energy stored in a capacitor and the energy density of the electric field; explains how dielectric materials increase capacitance by reducing the effective field; and shows how capacitors in series and parallel combine. The dielectric is the conceptually rich part: polarization of the dielectric material is the first example of a material's response to an applied field — a theme that continues in magnetism. The simulation shows the charging and discharging of a capacitor, making the time constant τ = RC physically visible.

**Core concepts:**
- Capacitance definition: C = Q/V; units farads (F) = C/V
- Parallel plate capacitor: C = ε₀A/d; derivation from Gauss's law and potential
- Cylindrical capacitor: C = 2πε₀L/ln(b/a)
- Spherical capacitor: C = 4πε₀ab/(b-a)
- Energy stored: U = Q²/2C = ½CV² = ½QV
- Energy density of the electric field: u_E = ½ε₀E²; energy is in the field, not on the plates
- Capacitors in series: 1/C_eq = Σ 1/Cᵢ
- Capacitors in parallel: C_eq = Σ Cᵢ
- Dielectrics: polarization, dielectric constant κ; C_dielectric = κC₀
  - Microscopic picture: induced dipoles reduce the internal field
  - Dielectric strength: breakdown field; why dielectrics allow thinner gaps
  - Permittivity: ε = κε₀
- Charging through a resistor: Q(t) = C·ε(1 - e^(-t/RC)); time constant τ = RC
- Discharging: Q(t) = Q₀ e^(-t/RC)

**Key vocabulary:** capacitance, capacitor, farad, dielectric, dielectric constant, polarization, energy density, time constant, RC circuit

**Common misconceptions:**
- "A capacitor stores charge" — it stores equal and opposite charges on two plates, with net zero charge; it stores energy in the field
- "The energy is stored on the plates" — the energy is in the electric field between the plates; energy density u = ½ε₀E²

**Worked examples:**
1. Parallel plate capacitor: compute C, E between plates, energy stored, for given A, d, V
2. Capacitors in series and parallel: find equivalent C for a mixed network; find charge on each capacitor
3. RC charging: find Q(t), V(t), I(t); determine what fraction of final charge is stored after time τ, 2τ, 5τ

**What the student builds:**
`05-capacitor-rc.html` — RC circuit charge/discharge simulator. Controls: resistance R slider, capacitance C slider, source voltage ε slider, charge/discharge toggle. Display: circuit diagram with animated charge flow (orange moving dots on wires); Q(t) and V(t) curves animating in real time; energy stored U(t) = Q²/2C curve; time constant τ = RC shown as a vertical line on the time axis. Second panel: parallel plate capacitor with dielectric slab — slider for dielectric constant κ shows how C changes and how the field between the plates weakens.

**Simulation physics:**
Q(t) = Cε(1 - e^{-t/RC}) for charging; Q(t) = Q₀e^{-t/RC} for discharging. Animate Q, V = Q/C, I = dQ/dt = (ε/R)e^{-t/RC} as live updating D3 line charts. For dielectric panel: E = σ/ε = Q/(εA) = Q/(κε₀A); show E decreasing as κ increases for fixed Q.

**Key references for research agent:**
- Serway & Jewett, Chapters 26, 28
- History of the capacitor: Leyden jar (1745); Franklin's experiments
- Dielectric materials: modern applications (ceramic capacitors, electrolytic capacitors, supercapacitors)
- Energy storage: capacitors vs. batteries; ultracapacitors in electric vehicles
- Physics Education Research: misconceptions about charge storage vs. energy storage

**Bridge to Chapter 6:** Electrostatics is complete. Chapter 6 asks: what happens when charges move? Current and resistance — and the first circuits with real dynamics.

---

### CHAPTER 06 — Electric Current and Resistance
**Filename:** `06-current-resistance.md`
**Arc position:** Act Two, Chapter 6

**One-line:** Students learn what electric current is microscopically, how resistance arises from collisions of electrons with the lattice, and derive Ohm's law — building a drift velocity simulator that shows current as a statistical phenomenon.

**Chapter description:**
Current is charge in motion. This chapter connects the macroscopic (current I, resistance R, voltage V) to the microscopic (drift velocity, electron density, mean free path). Ohm's law V = IR is derived from the Drude model — not postulated — making it clear that Ohm's law is an approximation valid for ohmic materials, not a universal truth. Resistance depends on geometry and material resistivity. Power dissipation (Joule heating) is the energy cost of driving current through resistance. This microscopic grounding is what the simulation makes vivid: students watch electrons drifting slowly (mm/s) against a background of fast thermal motion, and see how increasing the field increases the drift velocity and therefore the current.

**Core concepts:**
- Electric current: I = dQ/dt; units amperes (A) = C/s; conventional current direction
- Current density: **J** = nq**v**_d; **J** = σ**E** (microscopic Ohm's law)
- Drift velocity: **v**_d = (qτ/m)**E**; why drift velocity is ~mm/s despite fast electrons
- The Drude model: free electron gas + collisions with lattice; mean free time τ
- Resistivity ρ and conductivity σ = 1/ρ: material property; temperature dependence
- Resistance: R = ρL/A; Ohm's law: V = IR
- Ohmic vs. non-ohmic materials: linear I-V (ohmic) vs. nonlinear (diodes, transistors)
- Power: P = IV = I²R = V²/R; Joule heating
- Electromotive force (EMF): energy source driving current; ε, internal resistance r
- Temperature coefficient of resistance: R(T) = R₀[1 + α(T-T₀)]
- Superconductivity preview: resistance drops to zero below critical temperature

**Key vocabulary:** current, current density, drift velocity, Drude model, resistivity, conductivity, Ohm's law, EMF, Joule heating, superconductivity

**Common misconceptions:**
- "Current flows at the speed of light" — the signal propagates near c, but electrons drift at mm/s
- "Ohm's law is a fundamental law" — it is an empirical approximation for ohmic materials; many devices are explicitly non-ohmic
- "Current is used up by a resistor" — current (charge per second) is conserved; energy is dissipated

**Worked examples:**
1. Compute drift velocity for a copper wire carrying 1 A (n = 8.5×10²⁸ e/m³, A = 1 mm²): answer ~0.07 mm/s
2. Resistance of a copper wire 10 m long, 1 mm diameter: R = ρL/A ≈ 0.22 Ω
3. Power dissipated: a 100 Ω resistor with 5 V across it; P = V²/R = 0.25 W

**What the student builds:**
`06-drift-velocity.html` — microscopic current simulator. Display: a cross-section of a wire; dots representing conduction electrons undergoing random thermal motion (fast, random directions) with a slow superimposed drift (rightward, representing conventional current to the left). Controls: applied voltage/field slider; wire cross-section area slider. Shows: drift velocity v_d computed and displayed; current I = nqv_dA computed; Joule heating P = I²R. Animation: electrons visibly drift faster as voltage increases.

**Simulation physics:**
Each electron: position updates as **v** = **v**_thermal + **v**_drift. **v**_thermal: random unit vector × v_thermal_magnitude (set to 10× v_drift_max for visual clarity). **v**_drift = (eτ/m)**E**, displayed as a slow rightward motion. Current I = nqv_dA displayed numerically. N=50 electrons simulated; periodic boundary conditions.

**Key references for research agent:**
- Serway & Jewett, Chapter 27
- Drude model history (1900): successes and failures
- Modern understanding of electrical conduction: quantum corrections to Drude
- Superconductivity: BCS theory overview; high-temperature superconductors
- Practical: why copper is preferred for wiring (resistivity, cost, ductility)

**Bridge to Chapter 7:** Individual resistors with current flowing through them are the elements. Chapter 7 builds circuits from these elements — Kirchhoff's laws organize the analysis of any DC circuit.

---

### CHAPTER 07 — DC Circuits
**Filename:** `07-dc-circuits.md`
**Arc position:** Act Two, Chapter 7

**One-line:** Students learn to analyze any DC circuit using Kirchhoff's current and voltage laws, solve multi-loop circuit problems systematically, and build an interactive circuit simulator that computes currents and voltages in real time.

**Chapter description:**
This chapter provides the analytical tools for DC circuits. Kirchhoff's current law (KCL: current in = current out at every node) and Kirchhoff's voltage law (KVL: voltage drops sum to zero around any loop) are the two organizing principles. Together they reduce any circuit to a system of linear equations. The chapter covers resistors in series and parallel, the Wheatstone bridge, the voltmeter and ammeter (as real instruments with internal resistance), and the RC circuit in more detail. The simulation is a live circuit builder: students drag resistors, batteries, and capacitors onto a canvas and watch the currents and voltages computed and displayed in real time as they build.

**Core concepts:**
- Kirchhoff's Current Law (KCL): Σ I_in = Σ I_out at every node (charge conservation)
- Kirchhoff's Voltage Law (KVL): Σ ΔV = 0 around any closed loop (energy conservation)
- Resistors in series: R_eq = Σ Rᵢ; same current through each
- Resistors in parallel: 1/R_eq = Σ 1/Rᵢ; same voltage across each
- Voltage divider: V_out = V_in × R₂/(R₁+R₂)
- Current divider
- Multi-loop circuit analysis: assign currents, write KCL/KVL equations, solve
- The Wheatstone bridge: balanced condition R₁/R₂ = R₃/R₄; application in sensors
- Real batteries: EMF ε with internal resistance r; terminal voltage V = ε - Ir
- Measuring instruments: voltmeter (high R, in parallel); ammeter (low R, in series); loading effect
- Power in circuits: P = IV; maximum power transfer theorem
- RC circuits: charging and discharging in more detail; time constant τ = RC

**Key vocabulary:** node, loop, Kirchhoff's laws, equivalent resistance, voltage divider, Wheatstone bridge, internal resistance, terminal voltage, loading effect

**Common misconceptions:**
- "KCL is only for simple parallel circuits" — it applies at every node in any circuit
- "An ideal voltmeter draws no current" — this requires infinite internal resistance; real voltmeters have large but finite R
- "Batteries always deliver their rated voltage" — terminal voltage drops under load due to internal resistance

**Worked examples:**
1. Two-loop circuit: three resistors, two batteries; write KCL and KVL equations, solve for three currents
2. Wheatstone bridge: determine the unknown resistance when the bridge is balanced
3. Real battery: ε = 12V, r = 0.5Ω; find terminal voltage at I = 2A, 10A; find maximum current (short circuit)

**What the student builds:**
`07-dc-circuits.html` — interactive DC circuit simulator. Interface: drag resistors (adjustable R), batteries (adjustable ε), and wires onto a grid; components snap to nodes. Solver: on each change, solve the nodal equations (using Gaussian elimination or a simple relaxation method) and display current through each branch (as animated orange arrows with magnitude) and voltage at each node (as color-coded labels). Students build the circuits from the worked examples and verify their hand calculations.

**Simulation physics:**
Nodal analysis: for N nodes, write KCL at each node as a linear equation in node voltages. Matrix form: GV = I_source. Solve via Gaussian elimination. Display branch currents as I = ΔV/R. Animate current direction with moving dots scaled by current magnitude.

**Key references for research agent:**
- Serway & Jewett, Chapters 28
- Kirchhoff's biography and the history of circuit analysis (1845)
- SPICE circuit simulation: how professional circuit simulators work
- Wheatstone bridge applications: strain gauges, resistance temperature detectors (RTDs)
- Physics Education Research: common errors in multi-loop circuit problems

**Bridge to Chapter 8:** DC circuits involve only electric fields and currents. Chapter 8 introduces the other half of electromagnetism: the magnetic force on moving charges and the magnetic field.

---

### CHAPTER 08 — Magnetism and the Magnetic Force
**Filename:** `08-magnetism-magnetic-force.md`
**Arc position:** Act Two, Chapter 8

**One-line:** Students learn that moving charges experience forces in magnetic fields, compute those forces using the Lorentz force law, and build a charged particle trajectory simulator showing circular and helical motion in magnetic fields.

**Chapter description:**
The magnetic force is the first hint that something deep connects electricity and magnetism. A charge at rest feels only electric forces. A moving charge feels an additional force — perpendicular to both its velocity and the magnetic field — with no classical analogue in electrostatics. This force does no work (it is always perpendicular to motion) but it deflects moving charges into circular orbits. The magnetic field **B** is introduced through its effect on charges, its sources are addressed in Chapter 9. This chapter covers the Lorentz force, motion of charged particles in magnetic fields (cyclotron motion, the mass spectrometer, the Hall effect), and the force on current-carrying conductors. The simulation shows particle trajectories in configurable **B** fields.

**Core concepts:**
- Magnetic force on a moving charge: **F** = q**v** × **B**
- The Lorentz force (combined): **F** = q(**E** + **v** × **B**)
- Magnetic field **B**: units tesla (T) = kg/(A·s²); the Earth's field ~50 μT; MRI ~1–3 T
- The magnetic force does no work: **F** ⊥ **v** always; kinetic energy conserved
- Circular motion in a uniform **B**: r = mv/(|q|B); cyclotron frequency ω_c = |q|B/m
- Helical motion: velocity component along **B** is unaffected; pitch of helix
- The mass spectrometer: separate ions by m/q ratio using circular paths in **B**
- The Hall effect: transverse voltage in a current-carrying conductor in **B**; sign of charge carriers
- Force on a current-carrying conductor: **F** = I**L** × **B**; torque on a current loop: τ = IAB sinθ
- Magnetic dipole moment: **m** = IA n̂; potential energy U = -**m**·**B**

**Key vocabulary:** magnetic force, Lorentz force, magnetic field, tesla, cyclotron radius, cyclotron frequency, mass spectrometer, Hall effect, magnetic dipole moment, torque

**Common misconceptions:**
- "Magnetic forces do work on moving charges" — the force is always perpendicular to velocity; it changes direction, not speed
- "Magnetic field lines start and end on magnetic charges (monopoles)" — no magnetic monopoles have been observed; magnetic field lines form closed loops
- "A current-carrying wire in a magnetic field experiences a force because of its charge" — the wire is neutral; the force is on the moving charges (electrons) inside

**Worked examples:**
1. Proton entering a 0.5 T field at 10⁶ m/s perpendicular to **B**: compute cyclotron radius and period
2. Mass spectrometer: two ions with same charge but different masses enter the same **B** field; compute separation of landing points
3. Rectangular current loop in uniform **B**: compute net force (zero) and net torque; find equilibrium orientation

**What the student builds:**
`08-particle-trajectory.html` — charged particle trajectory simulator. Controls: particle charge q, mass m, initial velocity (v_x, v_y, v_z sliders), magnetic field **B** (B_x, B_y, B_z sliders), electric field **E** (optional). Display: 2D projection of 3D trajectory as an animated path; trail showing recent positions; cyclotron radius and frequency computed and displayed. Students verify circular motion for **v** ⊥ **B**, helical motion for **v** at angle to **B**, and the effect of adding an **E** field (E×B drift).

**Simulation physics:**
Equations of motion: m d**v**/dt = q(**E** + **v** × **B**). Integrate using RK4 with timestep Δt = T_cyclotron/100. 3D trajectory; project to 2D for display. Compute r = mv_⊥/(|q|B), ω_c = |q|B/m and display.

**Key references for research agent:**
- Serway & Jewett, Chapters 29
- Cyclotron: Lawrence's invention (1930); modern particle accelerators
- MRI: magnetic resonance as a cyclotron frequency phenomenon
- Hall effect: discovery (1879); quantum Hall effect (Nobel 1985, 1998)
- Earth's magnetosphere: charged particle trapping in the Van Allen belts

**Bridge to Chapter 9:** Chapter 8 asked what magnetic fields do to charges. Chapter 9 asks where magnetic fields come from: moving charges (currents) are the sources, and Biot-Savart and Ampère's law are the magnetic analogues of Coulomb's law and Gauss's law.

---

### CHAPTER 09 — Sources of Magnetic Fields
**Filename:** `09-sources-magnetic-fields.md`
**Arc position:** Act Two, Chapter 9

**One-line:** Students learn that currents are the sources of magnetic fields, compute **B** using the Biot-Savart law and Ampère's law, and build a magnetic field visualizer for wires, loops, and solenoids.

**Chapter description:**
This chapter is the magnetic analogue of Chapters 2 and 3 combined: the Biot-Savart law is the magnetic Coulomb's law (field from a source element), and Ampère's law is the magnetic Gauss's law (field from symmetric current distributions). The key results are the fields of an infinite straight wire, a circular loop, and a solenoid — three configurations that appear repeatedly in motors, transformers, and electromagnets. The two parallel wires problem introduces the definition of the ampere through magnetic force. The chapter ends with Ampère's law in differential form (∇×**B** = μ₀**J**), pointing toward Maxwell's equations. The simulation renders magnetic field lines for configurable current distributions.

**Core concepts:**
- Biot-Savart law: d**B** = (μ₀/4π) I d**l** × r̂/r²
  - μ₀ = 4π×10⁻⁷ T·m/A (permeability of free space)
  - Direction: right-hand rule; field curls around current
- Field of an infinite straight wire: B = μ₀I/(2πr); field lines are circles around the wire
- Force between parallel wires: F/L = μ₀I₁I₂/(2πd); definition of the ampere
- Magnetic field of a circular loop: B = μ₀IR²/(2(R²+x²)^(3/2)) on axis
- The solenoid: B = μ₀nI inside (uniform); B ≈ 0 outside; n = N/L
- The toroid: B = μ₀NI/(2πr) inside; B = 0 outside
- Ampère's law: ∮**B**·d**l** = μ₀I_enc (integral form)
  - Analogous to Gauss's law but for magnetic fields and currents
  - Amperian loops: same strategy as Gaussian surfaces
- Magnetic flux: Φ_B = ∫∫**B**·d**A**; Gauss's law for magnetism: ∮**B**·d**A** = 0 (no monopoles)
- Differential form: ∇×**B** = μ₀**J** (one of Maxwell's equations, pre-displacement current)
- Magnetic materials: diamagnets, paramagnets, ferromagnets; relative permeability μᵣ

**Key vocabulary:** Biot-Savart law, permeability, solenoid, toroid, Ampère's law, Amperian loop, magnetic flux, magnetic monopole, ferromagnetism

**Common misconceptions:**
- "Magnetic field lines start on north poles and end on south poles" — they form closed loops; what appear to be sources are just where field lines enter/exit a material
- "Ampère's law only works for infinite symmetry" — it is always true; symmetry determines whether it is useful for computing **B**
- "The solenoid field is uniform everywhere" — only inside, and only for an ideal infinite solenoid; it frings at the ends

**Worked examples:**
1. Magnetic field at the center of a circular loop of radius R carrying current I: B = μ₀I/2R
2. Force per unit length between two parallel wires 1 m apart, each carrying 1 A: F/L = 2×10⁻⁷ N/m (this defines the ampere)
3. Solenoid: n=1000 turns/m, I=2A; find B inside; find the field at the end (half the interior value)

**What the student builds:**
`09-magnetic-field-sources.html` — magnetic field line visualizer for current sources. Controls: choose source configuration (straight wire, circular loop, solenoid cross-section, two parallel wires); set current magnitudes and directions. Display: magnetic field lines as curves (computed by RK4 integration of **B** direction); field strength color map; right-hand rule illustrated with arrow overlays. Students set two parallel wires with same vs. opposite currents and observe the field pattern difference.

**Simulation physics:**
For a straight wire at position (x₀,y₀) carrying current I: **B**(x,y) = (μ₀I/2πr)(−sinφ, cosφ) where r and φ are polar coordinates from the wire. For multiple wires: superposition. Field lines integrated via RK4. For solenoid cross-section: model as N parallel wires arranged on a circle; superpose fields.

**Key references for research agent:**
- Serway & Jewett, Chapter 30
- Biot and Savart's original experiment (1820) and Ampère's work (1820–1825)
- Definition of the ampere: history of the SI redefinition (2019)
- MRI solenoids: field strength, homogeneity requirements
- Ferromagnetism: domain theory, hysteresis, hard vs. soft magnets

**Bridge to Chapter 10:** Chapter 9 showed that currents create magnetic fields. Chapter 10 asks the converse: can changing magnetic fields create currents? The answer — Faraday's law — is the last piece before Maxwell's equations.

---

### CHAPTER 10 — Electromagnetic Induction and Faraday's Law
**Filename:** `10-electromagnetic-induction.md`
**Arc position:** Act Two → Act Three transition, Chapter 10

**One-line:** Students learn that changing magnetic flux induces an EMF, compute induced currents using Faraday's law and Lenz's law, and build an induction simulator showing a moving magnet inducing current in a coil.

**Chapter description:**
Faraday's law is the discovery that changed everything: a changing magnetic flux through a loop induces an EMF — and therefore a current — in that loop. This is the operating principle of every electric generator, transformer, and induction motor on Earth. The chapter derives Faraday's law, establishes Lenz's law (the induced current opposes the change that caused it — a statement of energy conservation), and applies both to generators, transformers, and inductors. The inductor is introduced as the magnetic analogue of the capacitor: it stores energy in the magnetic field and resists changes in current. The RL circuit exhibits exponential current rise and fall with time constant τ = L/R. This chapter is the last building block before Maxwell's equations.

**Core concepts:**
- Faraday's law: ε = -dΦ_B/dt; EMF induced by changing magnetic flux
- Magnetic flux: Φ_B = ∫∫**B**·d**A** = BAcosθ for uniform **B**
- Lenz's law: induced current direction opposes the change in flux (the minus sign)
- Motional EMF: ε = BLv for a rod moving in a magnetic field
- The electric generator: rotating coil in **B**; ε = NBAω sin(ωt)
- Mutual inductance: M = Φ₂₁/I₁; transformer: V₂/V₁ = N₂/N₁
- Self-inductance: L = Φ/I; inductor opposes changes in current
  - Solenoid inductance: L = μ₀n²V
- Energy stored in an inductor: U = ½LI²
- Energy density of the magnetic field: u_B = B²/(2μ₀)
- RL circuit: I(t) = (ε/R)(1 - e^{-t/τ}) for τ = L/R; I(t) = I₀e^{-t/τ} for decay
- Eddy currents: induced currents in bulk conductors; dissipation and shielding

**Key vocabulary:** Faraday's law, magnetic flux, Lenz's law, motional EMF, generator, transformer, mutual inductance, self-inductance, RL circuit, eddy currents

**Common misconceptions:**
- "Faraday's law requires a physical wire loop" — EMF is induced in any changing flux region; the wire just provides a path for current
- "Lenz's law is a separate law from Faraday's" — Lenz's law is the physical interpretation of the minus sign in Faraday's law
- "Transformers amplify power" — they transform voltage and current; power is conserved (minus losses)

**Worked examples:**
1. Square loop entering a uniform **B** field: compute ε, I, and force on the loop as a function of position
2. Generator: coil (N=100 turns, A=0.01 m², **B**=0.5 T) rotating at ω = 60π rad/s; peak EMF and frequency
3. RL circuit: L=2H, R=10Ω, ε=20V; find I(t), time to reach 90% of final current

**What the student builds:**
`10-faraday-induction.html` — electromagnetic induction simulator. Controls: magnet speed and direction (moving toward/away from the coil), coil turns N, coil area A. Display: bar magnet moving toward a coil; field lines of the magnet shown (static approximation); flux Φ_B through the coil computed and displayed as a time series; induced EMF ε = -dΦ_B/dt shown; induced current direction shown with arrows in the coil (using Lenz's law). Ammeter reading shown. Students verify that faster motion = larger EMF; reversing motion = reversed current.

**Simulation physics:**
Model magnet as a magnetic dipole with moment **m**. Field at distance r along axis: B = (μ₀/4π)(2m/r³). Flux through the coil: Φ_B = B(x(t))·A where x(t) is magnet position. EMF = -N dΦ_B/dt computed numerically. Current I = EMF/R_coil. Display as animated time series.

**Key references for research agent:**
- Serway & Jewett, Chapter 31–32
- Faraday's discovery of electromagnetic induction (1831); Henry's independent discovery
- Maxwell's mathematical formulation of Faraday's law (1855–1865)
- Transformer efficiency: why transmission lines use high voltage
- Induction cooktops, wireless charging: eddy current applications

**Bridge to Chapter 11:** Faraday's law says a changing **B** creates **E**. Maxwell asked the converse: does a changing **E** create **B**? The answer requires adding a term to Ampère's law — the displacement current — and the result is Maxwell's complete equations.

---

### CHAPTER 11 — Maxwell's Equations and Electromagnetic Waves
**Filename:** `11-maxwells-equations.md`
**Arc position:** Act Three, Chapter 11

**One-line:** Students see how Maxwell's addition of the displacement current completes the four equations, derive that oscillating solutions are waves traveling at the speed of light, and build a transverse EM wave visualizer.

**Chapter description:**
This is the payoff chapter. Everything in Chapters 1–10 has been building toward this moment. Maxwell looked at Faraday's law (changing **B** creates **E**) and noticed an asymmetry: Ampère's law said nothing about a changing **E** creating **B**. He added the displacement current term and thereby completed the equations. The consequence — which Maxwell derived within the same paper — is that oscillating electromagnetic solutions must exist, and their speed is 1/√(ε₀μ₀) = 3×10⁸ m/s. This is the speed of light. The realization that light is an electromagnetic wave is the unification this book has been building toward.

**Core concepts:**
- The four Maxwell's equations (integral form):
  1. Gauss's law: ∮**E**·d**A** = Q_enc/ε₀
  2. Gauss's law for magnetism: ∮**B**·d**A** = 0
  3. Faraday's law: ∮**E**·d**l** = -dΦ_B/dt
  4. Ampère-Maxwell law: ∮**B**·d**l** = μ₀I_enc + μ₀ε₀ dΦ_E/dt
- The displacement current: J_d = ε₀ dE/dt; why it was needed (charging capacitor argument)
- Differential form of Maxwell's equations:
  1. ∇·**E** = ρ/ε₀
  2. ∇·**B** = 0
  3. ∇×**E** = -∂**B**/∂t
  4. ∇×**B** = μ₀**J** + μ₀ε₀ ∂**E**/∂t
- Deriving the wave equation from Maxwell's equations: take curl of (3) or (4), substitute (4) or (3)
  - ∇²**E** = μ₀ε₀ ∂²**E**/∂t²; wave speed c = 1/√(μ₀ε₀) = 3×10⁸ m/s
- Plane wave solutions: **E** = E₀ cos(kx - ωt) ŷ; **B** = B₀ cos(kx - ωt) ẑ
  - **E** ⊥ **B** ⊥ direction of propagation; transverse waves
  - E₀/B₀ = c; energy shared equally between **E** and **B** fields
- The electromagnetic spectrum: radio → microwave → IR → visible → UV → X-ray → gamma
- Energy transport: Poynting vector **S** = (1/μ₀)**E** × **B**; intensity I = S_avg
- Radiation pressure: P = S/c; implications for solar sails

**Key vocabulary:** displacement current, Maxwell's equations, wave equation, plane wave, transverse wave, electromagnetic spectrum, Poynting vector, radiation pressure, speed of light

**Common misconceptions:**
- "Maxwell invented the displacement current to save his equations from inconsistency" — he added it for physical reasons (charge conservation at a capacitor); the consistency was a consequence
- "Light is different from radio waves and X-rays" — all are electromagnetic waves; they differ only in frequency
- "The speed of light is constant everywhere" — it is c in vacuum; it slows in materials by factor n (index of refraction)

**Worked examples:**
1. Displacement current in a charging capacitor: C=1μF, charging at dV/dt = 10⁶ V/s; find I_d and verify it equals the conduction current
2. EM plane wave: E₀=100 V/m; find B₀, frequency if λ=500nm, intensity S_avg
3. Radiation pressure on a perfect absorber: I=1 kW/m² (approximate sunlight); pressure P = I/c = 3.3×10⁻⁶ Pa

**What the student builds:**
`11-em-wave.html` — transverse electromagnetic wave visualizer. Controls: frequency slider (radio → visible → X-ray), amplitude slider, polarization angle. Display: animated 3D-like EM wave showing **E** (orange) and **B** (purple) oscillating perpendicular to each other and to propagation direction (**k**); rendered as two perpendicular sine curves propagating to the right. Wavelength and frequency displayed. Energy density u_E(t) and u_B(t) shown as time series — students verify they are equal. Poynting vector magnitude shown.

**Simulation physics:**
**E**(x,t) = E₀ cos(kx - ωt) ŷ; **B**(x,t) = (E₀/c) cos(kx - ωt) ẑ. Render as two SVG sine curves (one in y-direction, one in z-direction) propagating in x. Animate by incrementing ωt. Display u_E = ½ε₀E² and u_B = B²/(2μ₀) — they should be equal at all times.

**Key references for research agent:**
- Serway & Jewett, Chapter 34
- Maxwell's original papers (1861–1865); Treatise on Electricity and Magnetism (1873)
- Hertz's experimental verification of EM waves (1887)
- The measurement of the speed of light: Michelson's experiments
- Special relativity connection: Maxwell's equations are Lorentz-covariant

**Bridge to Chapter 12:** Maxwell's equations are complete. Chapter 12 explores their consequences: light as an EM wave, the electromagnetic spectrum, and connections to modern physics — optics, quantum electrodynamics, wireless communication.

---

### CHAPTER 12 — Capstone: Light, Radiation, and the Unified Field
**Filename:** `12-capstone-unified-field.md`
**Arc position:** Act Three, Chapter 12

**One-line:** Students connect Maxwell's equations to the physics they will encounter in subsequent courses — optics, relativity, quantum mechanics, and wireless communication — through simulations of wave interference, antenna radiation, and the photoelectric effect.

**Chapter description:**
The capstone chapter does not introduce new fundamental content. It uses Maxwell's equations to understand phenomena students encounter in the world and in subsequent courses. Five topics are covered: geometric and wave optics (light as an EM wave, reflection, refraction, interference, diffraction), antenna radiation (oscillating charges radiate; the radiation pattern is a consequence of Maxwell's equations), the photoelectric effect as the limit of Maxwell's framework (where the classical field theory breaks down and quantum mechanics begins), special relativity (Maxwell's equations are automatically Lorentz-covariant; this is the historical motivation for relativity), and wireless communication (from Hertz's spark-gap transmitter to modern WiFi as applied Maxwell). The simulation offers a choice: an antenna radiation pattern visualizer or a two-slit interference simulator.

**Core concepts:**
- Geometric optics from Maxwell: reflection (angle in = angle out), Snell's law n₁sinθ₁ = n₂sinθ₂
  - Index of refraction: n = c/v = √(κμᵣ); slowing of light in materials
- Wave optics: superposition of EM waves; interference; diffraction
  - Double slit: d sinθ = mλ (maxima); path length difference determines phase
  - Single slit diffraction: a sinθ = mλ (minima)
- Antenna radiation: oscillating dipole antenna; radiation pattern ∝ sin²θ; near field vs. far field
  - Larmor formula: P = q²a²/(6πε₀c³); accelerating charges radiate
- The photoelectric effect: light ejects electrons from metals; threshold frequency; Einstein's explanation
  - Failure of Maxwell: intensity should determine ejection energy, not frequency
  - E_photon = hf: the quantum of electromagnetic energy
- Special relativity motivation: Maxwell's equations give the same c in all frames; this requires Lorentz transformations
  - E and B fields mix under Lorentz boosts; they are components of a single electromagnetic tensor
- Wireless communication: AM/FM as modulated carrier waves; encoding information in EM fields

**Key vocabulary:** index of refraction, Snell's law, interference, diffraction, antenna, radiation pattern, Larmor formula, photoelectric effect, photon, Lorentz transformation, electromagnetic tensor

**Worked examples:**
1. Snell's law: light entering glass (n=1.5) at 30°; find refraction angle; find critical angle for total internal reflection
2. Double-slit interference: λ=500nm, d=0.1mm, screen at L=1m; find fringe spacing
3. Photoelectric effect: sodium work function φ=2.3eV; find threshold frequency; find maximum electron kinetic energy for light at 400nm

**What the student builds:**
`12-two-slit-interference.html` — double-slit interference simulator (or `12-antenna-pattern.html` — antenna radiation pattern). For the interference simulator: Controls: slit separation d, wavelength λ (color-mapped), slit width a (adds diffraction envelope), screen distance L. Display: animated wavefronts from each slit; interference pattern on screen as intensity vs. position; single-slit diffraction envelope overlaid. Students verify fringe spacing Δy = λL/d.

**Final project options:** (A) A complete annotated simulation gallery for all 12 chapters, with written exploration notes for each; (B) A simulation of an E&M application from the student's intended field (electrical engineering, medical physics, materials science), with written explanation connecting it to Maxwell's equations; (C) A simulation-based derivation of one of Maxwell's equations, showing numerically how the equation is satisfied for a specific charge/current distribution.

**Key references for research agent:**
- Serway & Jewett, Chapters 35–38
- Hecht, *Optics* — wave optics chapters
- Einstein's photoelectric effect paper (1905, Nobel 1921)
- Hertz's antenna experiments (1887–1888)
- History of special relativity: the Maxwell motivation (Poincaré, Lorentz, Einstein)
- Wireless communication history: from Marconi to WiFi

---

## Assessment Structure

| Component | Chapters | Notes |
|-----------|---------|-------|
| Weekly simulation builds (11 × 15 pts) | 1–11 | One simulation per chapter; graded on correctness and exploration documentation |
| Chapter 0 setup (25 pts) | 0 | CLAUDE.md, DESIGN.md, PROJECT.md all present and correct |
| Act One checkpoint: field and potential (75 pts) | 1–5 | Problem set: Gauss's law applications, potential calculations, capacitor energy |
| Act Two checkpoint: circuits and induction (75 pts) | 6–10 | Multi-loop circuits, magnetic force problems, Faraday's law |
| Final exam: Maxwell's equations and waves (100 pts) | 11–12 | Derive wave equation from Maxwell; EM wave properties; capstone connections |
| Simulation exploration reports (3 × 25 pts) | 3, 8, 11 | Short written report: what did you change, what did you observe, what does it mean physically |
| Final project (150 pts) | 12 | See Chapter 12 options above |

---

## Simulation Stack Reference

All simulations use D3 v7, single HTML files with inline CSS and JS.

**Standard E&M simulation elements defined in CLAUDE.md:**
- SVG canvas: 700×500px for 2D field visualizations; 700×400px for time-series plots
- Field line integration: RK4 with adaptive step size; terminate when leaving canvas or when |**E**| < threshold
- Vector field rendering: 20×15 grid of arrows; arrow length = log(1 + |**F**|) × scale; direction = **F**/|**F**|
- Parameter sliders: HTML range inputs, live update on `input` event; label shows current value
- Animation: `requestAnimationFrame` loop; pause/play button always present
- Physics constants: ε₀ = 8.85×10⁻¹², μ₀ = 4π×10⁻⁷, k = 8.99×10⁹, c = 3×10⁸ (defined once in CLAUDE.md)
- Dark mode: `prefers-color-scheme` media query in all files

---

## Open Questions for Research Agent

1. What are the current best-reviewed calculus-based E&M textbooks and how do their chapter structures compare to this one? Specifically: Serway/Jewett, Halliday/Resnick/Krane, Young/Freedman, Griffiths intro — what do they cover and in what order?
2. What are the most common student misconceptions at each stage of E&M, per Physics Education Research literature? Key PER groups: University of Washington Tutorials, PHEC, Matter & Interactions curriculum.
3. What D3 or browser-based physics simulations currently exist for E&M? What is the state of the art? PhET simulations are the benchmark — where do they succeed and what gaps remain?
4. What are the key historical primary sources that should anchor each chapter narratively? Especially: Coulomb's torsion balance, Faraday's lab notebooks, Maxwell's 1865 paper, Hertz's antenna experiments.
5. For Chapter 11 (Maxwell's Equations): what are the most accessible treatments of the displacement current argument and the wave equation derivation for undergraduates?
6. For Chapter 12 (Capstone): what are accessible review articles or textbook treatments connecting classical E&M to special relativity and quantum mechanics at the intro level?
7. What existing chapters in the `physics-plus-one-electromagnetism/chapters/` directory can be directly incorporated, and what is their current coverage quality?

---

*TIKTOC.md v1.0 — 13 chapters (Chapter 0 + Chapters 1–12)*
*Ready for: research gathering (Cowork research prompt), chapter drafting*
*Repo: physics-plus-one-electromagnetism*
*Consolidates existing chapters: 01+02 → Ch01+Ch02 split; 06+08 → Ch08; 04+07 → Ch07; adds Ch03 (Gauss), Ch05 (Capacitance), Ch09 (Sources of B), Ch12 (Capstone)*
