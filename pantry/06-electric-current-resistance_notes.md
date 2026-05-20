# Research Notes: Chapter 06 — Electric Current and Resistance

**Source:** TIKTOC.md chapter entry (Chapter 06)
**Notes file:** 06-electric-current-resistance_notes.md
**Corresponding chapter:** chapters/06-electric-current-resistance.md (not yet written)
**Predecessor archive:** chapters/_archive/05-electric-current-resistance-and-ohm-s-law.md (OpenStax-derived source; mined for examples and worked-problem numbers)
**Generated:** 2026-05-16

---

## Chapter summary (from TIKTOC.md)

Act Two opens. Current is charge in motion. The chapter walks from macroscopic ($I$, $R$, $V$) to microscopic (drift velocity, electron density, mean free time) and *derives* Ohm's law from the Drude model rather than postulating it. The pedagogical center is the four-speeds-of-electricity puzzle — Fermi velocity ~$10^6$ m/s, thermal velocity ~$10^5$ m/s, drift velocity ~$10^{-4}$ m/s, signal propagation ~$10^8$ m/s — and the realization that a current is a statistical bias on top of fast thermal chaos. Resistance comes from collisions of carriers with the lattice (phonons + defects). Power dissipation $P = IV$ is the energy cost of running carriers through that scattering bath. Students build a drift-velocity simulator (`06-drift-velocity.html`) — periodic-boundary box, ~50 electrons, random thermal kicks plus a tunable applied field, live readout of $v_d$, $I$, $P$.

Learning outcomes:
- Define current $I = dQ/dt$ and current density $J = nqv_d$
- Derive $v_d = (q\tau/m)E$ from the Drude model
- Derive Ohm's law $V = IR$ from $J = \sigma E$ plus geometry
- Distinguish ohmic from nonohmic materials and explain why metals are (approximately) ohmic
- Compute resistance from $R = \rho L/A$; reason about temperature dependence
- Compute power dissipation three ways: $P = IV = I^2R = V^2/R$
- Distinguish the four electron speeds and resolve the "instant light" paradox
- Sketch the historical arc: Drude (1900) → Sommerfeld (1928) → band theory → BCS (1957) → cuprates (1986)

---

## A. Conceptual foundations

### Current: rate of charge flow, but watch the sign convention

Electric **current** is the time rate at which charge crosses a fixed cross-section:

$$I = \frac{dQ}{dt}, \quad \text{units: ampere (A) = coulomb/second (C/s)}.$$

For steady DC: $I = Q/t$. For time-varying current (RC discharge, AC, switching transients): the derivative form is the honest one.

**Conventional current** is the direction *positive* charges would move — from + terminal of a battery, through the external circuit, to the − terminal. Franklin set this convention before electrons were known. **Electron flow** is opposite, because electrons are negative. The two are identical in physical effect; we keep conventional current because most textbook equations are written with it.

There is a real ambiguity here worth naming for students: in a metal wire, the actual charge carriers are electrons drifting from − to +. In an ionic solution (battery interior, electrochemistry), positive and negative ions drift in opposite directions and *both* contribute to $I$. In a p-type semiconductor, the carriers are "holes" — absences of electrons in the valence band — and conventional current points in the direction holes drift. The sign convention is *not* a statement about what's microscopically happening; it's a bookkeeping choice that lets every equation look the same.

**Order-of-magnitude anchors (memorize these):**
- USB-C charger: 1–3 A
- Kitchen toaster: 10–15 A
- Car starter motor cranking: 200–400 A (briefly)
- High-voltage transmission line: ~2,000 A
- Lightning bolt: ~30,000 A for ~30 µs
- Neuron action potential current through a single ion channel: ~1 pA

The factor-of-$10^{16}$ span between an ion channel and a lightning stroke is one of the cleaner illustrations of how a single physical quantity can scale across all of physics, biology, and engineering.

### Current density: the local version

For a wire of cross-section $A$, **current density** $J = I/A$ (units A/m²). For arbitrary geometry, $\mathbf{J}$ is a vector: magnitude is current per unit area perpendicular to flow, direction is the local flow direction of positive charge.

In terms of carriers:

$$\mathbf{J} = nq\mathbf{v}_d$$

where $n$ is carrier number density (m$^{-3}$), $q$ is the charge per carrier (signed), and $\mathbf{v}_d$ is the drift velocity. This is *the* microscopic definition. For electrons with $q = -e$, $\mathbf{J}$ points opposite to $\mathbf{v}_d$ — exactly the conventional-current convention.

Then $I = \int \mathbf{J} \cdot d\mathbf{A}$ through any cross-section, and for a uniform wire reduces to $I = nqv_dA$.

### Drift velocity: a statistical bias on thermal chaos

This is the conceptual heart of the chapter. In a metal with no applied field, the free electrons move at high speed ($\sim 10^6$ m/s, the Fermi velocity in copper) but in random directions; their mean velocity is zero, so $\mathbf{J} = 0$. Apply a field $\mathbf{E}$ along the wire. Each electron now feels a force $\mathbf{F} = -e\mathbf{E}$ and accelerates between collisions. After each collision (with a phonon or a lattice defect), it's randomized — its memory of the previous trajectory is wiped. But between collisions, the field has nudged it slightly in one direction. Average that nudge over many collisions and you get the drift velocity:

$$\mathbf{v}_d = \frac{q\tau}{m}\mathbf{E}$$

where $\tau$ is the **mean free time** between collisions and $m$ is the carrier mass. For electrons in copper, $\tau \approx 2.5 \times 10^{-14}$ s. The drift velocity is the *bias* on the random motion, not a separate motion.

This is what the simulation will show. Each electron in the box does its thermal bouncing (which dominates the eye); turn the field up and the cloud as a whole creeps slowly in one direction. The current is the slow creep of a cloud whose individuals are nearly all moving in other directions at any given moment.

**Worked example — copper wire carrying 1 A through 1 mm² cross-section:**

$n_{\text{Cu}} = 8.5 \times 10^{28}$ m$^{-3}$ (one conduction electron per atom; standard value).

$$v_d = \frac{I}{nqA} = \frac{1.0}{(8.5 \times 10^{28})(1.6 \times 10^{-19})(1.0 \times 10^{-6})} \approx 7.4 \times 10^{-5} \text{ m/s} \approx 0.074 \text{ mm/s}.$$

Less than a tenth of a millimeter per second. A finger drumming on a desk goes faster. The OpenStax archive uses a 14-gauge wire ($A = 3.1 \times 10^{-6}$ m²) and gets $v_d \approx 2.5 \times 10^{-5}$ m/s for 1 A — same order of magnitude, different cross-section. The TIKTOC spec uses 1 mm² and 1 A and asks for "~0.07 mm/s" — confirmed.

### The four speeds, and why "instant light" isn't a paradox

This is the chapter's pedagogical centerpiece. Four distinct speeds, often confused:

| Speed | Magnitude | What it is |
|---|---|---|
| Drift velocity $v_d$ | $\sim 10^{-4}$ m/s | Bias on thermal motion under $\mathbf{E}$. Sets the current. |
| Thermal velocity (classical) | $\sim 10^5$ m/s at 300 K | RMS speed if electrons were a classical gas. |
| Fermi velocity $v_F$ | $\sim 1.6 \times 10^6$ m/s for Cu | Actual speed of electrons at the Fermi surface — quantum, T-independent below the Fermi temperature. |
| Signal speed (E-field propagation in the wire) | $\sim 2 \times 10^8$ m/s | Transverse EM wave guided by the conductor. Sets when the bulb turns on. |

Why does the bulb light instantly when you flip the switch, if drift is mm/s? Because the *signal* — the rearrangement of the electric field through the wire — propagates near $c$. The field reaches every electron in the wire within nanoseconds, and every electron *starts drifting where it already is*. No electron has to travel from the switch to the bulb. The bulb glows because the electrons *already inside the filament* begin drifting (and dissipating energy by scattering) almost the instant the switch closes.

The water-pipe analogy works here, if you keep its limits in mind: a pipe full of water has the water at the far end emerge essentially the instant you push at the near end — the marbles don't have to travel the length. The analogy breaks down where it matters most: the "push" through a metal wire is not a mechanical pressure wave through the electron fluid, it's a transverse electromagnetic wave guided by the conductor's surface and dielectric environment. Most of the action is *outside* the wire, in the field. This is the bridge to transmission lines, waveguides, and antennas in later chapters.

A second confusion worth pre-empting: the Fermi velocity is *not* the drift velocity, and it is *not* the thermal velocity. Electrons in a metal are a degenerate Fermi gas. Pauli exclusion forces them to occupy states up to a Fermi energy $\sim$ 7 eV in copper, corresponding to $v_F \approx 1.6 \times 10^6$ m/s. This speed is set by quantum statistics, not temperature; cooling copper to 4 K barely changes $v_F$ but dramatically changes $\tau$. The mean free path is $\lambda = v_F \tau \approx (1.6 \times 10^6)(2.5 \times 10^{-14}) \approx 40$ nm at room temperature — long compared to the lattice spacing (~0.26 nm in Cu), short compared to the wire (~mm to m). Verified value: 39–40 nm, in agreement with thin-film resistivity fits.

**Source:** *Electron mean free path in elemental metals*, J. Appl. Phys. 119, 085101 (2016), https://pubs.aip.org/aip/jap/article/119/8/085101/143910/

### The Drude model: free electron gas + lattice collisions

Paul Drude proposed the model in 1900, three years after J.J. Thomson identified the electron and several decades before quantum mechanics. The picture:

1. Each metal atom contributes one (or a few) free electrons to a "gas" that fills the metal.
2. The electrons move freely between collisions with stationary ion cores (the lattice).
3. After each collision, the electron's velocity is randomized to a thermal distribution at the local temperature.
4. The mean time between collisions is $\tau$.

**Derivation of $\mathbf{v}_d = (q\tau/m)\mathbf{E}$.** Between collisions, the equation of motion is $m\dot{\mathbf{v}} = q\mathbf{E}$. The drift velocity is the average velocity that builds up before a collision wipes it out. If collisions happen with characteristic time $\tau$, the average post-collision velocity gain is $\mathbf{v}_d = (q\mathbf{E}/m)\tau$. (More rigorously: solve the relaxation-time equation $d\langle\mathbf{v}\rangle/dt = q\mathbf{E}/m - \langle\mathbf{v}\rangle/\tau$ in steady state.) Either way:

$$\mathbf{v}_d = \frac{q\tau}{m}\mathbf{E}$$

Combine with $\mathbf{J} = nq\mathbf{v}_d$:

$$\mathbf{J} = \frac{nq^2\tau}{m}\mathbf{E} \equiv \sigma\mathbf{E}$$

with conductivity

$$\sigma = \frac{nq^2\tau}{m}$$

This is the **microscopic Ohm's law**. It says current density is proportional to applied field, with a constant of proportionality determined entirely by carrier density and mean free time. Resistivity is $\rho = 1/\sigma = m/(nq^2\tau)$.

**Derivation of macroscopic Ohm's law.** For a uniform wire of length $L$ and cross-section $A$: $E = V/L$ (uniform field from constant potential gradient), $J = I/A$, so

$$\frac{I}{A} = \sigma\frac{V}{L} \implies V = I \cdot \frac{L}{\sigma A} = I \cdot \frac{\rho L}{A} \equiv IR$$

with

$$R = \frac{\rho L}{A}$$

Ohm's law $V = IR$ is *not* a fundamental law of nature. It is a consequence of (1) a constant carrier density, (2) a mean free time $\tau$ that doesn't depend on the field, and (3) linear response — the drift velocity is proportional to the field. For metals at modest fields and constant temperature, all three hold to a remarkable approximation. For semiconductors $n$ depends on temperature and field (mobile carriers are excited across a band gap), for diodes the geometry is asymmetric (p-n junction), for tungsten filaments $\tau$ drops sharply as the wire heats. In all those cases, $V$ vs. $I$ is nonlinear and Ohm's law fails.

**This is the chapter's central honesty.** Most intro texts state Ohm's law as a postulate and let students walk away thinking it's universal. The Drude derivation makes it visibly an *approximation* — and shows exactly where it breaks.

### What Drude got right and what Drude got wrong

This is rarely taught at the intro level but it's where the story becomes interesting.

**Got right:**
- Ohm's law $J = \sigma E$ (correct functional form)
- The Wiedemann–Franz law: $\kappa/\sigma T \approx L_0$ (Lorenz number) — the ratio of thermal to electrical conductivity in metals is a constant at fixed temperature. Drude predicted the right magnitude (within a factor of 2) by treating thermal and electrical transport with the same carrier gas. This was a stunning success — and a coincidence, as it turned out.
- Hall effect (sign and magnitude for many metals)

**Got wrong:**
- **Electronic specific heat too high.** Drude predicted electrons contribute $(3/2)k_B$ per electron to the specific heat (equipartition). Measured value is ~100× smaller at room temperature. This was the biggest empirical embarrassment for the classical model.
- **Magnetic susceptibility too large.** Predicted Curie-law paramagnetism; observed Pauli paramagnetism is a couple of orders smaller.
- **Predicted sign of Hall coefficient wrong for some metals** (Al, Zn, Cd).

Sommerfeld fixed most of these in 1928 by replacing Maxwell–Boltzmann statistics with Fermi–Dirac statistics. The electrons obey Pauli exclusion; almost all of them are locked in deep states and *can't* absorb thermal energy because there are no empty states nearby. Only electrons within $k_BT$ of the Fermi surface participate in heat capacity. This kills the specific-heat catastrophe and rescues the Wiedemann–Franz prediction at the same time. The conductivity formula $\sigma = ne^2\tau/m$ survives essentially intact — but now $\tau$ is the relaxation time at the Fermi surface, not the average classical time. The numerical coincidence is that the two definitions of $\tau$ happen to be similar in metals at room temperature.

**Sources:**
- Drude, P. *Zur Elektronentheorie der Metalle*, Ann. Phys. 306, 566–613 (1900). https://onlinelibrary.wiley.com/doi/abs/10.1002/andp.19003060312
- Sommerfeld, A. *Zur Elektronentheorie der Metalle auf Grund der Fermischen Statistik*, Z. Phys. 47, 1 (1928). Two-part treatise summarized in PNAS 14, 370 (1928), https://www.pnas.org/doi/10.1073/pnas.14.5.370
- Ashcroft & Mermin, *Solid State Physics*, Ch. 1 (Drude) and Ch. 2 (Sommerfeld) — the standard graduate-level treatment.

### What's actually scattering the electrons?

Drude said "ion cores," and that's wrong by a quantum-mechanical mile. In a *perfectly periodic* lattice, electrons propagate as Bloch waves with infinite mean free path. The lattice itself doesn't scatter them. What scatters them is *departures from periodicity*:

1. **Lattice vibrations (phonons).** As $T$ rises, atoms vibrate more, the lattice deviates more from perfect periodicity, and scattering rates grow. Phonon scattering rate $\propto T$ for $T \gg \Theta_D$ (the Debye temperature). This dominates room-temperature resistivity of pure metals.
2. **Defects and impurities.** Vacancies, dislocations, foreign atoms — all are static deviations from periodicity. They give a temperature-independent contribution to resistivity (Matthiessen's rule: $\rho(T) = \rho_{\text{phonon}}(T) + \rho_{\text{defects}}$).
3. **Other electrons.** Electron-electron scattering is usually small in metals (Fermi liquid theory), giving a $T^2$ contribution that is significant only at very low temperatures.

This is the proper microscopic picture of resistance. Drude's "billiard balls hitting ions" is a useful cartoon that produces the right $\sigma = ne^2\tau/m$ but gets the mechanism of $\tau$ wrong.

### Resistivity table — verify and span the range

| Material | $\rho$ at 20 °C (Ω·m) | Notes |
|---|---|---|
| Silver | $1.59 \times 10^{-8}$ | Best room-T conductor (slightly better than Cu) |
| Copper | $1.68 \times 10^{-8}$ | Workhorse for wiring |
| Aluminum | $2.65 \times 10^{-8}$ | Lighter than Cu; high-voltage transmission |
| Tungsten | $5.60 \times 10^{-8}$ | Filaments — chosen for melting point, not resistivity |
| Iron | $9.71 \times 10^{-8}$ | Structural; not used for wiring |
| Nichrome (Ni-Cr alloy) | $1.10 \times 10^{-6}$ | Heating elements (toaster, hair dryer) |
| Carbon (graphite, polycrystalline) | $\sim 3 \times 10^{-5}$ | Brushes in motors, pencils |
| Silicon (pure) | $\sim 640$ | Useless as conductor; doped silicon is the basis of every chip |
| Glass | $10^{10}$–$10^{14}$ | Insulator |
| Quartz (fused) | $\sim 7.5 \times 10^{17}$ | Among the best room-T insulators |

26 orders of magnitude from quartz to silver. This is the largest range in physics for any everyday physical parameter that isn't a particle mass — and the conceptual key is that within this range there is no smooth interpolation. Conductors and insulators are qualitatively different states of matter, separated by a band gap (~5 eV for SiO₂, ~1.1 eV for Si, zero for Cu). Doping silicon doesn't change its band structure much; it adds carriers into otherwise-empty bands and slides the Fermi level. That's how 26 orders of magnitude of resistivity can be engineered with parts-per-billion impurity concentrations.

**Why copper for wiring** (vs. silver, which is slightly better):
- Cost: silver is ~80× more expensive per kg.
- Ductility: both are excellent, copper is workable down to fine gauges.
- Corrosion: copper develops a self-passivating oxide; silver tarnishes (Ag₂S) which is a worse conductor.
- Abundance: Cu is ~1000× more abundant in Earth's crust.

**Why aluminum for high-voltage transmission lines** (despite higher resistivity):
- About 1/3 the mass density of Cu, so for the same conductance per kg, Al wins for long spans.
- Cheaper.
- Trade-off: Al-to-Cu junctions suffer "aluminum-to-copper joint failure" if not properly made (galvanic corrosion + differential thermal expansion). The 1970s US house-wiring aluminum failures motivated current code requiring CO/ALR-rated devices.

**Why tungsten for filaments** (despite mediocre resistivity):
- Melting point 3,422 °C — the highest of any metal. A filament needs to glow at ~2,500–3,000 K to emit substantial visible light, which would vaporize any other common metal.
- High resistivity at operating T (≈10× room-T value) is actually convenient for matching to line voltage with a short, stout wire.

### Temperature dependence: metals up, semiconductors down

For metals near room temperature:

$$R(T) = R_0\left[1 + \alpha(T - T_0)\right]$$

with $\alpha > 0$. Microscopically: warmer lattice = more phonons = shorter $\tau$ = lower $\sigma$ = higher $\rho$. Sample values of $\alpha$ at 20 °C:
- Copper: $4.04 \times 10^{-3}$ /K
- Aluminum: $3.9 \times 10^{-3}$ /K
- Tungsten: $4.5 \times 10^{-3}$ /K
- Iron: $5.0 \times 10^{-3}$ /K
- Nichrome: $4 \times 10^{-4}$ /K (alloy disorder dominates over phonons, so $\alpha$ is small — this is why nichrome is used in precision resistors and heating elements where stable $R$ matters)

For semiconductors, $\alpha < 0$ at moderate temperatures: heating excites more carriers across the band gap; the increase in $n$ dominates the decrease in $\tau$. Pure Si has $\alpha \approx -0.07$ /K near room temperature — vastly more sensitive than any metal, and the basis for thermistors.

**Worked numerical anchor — incandescent bulb inrush current:**

A 60 W bulb runs at 120 V, drawing $I = P/V = 0.5$ A. Operating resistance $R_{\text{hot}} = V/I = 240$ Ω. The tungsten filament runs at ~2,800 K (≈ 2,500 °C above room temperature). Using $\alpha = 4.5 \times 10^{-3}$ /K extrapolated linearly:

$$R_{\text{hot}}/R_{\text{cold}} \approx 1 + (4.5 \times 10^{-3})(2,800 - 293) \approx 12.3$$

So $R_{\text{cold}} \approx 240/12.3 \approx 20$ Ω, and at switch-on the inrush current is $120/20 = 6$ A — twelve times the steady-state draw. The bulb survives because the filament heats to operating temperature in ~100 ms, well before it can melt; the time-averaged $I^2R$ over that transient is bounded by the filament's thermal mass. Filaments most often fail *at the moment of turn-on* precisely because that's when current is highest and a thin spot (already nearer to failure) gets the worst of it. This is the empirical reason old-style filament bulbs were often replaced after a switch-on event rather than during steady operation.

### Power dissipation: $P = IV = I^2R = V^2/R$

The energy delivered per unit time by a battery driving current $I$ across potential difference $V$ is $P = IV$. For a resistor obeying Ohm's law, all three forms are algebraically equivalent:

$$P = IV = I^2R = \frac{V^2}{R}$$

Different forms are useful in different problems:
- Voltage source + known $R$: use $V^2/R$.
- Current source + known $R$: use $I^2R$.
- Measured $V$ and $I$ on an unknown load: use $IV$.

**Microscopic picture:** Each carrier picks up energy $qE\Delta x$ between collisions, then dumps that energy into the lattice in the collision. The rate of energy dumping per unit volume is $\mathbf{J} \cdot \mathbf{E} = \sigma E^2 = J^2/\sigma$. Integrate over a uniform wire and you recover $P = I^2R$. This is **Joule heating**: ordered drift energy converted to disordered lattice energy (heat) one collision at a time.

**Worked example — the TIKTOC's 100 Ω at 5 V:**
$$P = \frac{V^2}{R} = \frac{25}{100} = 0.25 \text{ W}$$
A quarter-watt — the standard small resistor power rating. Doubling V to 10 V quadruples P to 1.0 W, exceeding the rating and likely smoking the part. This is the *most common student misconception* (TIKTOC item 4): doubling voltage doubles current and *quadruples* power. The intuition that "doubling V doubles P" comes from sloppy use of $P = IV$ as if both $I$ and $V$ are independent; they aren't, by Ohm's law.

### EMF and internal resistance

Real batteries are not ideal voltage sources. They have an **electromotive force** ε (the open-circuit voltage, set by the chemistry) and an **internal resistance** $r$ (set by the electrolyte conductivity, electrode kinetics, and geometry). When the battery drives current $I$ through an external load $R$:

$$\varepsilon = I(R + r)$$

The terminal voltage (what a voltmeter across the battery reads under load) is $V = \varepsilon - Ir$. A fresh AA alkaline has ε ≈ 1.5 V and $r \approx 0.15$–$0.30$ Ω; as it discharges, $r$ rises (the electrolyte develops products that impede ion flow), and the terminal voltage sags. A "dead" battery often has ε still close to 1.5 V — open-circuit measurement looks fine — but $r$ has risen to several ohms and the battery can no longer supply useful current.

The chapter should resist the temptation to derive Kirchhoff's loop equation here; that's Chapter 7 (circuits). The point now is just that the battery contributes both an EMF and a series resistance, and the latter dissipates a fraction $r/(R+r)$ of the total power inside the battery (which is why batteries get warm under load).

### Superconductivity: the limit case where R = 0 exactly

Three milestones, each with verified dates:

1. **Discovery (1911).** Heike Kamerlingh Onnes, having become the first person to liquefy helium (1908, reaching 4.2 K), measured the resistivity of solid mercury as he cooled it. At 4.19 K, the resistance dropped abruptly to *unmeasurably small*. His lab notebook (8 April 1911, 16:00): "*Kwik nagenoeg nul*" — "Mercury nearly zero." Onnes won the 1913 Nobel Prize, primarily for the helium liquefaction; superconductivity was the bonus discovery the technique made possible.
2. **BCS theory (1957).** John Bardeen, Leon Cooper, and Robert Schrieffer (University of Illinois) published *Theory of Superconductivity* in Phys. Rev. 108, 1175 (1957), Dec. 1, 1957, following a brief Letter in Phys. Rev. 106, 162 (April 1957). The mechanism: electrons near the Fermi surface bind into **Cooper pairs** mediated by the exchange of lattice vibrations (phonons) — counterintuitively, two negative charges attract via the lattice's response. Cooper pairs are bosons and condense into a coherent quantum state that flows without scattering. Bardeen (his second Nobel), Cooper, and Schrieffer shared the 1972 Nobel Prize.
3. **High-Tc cuprates (1986).** J. Georg Bednorz and K. Alex Müller at IBM Zurich measured a transition at ~35 K in La₂₋ₓBaₓCuO₄ — far above the previous record (~23 K in Nb₃Ge). Their paper appeared in Z. Phys. B 64, 189 (1986). The 1987 Nobel Prize followed *the next year* — the shortest time from discovery to Nobel in physics history. Within months, Paul Chu and M.K. Wu (University of Houston, January 1987) synthesized YBa₂Cu₃O₇ (YBCO), with $T_c \approx 92$ K — above the boiling point of liquid nitrogen (77 K). The economic and engineering threshold mattered: liquid N₂ costs ~$0.50/L vs. liquid He at ~$10–30/L, and cryogenics suddenly became routine.

**Why high-Tc is still a research problem in 2026:** the mechanism that binds Cooper pairs in cuprates is *not* phonon exchange (BCS would not predict $T_c$ this high). It is widely thought to involve antiferromagnetic spin fluctuations in the copper-oxide planes, but a quantitative microscopic theory comparable to BCS has remained elusive for forty years. This is one of the hardest open problems in condensed matter physics.

**Recent claims and retractions (2023):**
- *LK-99* (Lee, Kim, et al. 2023, Korean preprint) claimed room-temperature ambient-pressure superconductivity in a copper-doped lead apatite. The claim went viral on social media in July 2023. By August 2023, independent replication attempts worldwide had concluded the material is *not* a superconductor; observed anomalies traced to Cu₂S impurities undergoing a structural phase transition near 385 K. The episode is a useful teaching anchor for *how science self-corrects rapidly when a claim is concrete enough to test*.
- Earlier *Ranga Dias et al.* claims (Nature, 2020) of room-temperature superconductivity in carbonaceous sulfur hydride at megabar pressures were retracted in 2022; a 2023 paper from the same group claiming superconductivity in nitrogen-doped lutetium hydride was retracted in 2023.

**Confirmed high-pressure superconductors as of 2026:** H₃S at 203 K under 150 GPa (Drozdov et al., 2015, replicated); LaH₁₀ at ~250 K under 170 GPa (Somayazulu et al., 2019, replicated). These are real but require diamond-anvil pressures — laboratory curiosities, not engineering materials.

**Practical superconductors in 2026:**
- Low-Tc (NbTi, Nb₃Sn): MRI magnets, particle accelerators (LHC), MagLev test lines. Need liquid helium.
- High-Tc cuprates (YBCO, BSCCO): tape conductors for fusion reactors (SPARC, ITER coils), grid-scale fault-current limiters, some MRI prototypes. Need liquid N₂.
- Magnesium diboride (MgB₂, $T_c = 39$ K, discovered 2001): cheaper than YBCO for $T < 30$ K applications.

**Sources:**
- Onnes, H. K. *The resistance of pure mercury at helium temperatures*, Comm. Leiden 120b, 122b (1911). Lab notebook entry 8 April 1911; APS Milestone https://ethw.org/Milestones:Discovery_of_Superconductivity,_1911
- Bardeen, J., Cooper, L. N. & Schrieffer, J. R. *Theory of superconductivity*, Phys. Rev. 108, 1175 (1957). https://link.aps.org/doi/10.1103/PhysRev.108.1175
- Bednorz, J. G. & Müller, K. A. *Possible high-Tc superconductivity in the Ba-La-Cu-O system*, Z. Phys. B 64, 189 (1986).
- Wu, M. K. et al. *Superconductivity at 93 K in a new mixed-phase Y-Ba-Cu-O compound*, Phys. Rev. Lett. 58, 908 (1987).
- LK-99 saga: Wikipedia https://en.wikipedia.org/wiki/LK-99 (rapid debunking summary, 2023); IEEE Spectrum coverage.

---

## B. Domain examples and cases

### Case 1: The 60 W incandescent bulb (and why we replaced it)

A 60 W incandescent bulb at 120 V: tungsten filament, operating at ~2,800 K, runs at ~240 Ω. Efficiency as a light source is ~2–3% — the rest of the input power is radiated as infrared (heat). For a 60 W bulb that's ~58 W of infrared and ~2 W of visible light. The bulb is closer to a small electric heater than a light source.

A 9 W LED replacement gives equivalent visible-light output (~800 lumens) at ~15% efficiency — about $3 W of visible light from 9 W input, with the remaining 6 W as heat from the LED driver electronics and resistive losses in the LED itself. The LED chip's electrical-to-optical efficiency is higher (~50%) but the driver circuitry (rectifier, current-limiter, sometimes capacitive dropper) eats a substantial fraction.

The teaching point is not that "LEDs are more efficient" — it's that incandescents *are nearly all heater*. The 60 W bulb is a 60 W resistive heater that happens to also glow visibly. Old hen-house heat lamps and chick brooders use 250 W infrared bulbs as deliberate heat sources; the visible-light "bonus" is irrelevant.

US incandescent general-service bulbs of 40–100 W were effectively banned from sale in August 2023 (DOE Final Rule requiring ≥45 lumens/watt) — Joule heating in lighting became regulatorily unacceptable on energy-efficiency grounds. Specialty applications (oven bulbs, appliance bulbs, heat lamps) are exempt.

### Case 2: Power transmission and the I²R argument

The grid runs at high voltage because $P_{\text{loss}} = I^2R$ in the transmission line. To deliver a fixed power $P_{\text{load}} = IV$ to the consumer, raising $V$ allows reducing $I$, which reduces $I^2R$ losses *quadratically*.

**Sample numerical example.** Deliver 1 GW over 200 km, line resistance 10 Ω (typical for steel-core aluminum cable):
- At $V = 110$ kV: $I = 9.1$ kA, $P_{\text{loss}} = (9100)^2(10) = 830$ MW. *83% of the generated power dissipated in the line.* Untenable.
- At $V = 345$ kV: $I = 2.9$ kA, $P_{\text{loss}} = 84$ MW. *8.4% loss.* Marginal.
- At $V = 765$ kV: $I = 1.3$ kA, $P_{\text{loss}} = 17$ MW. *1.7% loss.* Standard US bulk transmission.

This is why the eastern US runs 345 kV–765 kV trunk transmission, why long-distance HVDC (high-voltage DC) links use ±400 kV to ±1100 kV (Xinjiang–Anhui ±1100 kV link, 3,300 km, completed 2019), and why local distribution drops to 13.8 kV (substation) → 7.2 kV (distribution) → 240/120 V (house service) through transformers. Each step is a power-vs-safety trade-off.

**HVDC vs. HVAC for long distance:** HVAC suffers from reactive losses (capacitance to ground, especially in undersea cables). Beyond ~600 km overhead or ~50 km undersea, HVDC becomes more efficient despite the cost of converter stations (AC-to-DC at one end, DC-to-AC at the other). HVDC also enables interconnects between asynchronous grids — the western US grid (60 Hz, but separately synchronized) ties to the eastern US grid through HVDC links.

US grid total transmission and distribution losses run around 5–6% of generated electricity (EIA, 2023 data, https://www.eia.gov/tools/faqs/faq.php?id=105).

### Case 3: Toaster, hair dryer, and the design economics of Joule heating

A 1500 W toaster at 120 V draws 12.5 A, so $R = 9.6$ Ω. Nichrome ribbon, $\rho \approx 1.1 \times 10^{-6}$ Ω·m, cross-section ~$5 \times 10^{-7}$ m² (a few mm wide, 0.1 mm thick): $L = RA/\rho \approx 4.4$ m. About four meters of nichrome wire, coiled and folded to fit inside the toaster. The element reaches ~1,000 °C in operation (visible orange glow), well below nichrome's ~1,400 °C melting point, with room for cyclic thermal stress without failure.

A 1875 W hair dryer at 120 V draws 15.6 A — close to the 15-A breaker limit, which is why hair-dryer-and-anything-else-on-the-same-circuit is the most common breaker-trip event in US homes. The element is a coil of nichrome, with a fan forcing air across the coil to keep the element from melting (and to deliver the heated air to the hair).

Why nichrome? Three reasons:
1. **Resistivity** ~70× that of copper, so the heating element is a manageable length (meters, not hundreds of meters).
2. **High melting point** (~1,400 °C) — survives glowing operation indefinitely.
3. **Forms a self-passivating chromium oxide layer** — does not oxidize away even at red heat. Pure iron or copper would oxidize through and fail in hours.

The same alloy family (with variations) is in your oven coils, your space heater, your soldering iron, your kiln, and the heating elements in industrial furnaces up to ~1,200 °C.

### Failure case: aluminum house wiring (1965–1973)

Between 1965 and 1973, a copper shortage drove US homebuilders to wire houses with aluminum branch circuits instead of copper. Aluminum has ~60% the conductivity of copper at the same cross-section, but it was used at a slightly larger gauge to compensate.

The failure mode was not resistivity — it was **the joint**, not the wire. Aluminum:
1. Thermally expands ~30% more than copper for the same temperature rise → joints loosen with every heating/cooling cycle.
2. Forms a hard, non-conductive aluminum oxide layer almost instantly when exposed to air.
3. Is mechanically softer than copper → creeps under the screw pressure of a standard outlet terminal, loosening further.

A loose joint has elevated resistance. Elevated resistance + high current = local $I^2R$ heating = more oxidation = higher resistance = runaway. Hundreds of US house fires were traced to Al-wired outlets in the 1970s; the CPSC estimates Al-wired homes were ~55× more likely to have a fire-hazard connection than Cu-wired homes. Modern code (since 1972) requires CO/ALR-rated devices for aluminum connections, with anti-oxidant paste at every joint.

The lesson for the chapter: **resistance is a property of the whole conducting path, including every joint and contact.** A wire with low $\rho$ does not save you if one connection has $R = 0.1$ Ω at 15 A — that's 22.5 W dissipated in a half-cubic-centimeter of metal, more than enough to start a fire over hours.

### Case 4: Power-MOSFET on-resistance ($R_{\text{DS(on)}}$) and EV motor controllers

Modern electric vehicles deliver hundreds of kilowatts through power MOSFETs (silicon or silicon carbide). A typical SiC MOSFET in a Tesla Model 3 motor inverter has $R_{\text{DS(on)}} \approx 5$ mΩ at room temperature. At 300 A peak current, $P_{\text{loss}} = I^2R = (300)^2(0.005) = 450$ W per device. The inverter has six such devices (three-phase bridge × 2 for top/bottom), so ~2.7 kW of total ohmic loss. The inverter housing has liquid cooling because that 2.7 kW must leave the part before $T$ rises into thermal runaway.

This is Joule heating in a modern semiconductor context. The Drude picture survives: $\rho$ is small but nonzero, geometry forces the current through a thin channel, and $I^2R$ has to be reckoned with at every stage. The reason SiC is replacing Si in EV inverters is that SiC's wider band gap allows higher temperatures and lower $R_{\text{DS(on)}}$ per area — 50% efficiency gains in the inverter, which translates to a few percent of vehicle range.

---

## C. Connections and dependencies

**Prerequisites (what reader must already know):**
- Ch 1 (Coulomb's law): force on a charged carrier in a field
- Ch 2 (Electric field): the $\mathbf{F} = q\mathbf{E}$ that accelerates carriers between collisions
- Ch 4 (Electric potential): $V$ as the driving potential difference; $E = -dV/dx$ gives field-from-voltage in a uniform wire
- Ch 5 (Capacitance): $\tau = RC$ as the time constant — the first dynamical timescale introduced
- Kinetic theory of gases (from thermo course): mean free time, average velocity, relaxation-time approximation — same machinery applied to a charged gas

**Unlocks (what this chapter makes possible):**
- Ch 7 (DC circuits): Kirchhoff's laws on multi-loop networks with $V$, $I$, $R$
- Ch 8 (Magnetism): magnetic force on moving charges ($\mathbf{F} = q\mathbf{v} \times \mathbf{B}$) — and the Hall effect, which directly measures $n$ and $v_d$
- Ch 9 (Sources of B): Ampère's law, where the source is *current*
- Ch 10 (Faraday): induced EMF generates current; $I^2R$ losses in transformers
- Ch 14 (Capstone): electrical power generation and grid distribution

**Adjacent chapter connections:**
- Ch 5 (Capacitance): RC time constants. Discharging a capacitor through a resistor dissipates $\frac{1}{2}CV^2$ as Joule heating in $R$, regardless of $R$. The simulator built here will connect to the RC simulator built there.
- Ch 8/9 (Magnetism): the Hall voltage is $V_H = IB/(nqt)$ — *direct experimental measurement of $n$ and the sign of $q$.* The Hall sign turning out to be "wrong" in Al/Zn/Cd was one of the puzzles that motivated band theory.

---

## D. Current state of the field

**Settled:**
- The Drude–Sommerfeld picture is exact for free-electron-like metals (alkali metals, noble metals) at modest fields and temperatures. $\sigma = ne^2\tau/m$ predicts conductivity to within a factor of order unity from first-principles materials properties.
- Ohm's law $V = IR$ is exact for ohmic materials within their linear response regime.
- The Wiedemann–Franz law $\kappa/\sigma T = L_0 = \pi^2 k_B^2/(3e^2) = 2.44 \times 10^{-8}$ W·Ω/K² is exact in the relaxation-time approximation, well-verified in most metals at moderate $T$.
- The Boltzmann transport equation, with band-structure inputs, predicts metallic transport properties to spectroscopic precision in conventional metals.

**Settled but counterintuitive:**
- Resistance is *not* due to electrons hitting ions. In a perfect lattice, electrons would propagate without resistance. Resistance is due to *imperfections* — phonons, defects, impurities, surfaces. This is the band-theory correction to Drude (Bloch, 1928; Wilson, 1931).
- Mean free path in pure Cu at room T is ~40 nm — 100× longer than the lattice spacing. Drude's "billiard balls" picture has the right phenomenology and the wrong mechanism.

**Active research (as of 2026):**
- *High-Tc superconductivity mechanism.* Forty years after the cuprate discovery, there is still no consensus microscopic theory analogous to BCS. Spin-fluctuation models lead the field but quantitative agreement with experiment remains incomplete. Hubbard model studies on supercomputer (DMRG, DMFT, quantum Monte Carlo) approaching from the theory side.
- *Strange metals* (cuprates, heavy-fermion compounds, twisted bilayer graphene). Resistivity ∝ $T$ all the way to absolute zero in some phases — Planckian dissipation, $\tau \sim \hbar/(k_B T)$. The conventional Fermi-liquid theory breaks down. Mechanism contested.
- *Topological materials.* Topological insulators have insulating bulk but metallic surface states protected by topology — resistance becomes a *geometric* property at edges. Quantum Hall effect at room temperature in graphene was achieved in 2023.
- *Room-temperature superconductor hunt.* Hydrogen-rich compounds under pressure (H₃S, LaH₁₀, CaH₆ in 2024) reach $T_c$ above 200 K, but only at >100 GPa. Ambient-pressure room-T superconductor remains the holy grail; LK-99 (2023), Dias et al. (2020, 2023) episodes show the field's pattern of bold claim → rapid replication failure → retraction. As of 2026, no credible ambient-pressure room-T superconductor exists.

**Key references:**
1. Ashcroft, N. W. & Mermin, N. D. *Solid State Physics*. Holt, Rinehart, Winston (1976). Ch. 1 (Drude), Ch. 2 (Sommerfeld), Ch. 13 (semiclassical transport). The standard advanced textbook.
2. Kittel, C. *Introduction to Solid State Physics*, 8th ed. (2005). Ch. 6 (free electron Fermi gas), Ch. 7 (energy bands). More accessible than Ashcroft & Mermin for a strong undergraduate.
3. Serway, R. & Jewett, J. *Physics for Scientists and Engineers*, Ch. 27 (current and resistance). The standard intro-physics presentation.
4. Drude, P. *Zur Elektronentheorie der Metalle*, Ann. Phys. 306, 566 (1900).
5. Sommerfeld, A. *Zur Elektronentheorie der Metalle*, Z. Phys. 47, 1 (1928).
6. Bardeen, J., Cooper, L. N. & Schrieffer, J. R. *Theory of superconductivity*, Phys. Rev. 108, 1175 (1957).
7. Bednorz, J. G. & Müller, K. A. Z. Phys. B 64, 189 (1986).
8. Gall, D. *Electron mean free path in elemental metals*, J. Appl. Phys. 119, 085101 (2016). https://pubs.aip.org/aip/jap/article/119/8/085101/143910/
9. Drozdov, A. P. et al. *Conventional superconductivity at 203 K at high pressures*, Nature 525, 73 (2015). (For H₃S high-pressure record.)
10. PER references on student misconceptions about current: McDermott, L. C. & Shaffer, P. S. *Research as a guide for curriculum development: an example from introductory electricity*, Am. J. Phys. 60, 994 (1992). The canonical study of the "current is consumed" misconception.

---

## E. Teaching considerations

**Where students get stuck:**

- **"Current is used up by the resistor."** This is the single most prevalent persistent misconception in introductory E&M (McDermott & Shaffer 1992 and dozens of follow-up studies). Students draw a circuit with the current "leaving the battery, getting smaller through each resistor, and a smaller current returning." The chapter must make conservation of charge visible and physical — every electron that enters the resistor leaves it. The simulation can help: cross-section ammeters at multiple points along the wire always read the same value.

- **The four speeds.** Students who learn "electrons drift slowly" think drift velocity *is* the speed of the electrons. They confuse it with thermal velocity ("but doesn't temperature make them faster?") and with signal speed ("how does the bulb know to come on?"). The chapter must lay out the four speeds *with a single table early* and reinforce them through the simulation (where the eye sees thermal chaos plus a faint drift, and a separate display shows the signal propagation at field speed).

- **Ohm's law as a "law of nature."** Most students leave intro physics thinking $V = IR$ is universal. The chapter's Drude derivation must make visible that it follows from *three* approximations (constant $n$, field-independent $\tau$, linear response), and that violating any one of them produces non-ohmic behavior. The diode I-V curve, shown alongside a metallic-wire I-V curve, makes the contrast unmissable.

- **Power scaling $P = V^2/R$ vs. $P = IV$.** Students reason "doubling voltage doubles power" because $P = IV$, missing that doubling $V$ also doubles $I$ in an ohmic load. Plot $P(V)$ for a fixed resistor — the parabola lands the point.

- **Direction of conventional current vs. electron flow.** Students who have just learned that electrons are the actual carriers find it perverse to point current arrows the opposite way. The chapter should name the convention explicitly, explain that the equations are written for $I$, and reassure that almost no problem requires distinguishing — except in the Hall effect, where the sign of the Hall voltage tells you the sign of the carriers (and Al's positive Hall coefficient is the historical clue that something was missing from Drude).

- **Temperature dependence in metals vs. semiconductors.** Students often try to apply the linear $R(T) = R_0[1 + \alpha\Delta T]$ formula to a thermistor and get nonsense. The formula assumes Drude with $n$ fixed and $\tau$ shrinking with $T$. In a semiconductor, $n$ rises exponentially with $T$ across the band gap. Different mechanism, different formula ($\rho \propto e^{E_g/2k_BT}$).

**Analogies and framings that work:**

- **Marbles in a pipe (for the signal-vs-drift distinction).** Push at one end, marble at the far end pops out essentially instantly, but no marble traveled the pipe's length. Quantitatively accurate for the speed-vs-flow part; breaks down for the mechanism of "push" (which in a wire is EM, not pressure).
- **Bias on Brownian motion (for drift velocity).** The drift is a small mean displacement on top of much larger random displacements per unit time. Shows up clearly in the simulation.
- **Water tower + leak (for EMF and internal resistance).** Tower height = ε. Pipe internal friction = $r$. Open tap = load $R$. The bigger the flow, the more pressure drop wastes inside the tower's pipes.
- **Phonon scattering as "wading through a windy field."** The lattice is the field; thermal vibrations are the wind; warmer day = more wind = harder walking = higher resistivity.

**Analogies that should NOT be used (or used with explicit caveat):**

- **"Current flows like water in a pipe."** Sometimes useful for circuits as a whole, but it cements the misconception that current is something *transported* through the wire from one place to another. In a metal, the electrons are *already everywhere in the wire*; they all start drifting at once. Water-pipe analogies must be paired with the "all electrons drift simultaneously" reminder.
- **"Resistance is like friction."** Friction dissipates kinetic energy continuously. Drude scattering dissipates energy in *discrete* events (collisions). The end result (energy → heat) is the same, but students who internalize "friction" sometimes try to derive Ohm's law from $F = -bv$ and get confused about why $b$ depends on temperature.

**Exercises that build the target skill:**

- *Symmetry / speed diagnosis (Bloom: Understand)* — Given a copper wire carrying 1 A, identify (a) the drift velocity, (b) the Fermi velocity of the electrons, (c) the thermal velocity at 300 K, (d) the speed at which the bulb at the other end of the wire lights up when the switch is closed. Compute each and rank them. This is the chapter's diagnostic exercise.
- *Drude-derive Ohm (Bloom: Apply)* — Start from $\mathbf{F} = q\mathbf{E}$ and a mean free time $\tau$; derive $v_d = q\tau E/m$, then $J = \sigma E$, then $V = IR$ with $R = \rho L/A$ and $\rho = m/(nq^2\tau)$. Plug in copper numbers ($n = 8.5 \times 10^{28}$, $\tau = 2.5 \times 10^{-14}$ s) and recover $\rho \approx 1.7 \times 10^{-8}$ Ω·m. Compares to measured. The capstone derivation.
- *Inrush current problem (Bloom: Apply + Analyze)* — Given a tungsten filament at room temperature and hot operating resistance, compute the cold-to-hot resistance ratio and the inrush current at switch-on. Then discuss why this explains "bulbs fail at the moment of turn-on."
- *Power transmission economics (Bloom: Apply + Evaluate)* — Deliver 1 GW over 200 km with line $R = 10$ Ω. Compute fractional power loss at 110 kV, 345 kV, 765 kV. Argue from the numbers that very-high-voltage transmission isn't a choice, it's a physical necessity given $I^2R$.
- *Ohmic vs. nonohmic diagnosis (Bloom: Analyze)* — Given V-I data for four devices (metal wire, incandescent filament hot vs. cold, diode forward, thermistor), classify ohmic vs. not, and identify *why* each non-ohmic one is non-ohmic (temperature, asymmetric geometry, $n(T)$).
- *Simulator exercise (Bloom: Apply + Synthesize)* — Use the drift-velocity simulator. (a) With $E = 0$, verify $v_d = 0$ (cloud-of-electrons centroid stationary). (b) Raise $E$; verify $v_d$ proportional to $E$. (c) Raise temperature; verify $v_d/E$ decreases (mimicking $\tau$ shortening). (d) Estimate $\tau$ from the simulation and compare to $\tau = m v_d / (qE)$. The simulator is the bridge from algebra to mechanism.

---

## F. Library files relevant to this chapter

- `chapters/_archive/05-electric-current-resistance-and-ohm-s-law.md` — the OpenStax-derived predecessor draft. Mined for example numbers (60 W bulb, 1500 W toaster, drift velocity in 14-gauge wire) and historical anchors (Ørsted 1820, Ohm 1827, Edison 1882). The new chapter replaces this with Drude derivation as the central machinery rather than Ohm's law as postulate.
- `pantry/05-capacitance-dielectrics_notes.md` — for the RC time constant connection and the "energy in the field" framing that this chapter complements with "energy dissipated by scattering."
- `pantry/03-gauss-law_notes.md` — for the established voice and structure of these notes files; the conductor-in-equilibrium derivation lives there but is *not* re-derived here.

---

## G. Gaps and flags

- **GAP:** OpenStax archive lumps "AC vs DC" into this chapter. The TIKTOC keeps AC for a later chapter (Faraday's law / generators). Recommend: in Chapter 06, mention RMS values briefly only if needed for the household-circuit examples; defer the full AC treatment to Ch 10 or 11. The reasoning being deferred to power transmission Edison-Westinghouse argument naturally sits with electromagnetic induction, not with the microscopic origin of resistance.

- **FLAG:** The TIKTOC asks for the simulator to display $v_d$, $I$, $P$ "live" with a field/voltage slider. The non-trivial design decision: do you simulate the *Drude* model (classical billiard balls with $\tau$ tuned to match Cu) or the *Sommerfeld* model (free Fermi gas with the same $\sigma$)? Recommend: simulate Drude classically. The simulator's job is to make $v_d$ visible against thermal chaos; Fermi statistics would complicate the visual without changing the conductivity formula. Note in the chapter that this is a Drude-flavored simulation and that the actual quantum picture changes the mechanism (band theory, phonons) but preserves $\sigma = ne^2\tau/m$.

- **FLAG:** Don't oversell BCS as "the theory of superconductivity." BCS explains conventional (low-Tc, phonon-mediated) superconductors. Cuprates and other high-Tc materials are *not* BCS; the mechanism is unsettled. The chapter should be explicit about this — it's a teachable case of *the standard theory does not yet cover the most economically important members of the class*.

- **FLAG:** The LK-99 episode is recent (2023) and excellent pedagogical material for "how science self-corrects rapidly when a claim is concrete." Worth a sidebar paragraph but not the chapter's center.

- **GAP:** A clean treatment of *why ohmic behavior is approximately linear over such a wide range* is genuinely hard at the intro level. The honest answer is: $\tau$ depends weakly on field strength because $eE\lambda \ll k_BT$ for any field a metal can sustain without breaking down. Below dielectric breakdown, the perturbation of carrier energies by the field is negligible compared to the thermal energy, so $\tau$ is essentially field-independent and Ohm's law holds. Above breakdown (or in semiconductors at high field), $\tau$ depends on $E$ and Ohm's law fails. The chapter should at least gesture at this rather than treat Ohm's-law linearity as magic.

- **GAP:** Hall effect deserves a forward-pointer ("we'll measure $n$ and the sign of $q$ in Chapter 8") but not full treatment here. The Al/Zn/Cd "wrong-sign" puzzle is one of the cleanest motivations for band theory, and a sentence noting it here pays off in Chapter 8.

- **GAP:** Earnshaw-like impossibility theorems for steady-state current don't have a clean analogue. The chapter could note (one sentence) that steady current requires a *non-conservative* EMF source — the line integral of $\mathbf{E}$ around a closed circuit must be nonzero, which means an EMF must exist somewhere. This is a forward pointer to Faraday's law in Ch 10.

- **FLAG:** Don't include AC power transmission cost-benefit analysis in this chapter's worked examples — that's Ch 10. Keep this chapter's transmission example simple: $P_{\text{loss}} = I^2R$, raising V lowers I, lowers losses quadratically. Save the AC-vs-DC story for later.

- **GAP:** The chapter must reckon honestly with the *historical accident* that Drude (1900) got the answer mostly right with the wrong mechanism. This is one of physics's cleaner examples of "the model is more robust than the picture that motivated it." The Wiedemann–Franz coincidence is the dramatic illustration. The chapter's "still puzzling" item could reasonably point at this: *why does $\sigma = ne^2\tau/m$ survive the transition from classical to quantum statistics essentially unchanged?* (Sommerfeld's calculation reveals it's because the relevant $\tau$ in both models happens to coincide for free-electron-like metals — but the agreement is closer than it has any right to be a priori.)
