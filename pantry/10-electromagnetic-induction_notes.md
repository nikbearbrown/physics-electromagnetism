# Research Notes: Chapter 10 — Electromagnetic Induction and Faraday's Law

**Source:** TIKTOC.md chapter entry (Chapter 10)
**Notes file:** 10-electromagnetic-induction_notes.md
**Corresponding chapter:** chapters/10-electromagnetic-induction.md (to be written; an archived OpenStax-style draft lives at `chapters/_archive/09-electromagnetic-induction-ac-circuits-and-electrical-technologies.md` and can be mined, not lifted)
**Generated:** 2026-05-16

---

## Chapter summary (from TIKTOC.md)

The Act Two → Act Three hinge. A changing magnetic flux through a loop induces an EMF, and therefore a current, in that loop. From this single fact follow generators, transformers, inductors, RL circuits, eddy currents, and (one chapter later) the third of Maxwell's equations. Establish Faraday's law (ε = −dΦ_B/dt) and Lenz's law (the minus sign as energy conservation); derive motional EMF (ε = BLv) and rotating-coil EMF (ε = NABω sin ωt); introduce self-inductance and mutual inductance; close with the RL circuit's exponential rise/fall and the magnetic energy density u_B = B²/(2μ₀). The chapter's simulation is `10-faraday-induction.html` — a bar magnet moved toward a coil, with the flux through the coil and the induced EMF shown as time-series traces, and the induced current direction set by Lenz.

This chapter is the *last building block* before Maxwell's equations (Ch 11). Ch 9 supplied the source side (currents → B, and the *definition* of magnetic flux Φ_B = ∫∫B·dA). Ch 10 supplies the response side (changing B → E). Ch 11 closes the loop by adding displacement current (changing E → B) and showing the pair propagates as light.

---

## A. Conceptual foundations

### Faraday's law: ε = −dΦ_B/dt

**What it says.** For any closed loop bounded by a surface S, the EMF (electromotive force, units volts) induced around the loop equals the negative time-derivative of the magnetic flux through S:

ε = −dΦ_B/dt, where Φ_B = ∫∫_S **B**·d**A**.

For uniform **B** through a flat loop of area A whose normal makes angle θ with **B**: Φ_B = BA cos θ, so

ε = −d(BA cos θ)/dt.

Three independent ways the flux can change, each producing an EMF:
1. **B changes in magnitude** at fixed geometry — a nearby AC current ramping up, a moving magnet, a switching electromagnet.
2. **A changes** — a loop whose enclosed area is being stretched, compressed, or swept through the field (the rod-on-rails geometry that motivates motional EMF).
3. **θ changes** — the loop is rotated in a fixed field (the generator geometry).

For a coil of N turns wrapped on the same flux path, the flux linkage NΦ_B replaces Φ_B and each turn contributes its own EMF in series:

ε = −N dΦ_B/dt.

**Why "EMF" and not "voltage."** In static circuits, voltage is the line integral of a conservative electric field between two points and is independent of path. The induced electric field from Faraday's law is *not conservative*: ∮**E**·d**ℓ** = −dΦ_B/dt ≠ 0 around a loop enclosing changing flux. The integral depends on which loop you choose. EMF labels the line-integral of this non-conservative field around a closed loop. Practically the units are still volts and the EMF drives a current ε/R through the loop's resistance, just like a battery would. Pedagogically: call it EMF, not voltage, on first introduction, then loosen to voltage in worked examples once the distinction has landed.

**Where Φ_B comes from.** The definition of magnetic flux is in Ch 9 (B-field from currents). Ch 10 uses it but does not redefine it. The Wb (weber) = T·m² is introduced in Ch 9; here we put it to work.

### Lenz's law: the minus sign is energy conservation

The minus sign in Faraday's law is not a bookkeeping convention — it is a physical statement, due in this form to Heinrich Lenz (1834): **the induced current flows in whichever direction creates a magnetic field that opposes the change in flux that produced it.**

Push the north pole of a bar magnet toward a coil. The flux through the coil (in whatever direction the magnet's field points through the coil's plane) is increasing. The induced current flows in the sense whose own magnetic moment **m** = IA**n̂** points *outward toward the approaching magnet's north* — that is, the coil presents its own north pole to push back. You feel a force resisting the motion; you do mechanical work; that work becomes electrical energy in the coil and ultimately heat in the coil's resistance.

Pull the magnet out: flux is decreasing. Induced current reverses to maintain the flux it had — the coil now presents a south pole, attracting the receding magnet. You again do work pulling it away.

**The energy-conservation argument, stated as a one-line proof by contradiction:** Suppose the induced current did *not* oppose the change. Push a magnet at velocity v toward the coil. The induced current then flows in the sense that *helps* the change, producing a field whose moment attracts the incoming magnet. The magnet accelerates. As it accelerates, the rate of flux change increases, so the induced EMF increases, so the induced current increases, so the attractive force increases, so the magnet accelerates harder. The coil meanwhile dissipates I²R in its resistance. You have an isolated mechanical system whose kinetic energy is increasing without bound while electrical energy is also being produced. Perpetual motion of the first kind, prohibited by the first law of thermodynamics. The only escape is the minus sign in Faraday's law: induced currents oppose the change, the magnet decelerates if you let go, and your mechanical work pays the electrical-and-thermal bill.

**Lenz's law is not separate from Faraday's law.** It is the physical content of the minus sign. Treating them as two principles is a pedagogical convenience for direction-finding; treating them as two laws is a category error.

### Motional EMF: ε = BLv

Specialize Faraday's law to a rigid conducting rod of length L sliding at velocity v along two stationary rails through a uniform B perpendicular to the rod and to v. The enclosed area grows at rate dA/dt = Lv, so the flux grows at dΦ_B/dt = B·Lv, and the EMF is

ε = BLv.

A different but equivalent derivation: each conduction electron in the moving rod feels a Lorentz force **F** = q**v**×**B** along the rod's length. This force does the work of separating charge until an electrostatic field inside the rod balances the magnetic force on stationary electrons. The accumulated potential difference end-to-end of the rod is BLv. The rod behaves like a battery with EMF BLv and internal resistance equal to its own resistance.

If the rails close the circuit through external resistance R, the current is I = BLv/R. The current-carrying rod in the external B then feels a Lorentz force F = BIL = B²L²v/R *opposing its motion* (Lenz again). To keep the rod moving at v, the external agent must supply mechanical power P_mech = Fv = B²L²v²/R, which equals exactly the electrical power dissipated in R: P_elec = I²R = (BLv)²/R. The energy ledger closes.

**The two derivations agree by no accident.** This is one of the famous symmetries of Maxwell theory: Faraday's law (flux-based, written in the lab frame) and the Lorentz force on the moving carriers (force-based, written in the carrier's terms) give the same EMF for the same physical setup. In the rod's rest frame, there is no motional EMF — only an electric field induced by the changing magnetic field the rod now "sees." Both pictures are correct; this is a foretaste of the relativistic unification of **E** and **B** that closes the book.

### Generators: ε(t) = NBAω sin(ωt)

A flat coil of N turns and area A rotates at angular frequency ω in a uniform B perpendicular to the rotation axis. At time t the coil's normal makes angle ωt with **B**, so Φ_B = NBA cos(ωt), and

ε(t) = −dΦ_B/dt = NBAω sin(ωt).

Peak EMF: ε₀ = NBAω. RMS for AC analysis: ε_rms = ε₀/√2.

Two notes:
- **Frequency choice is mechanical.** A 60 Hz generator runs at ω = 2π(60) ≈ 377 rad/s. With a two-pole rotor on a steam turbine, that's 3600 rpm — a convenient steam-turbine shaft speed. 50 Hz corresponds to 3000 rpm. The line frequency was effectively set by the available turbine speeds and once chosen has been locked in by installed base.
- **DC generators add a commutator** — a split-ring mechanical switch that flips the brush connections each half-rotation, so the external circuit sees the *absolute value* of the sinusoid (pulsed DC), not the raw AC. Modern alternators (in cars) generate AC and rectify it with diodes; the commutator is largely obsolete in new designs.

### Self-inductance: L = NΦ/I and ε = −L dI/dt

A current I in a coil produces a magnetic flux Φ through itself. The flux is proportional to I (linear magnetics, ignoring saturation), so define **self-inductance** L by

NΦ = LI, i.e., L = NΦ/I.

Units: henry (H) = Wb/A = V·s/A. Named for Joseph Henry, who discovered self-induction independently of Faraday and slightly earlier (see §B Case 1).

If I changes in time, the flux it produces changes, and Faraday's law gives an induced EMF that *opposes* the change:

ε = −L dI/dt.

This is the minus sign of Lenz: the coil fights changes in its own current. It does so by storing energy in its magnetic field during current rise and releasing that energy during current fall.

**Solenoid inductance.** For a long solenoid of n turns per unit length, cross-sectional area A, length ℓ (so N = nℓ): inside the solenoid B = μ₀nI (Ch 9), flux per turn Φ = BA = μ₀nIA, total flux linkage NΦ = nℓ · μ₀nIA = μ₀n²ℓA·I = μ₀n²V·I, where V = ℓA is the solenoid's interior volume. Therefore

L_solenoid = μ₀n²V.

Useful sanity: a 1000-turn solenoid 10 cm long with 1 cm² cross-section has n = 10⁴ turns/m, V = 10⁻⁵ m³, L = (4π×10⁻⁷)(10⁸)(10⁻⁵) ≈ 1.3 mH. Iron-cored versions multiply this by μ_r (hundreds to thousands), reaching the henry range.

### Mutual inductance and the transformer

Two coils share flux through a common geometry (often an iron core that channels the flux). Current I₁ in coil 1 produces flux Φ₂₁ through each turn of coil 2. Define **mutual inductance** M by

N₂Φ₂₁ = M I₁.

It is a theorem (not just a convention) that the same M describes the inverse coupling: N₁Φ₁₂ = M I₂. Mutual inductance is symmetric: M₁₂ = M₂₁ = M.

Faraday's law gives the induced EMF in the secondary from the primary's changing current:

ε₂ = −M dI₁/dt.

**The transformer.** An idealized transformer has both primary and secondary wound on a common iron core so that all flux from one passes through the other. The same dΦ/dt threads each turn of each coil, so the EMF per turn is the same on both sides. Therefore

V₂/V₁ = N₂/N₁ (turns ratio).

Power conservation in an ideal transformer means V₁I₁ = V₂I₂, so

I₂/I₁ = N₁/N₂.

Step *up* the voltage, step *down* the current. This is the technology that makes long-distance power transmission economic — see §B Case 2 below.

### Energy stored in an inductor: U = ½LI²

Build current I in an inductor of inductance L from zero. The induced back-EMF is ε = −L dI/dt, opposing the rise. The external source must supply power P = ε_ext · I = L (dI/dt) · I against this back-EMF. Integrate from 0 to I:

U = ∫₀^I LI' dI' = ½LI².

This energy is stored in the magnetic field inside (and around) the coil. For a long solenoid with L = μ₀n²V and B = μ₀nI:

U = ½ (μ₀n²V) I² = ½ (μ₀n²I²) V = ½ (B²/μ₀) V = (B²/2μ₀) · V.

The **energy density** of the magnetic field is therefore

u_B = B²/(2μ₀).

This is the magnetic analogue of the electric energy density u_E = ½ε₀E² introduced in Ch 5 (capacitance). Together they give the energy density of any electromagnetic field — a result that becomes the Poynting-flux machinery in Ch 11.

**The deep claim:** energy lives *in the field*, not in the wires that produced the field. A solenoid disconnected from its source but with current still flowing (a superconducting loop, say) has energy ½LI² stored in the volume the field occupies. Cut the wire and discharge the field; the energy comes out as a spark, an EMF spike, infrared, or sound, depending on the dissipation channel. This claim is the bridge from Ch 5's "energy in the electric field" to Ch 11's "energy in the propagating wave."

### RL circuits: τ = L/R, exponential rise and fall

Series circuit: ideal battery ε, resistor R, inductor L, switch. Close the switch at t = 0. Kirchhoff's voltage law:

ε − IR − L dI/dt = 0.

This is a linear ODE with the standard solution

I(t) = (ε/R) [1 − e^(−t/τ)], where τ = L/R.

The current rises exponentially toward the final value ε/R with **time constant** τ. The inductor's back-EMF starts at +ε (perfectly opposing the source, current zero) and decays to zero (no flux change at steady state, current at ε/R).

Discharge (open the source, short the inductor through R): solution is the mirror image,

I(t) = I₀ e^(−t/τ).

**Useful benchmarks:**
- t = τ → I has reached (1 − 1/e) ≈ 63% of final value (or fallen to 37%).
- t = 2τ → 86%.
- t = 3τ → 95%.
- t = 5τ → 99.3% — the conventional "engineering full charge."
- **Time to 90% of final: t₉₀ = τ ln(10) ≈ 2.303τ.** This is the answer to TIKTOC Worked Example #3.

The RL circuit is the magnetic mirror of the RC circuit (Ch 5/7). Compare:
| Quantity | RC | RL |
|---|---|---|
| Time constant | τ = RC | τ = L/R |
| Stored energy | U = ½CV² | U = ½LI² |
| Stored in | Electric field | Magnetic field |
| Energy density | ½ε₀E² | B²/(2μ₀) |
| Element resists changes in | Voltage | Current |

Notice the *inverted* dependence on R: a bigger R makes RC slower but RL faster. That inversion catches students.

### Eddy currents

Faraday's law applies to *any* closed conducting path, including paths you didn't intend. A solid metal plate moving through a region of changing B (or moving through a non-uniform stationary B) develops induced loop currents — **eddy currents** — in the conducting bulk. By Lenz, those currents produce fields that oppose the change, which means the plate feels a *retarding force* whenever it moves through field gradients.

Three engineering consequences:

1. **Magnetic braking.** Drop a strong neodymium magnet down a copper or aluminum tube and it falls *slowly* — eddy currents in the tube wall produce a retarding force that nearly balances gravity. Used in regenerative-braking systems (trains, roller-coasters, some elevators) where you want contactless, wear-free deceleration. The kinetic energy ends up as ohmic heat in the conductor.

2. **Transformer core losses.** A solid iron transformer core would itself act like a fat conducting loop and dissipate huge eddy-current losses. The fix: **laminated cores** — the iron is built up from thin (~0.3 mm) varnished sheets, each insulated from the next, so eddy-current loops cannot close through the bulk. Power transformer efficiencies of 98–99% depend on this trick.

3. **Induction heating.** Drive a coil with high-frequency AC and place a conductor inside; the conductor heats from eddy-current dissipation. Industrial: melting steel in induction furnaces. Domestic: induction cooktops (~25 kHz drive), which heat ferromagnetic cookware directly. Pan must be ferrous (high μ_r concentrates the flux at the pan bottom); aluminum and copper cookware barely heat at all.

4. **The Foucault pendulum demonstration.** A copper plate swung between the pole faces of a strong electromagnet damps to a halt within a few swings; the same plate with radial slits cut through it (so eddy loops cannot close) swings nearly freely. Léon Foucault used this in 1855 to demonstrate the effect that now bears his name in some texts ("Foucault currents," especially in French).

---

## B. Domain examples and cases

### Case 1: Faraday 1831, Henry 1830, and the historical record

**Michael Faraday, August 29, 1831, Royal Institution, London.** Faraday wound two coils on opposite sides of a soft iron ring (an "iron ring with helices"). Coil A was connected through a switch to a battery; coil B was connected to a galvanometer across the room. He closed the switch on the A side. The B-side galvanometer needle deflected — *then returned to zero* while the A-side current flowed steadily. When he opened the switch, the needle deflected the other way and again returned to zero.

The induction was *transient*, occurring only during the moment the A-side current was *changing* — at switch-on and switch-off. Steady current in A produced no effect in B no matter how strong. This was Faraday's first demonstration that the effect required *change*, not just the presence of a field. He repeated the experiment with permanent magnets pushed in and out of a coil in October 1831 (the demonstration most textbooks describe; it is iconic but historically second), confirming the same conclusion. He read the results at the Royal Society on November 24, 1831; the paper appeared in the *Philosophical Transactions* in 1832 as the first of his *Experimental Researches in Electricity* series.

**Source — primary:** Faraday, M. "Experimental Researches in Electricity. First Series." *Philosophical Transactions of the Royal Society of London* 122, 125–162 (1832). Open access via the Royal Society: https://royalsocietypublishing.org/doi/10.1098/rstl.1832.0006

**Joseph Henry, Albany Academy, summer 1830.** Henry, working alone in the United States, had observed essentially the same effect roughly a year earlier than Faraday's iron-ring experiment — but he didn't publish until 1832, after Faraday's paper had appeared. Henry was busy with electromagnets (he had built a 750-pound electromagnet for Yale in 1831, capable of lifting more than a ton). He did publish self-induction in 1832, the first to identify *that* specifically distinct effect (a coil inducing an EMF in itself).

The convention is to credit Faraday with the discovery because he published first and worked out the phenomenology more thoroughly; the SI unit of inductance, the henry, honors Henry's independent discovery. Both men corresponded after the fact and acknowledged each other's priority on different aspects.

**Source — primary (Henry):** Henry, J. "On the production of currents and sparks of electricity from magnetism." *American Journal of Science and Arts* 22, 403–408 (1832). The paper is short and reads cleanly today.

**Source — historical synthesis:** Williams, L. P. *Michael Faraday: A Biography.* New York: Basic Books, 1965. The definitive biography; Chapter 4 covers the 1831 induction work in detail.

**Maxwell's mathematical formulation, 1855–1865.** Maxwell wrote three foundational papers translating Faraday's pictorial field theory into mathematics. (i) "On Faraday's lines of force" (1855), the first attempt. (ii) "On physical lines of force" (1861–1862), where the displacement current first appears. (iii) "A dynamical theory of the electromagnetic field" (1865), the canonical statement of the four equations and the wave-speed calculation. Faraday's law appears in (iii) in its familiar form. The 1865 paper is open-access at the Royal Society: https://royalsocietypublishing.org/doi/10.1098/rstl.1865.0008

For the Ch 10 chapter, treat Faraday and Henry symmetrically (give Faraday discovery priority and Henry the unit), and *do not* try to recapitulate Maxwell's contribution — that belongs in Ch 11.

### Case 2: The electrical grid and high-voltage transmission

**Why high voltage.** A transmission line of resistance R carrying current I dissipates power P_loss = I²R as heat. To move power P from generator to load, you can choose any combination of V and I with V·I = P. Doubling V halves I, which *quarters* the loss. The dependence on V is dramatic: at V = 345 kV (a standard US transmission voltage) versus V = 240 V (residential), the same power delivered through the same wire dissipates a factor (345000/240)² ≈ 2 × 10⁶ less.

This is why every long-haul transmission line in the world runs at 100s of kV: 230 kV, 345 kV, 500 kV, 765 kV are the standard US "extra high voltage" classes; 1100 kV "ultra-high voltage" lines exist in China (Changji–Guquan line, 1100 kV DC, commissioned 2019).

**The transformer chain.** Modern grid voltage stages, US convention:
- Generator: ~25 kV at the power plant (mechanical insulation limits).
- Step-up transformer at the plant → 345 kV (or up to 765 kV) for long-distance transmission.
- Step-down at regional substation → ~69 kV for sub-transmission.
- Step-down at neighborhood substation → ~12.5 kV for local distribution.
- Step-down at pole-pig or pad-mount transformer → 240 V split-phase for residential (giving 120 V per leg).

Each transformer is two coils on a laminated iron core; each obeys V₂/V₁ = N₂/N₁; each loses 1–3% to copper losses, iron eddy-current losses, and hysteresis. Big utility transformers achieve 98–99.5% efficiency.

**"Roughly 99% of US electricity comes from Faraday induction."** This claim is in TIKTOC. Verifying: the EIA reports that in 2024, US net electricity generation was 4178 TWh, with ~85% from sources requiring a spinning generator (coal 16%, natural gas 43%, nuclear 19%, hydro 6%, wind 10%) and ~15% from photovoltaic solar plus a sliver from other non-Faraday sources (battery discharge from non-Faraday charging, fuel cells). [verify exact 2024 numbers in EIA Electric Power Monthly]. So "the vast majority — closer to 85–90% in 2024 — is Faraday induction" is the safer phrasing than "99%." The claim was closer to 99% in earlier decades when PV solar share was negligible.

**Source:** US Energy Information Administration, "Electricity Explained," https://www.eia.gov/energyexplained/electricity/. EIA Electric Power Monthly tables for current generation mix by source.

### Case 3: Induction cooktops

A flat spiral coil sits ~5 mm below the glass cooktop surface. A power electronics module drives it at 20–50 kHz (commonly ~25 kHz) with currents of order 25 A peak. The coil's AC magnetic field penetrates the glass (non-magnetic, non-conducting at these frequencies) and induces eddy currents in any ferromagnetic pan placed on top. The pan heats from I²R losses in its own bulk; the cooktop surface itself stays cool (warmed only by conduction from the pan back through the glass).

**Why ferromagnetic.** Two reasons: (i) high μ_r concentrates the flux at the pan bottom rather than letting it spread away (boosts coupling); (ii) the skin depth δ = √(2/(σμω)) is small for ferromagnetic materials at 25 kHz (~0.1 mm for cast iron), so the induced eddy currents are concentrated near the pan surface where they can dissipate efficiently. Aluminum and copper have low μ_r and large skin depths at 25 kHz, so they couple poorly and barely heat. Some recent "all-metal" induction cooktops use much higher frequencies (>100 kHz) to compensate, but they remain niche.

**Power transfer.** A 1.8 kW domestic burner moves ~80% of input power into the pan; a 3.6 kW commercial burner moves more. Boiling 1 L of water in ~60 seconds is the rough benchmark, vs. ~150 s on a typical electric resistive coil.

**Source:** Lucia, O., Maussion, P., Dede, E. J., & Burdio, J. M. "Induction heating technology and its applications: past developments, current technology, and future challenges." *IEEE Transactions on Industrial Electronics* 61(5), 2509–2520 (2014). https://ieeexplore.ieee.org/document/6661334

### Case 4: Wireless charging (Qi standard) and magnetic resonance

The **Qi standard** (pronounced "chee"), maintained by the Wireless Power Consortium since 2008, drives ~110–205 kHz between a transmit coil in the pad and a receive coil in the phone. The two coils are weakly coupled (k ≈ 0.3–0.7 depending on alignment), so they form a *mutual-inductance* system, not an iron-core transformer. Power transferred: 5 W (Qi v1.1), 15 W (Qi v1.3 Extended Power Profile), 15 W with magnetic alignment (Qi2, 2023, which adopts Apple's MagSafe magnet ring as the alignment mechanism).

Efficiency is heavily alignment-dependent: 70–85% with good alignment, dropping to 50% or worse with offsets of ~1 cm. Apple's MagSafe (2020) added a ring of permanent magnets around the coil specifically to enforce alignment; Qi2 (2023) standardizes the same mechanism for the broader ecosystem.

**Magnetic-resonance coupling.** Standard Qi inductive coupling falls off rapidly with separation: 5 mm is fine, 30 mm is impractical. Magnetic *resonant* coupling (Soljačić, MIT, 2007) tunes both coils to the same resonant frequency, dramatically reducing the off-axis coupling losses and extending practical separation to 10–50 cm. Commercial implementations (AirFuel Resonant, Apple's 2020 prototype) exist but remain less standard than Qi. The physics is still Faraday induction; the engineering trick is using resonance to make a weakly-coupled system behave like a strongly-coupled one.

**Source — Qi:** Wireless Power Consortium, "Qi Specifications," https://www.wirelesspowerconsortium.com/. Free access to the public-facing specifications.
**Source — magnetic resonance:** Kurs, A. et al. "Wireless power transfer via strongly coupled magnetic resonances." *Science* 317, 83–86 (2007). https://www.science.org/doi/10.1126/science.1143254

### Case 5: MRI gradient coils

The static main field of an MRI scanner (1.5 T, 3 T, or 7 T) is set by the superconducting solenoid covered in Ch 9. *Spatial encoding* uses **gradient coils** that add a position-dependent perturbation to the main field, switching on and off in microseconds during the imaging sequence. Each switch is a dB/dt event; each event induces eddy currents in nearby conductors — and, by Faraday's law, in patient tissue.

The induced electric field in tissue is roughly E ≈ (r/2) dB/dt for a cylindrical region of radius r. For dB/dt ~ 50 T/s (typical of a fast EPI gradient) and r = 0.2 m: E ≈ 5 V/m. This is just below the threshold for peripheral nerve stimulation in healthy tissue (~ 6–10 V/m, by FDA guidance). Modern fast gradient systems are *gradient-limited by nerve stimulation*, not by hardware capability. Patients in fast-imaging sequences may feel tingling in the arms or fingers.

This is the chapter's example of Faraday's law operating *in vivo* — the imaging that diagnoses you also induces measurable currents in your body, and the engineering trade-off is real.

**Source:** Schaefer, D. J., Bourland, J. D., & Nyenhuis, J. A. "Review of patient safety in time-varying gradient fields." *Journal of Magnetic Resonance Imaging* 12, 20–29 (2000). https://onlinelibrary.wiley.com/doi/10.1002/1522-2586(200007)12:1<20::AID-JMRI3>3.0.CO;2-Y

### Failure case: when Faraday's flux rule is misleading (Feynman's homopolar paradox)

Feynman's *Lectures on Physics* Vol. II, §17-2, presents a "paradox" of Faraday's law: a homopolar disk generator (Faraday's own 1831 disk) produces an EMF even though, if you draw the obvious circuit loop, the flux through it is not changing. The resolution is that the **flux rule** ε = −dΦ_B/dt assumes a well-defined material circuit boundary; when conduction paths are through sliding contacts or rotating bulk, you must go back to the underlying ∮**E**·d**ℓ** + ∮(**v**×**B**)·d**ℓ** form. The two are *equivalent* on circuits with definite boundaries; they can diverge on circuits where the boundary itself is ambiguous.

For an intro chapter, this is a footnote. But it's worth a sentence somewhere: "Faraday's law as we have written it presupposes a well-defined loop. Subtle cases (rotating disks, sliding contacts) require care, and we'll see them in advanced electrodynamics." This protects against students applying ε = −dΦ_B/dt to genuinely subtle geometries and getting wrong answers.

**Source:** Feynman, R. P., Leighton, R. B., & Sands, M. *The Feynman Lectures on Physics, Vol. II*, §17-2. Caltech, open access: https://www.feynmanlectures.caltech.edu/II_17.html

---

## C. Connections and dependencies

**Prerequisites (what reader must already know):**
- **Ch 5 (Capacitance, dielectrics, RC circuits).** The RL circuit derivation is structurally parallel to the RC circuit; students should be able to write Kirchhoff's voltage law for a single-loop RL circuit. The "energy in the field" interpretation of capacitor energy (½CV² = ∫u_E dV) sets up the magnetic analogue.
- **Ch 6 (Current, Ohm's law).** EMF drives current through resistance; basic V = IR and P = I²R.
- **Ch 7 (DC circuits).** Kirchhoff's loop rule; multi-loop reasoning.
- **Ch 8 (Magnetic force).** The Lorentz force F = q**v**×**B** is essential to the motional-EMF derivation.
- **Ch 9 (Sources of B).** Magnetic flux definition (Φ_B = ∫∫**B**·d**A**, weber unit); B-field from a long solenoid (B = μ₀nI, derived via Ampère); right-hand rule for B around currents. Magnetic energy density anticipated.

**Unlocks (what this chapter makes possible):**
- **Ch 11 (Maxwell's equations).** Faraday's law *is* Maxwell's third equation. Ch 11 will write it in differential form ∇×**E** = −∂**B**/∂t and pair it with the new displacement-current term in Ampère's law to derive the wave equation. The "changing B makes E" intuition built here is half of the wave mechanism.
- **Ch 11 also reuses u_B = B²/(2μ₀)** as half the EM-wave energy density u = ½ε₀E² + B²/(2μ₀).
- **Ch 12 (Capstone).** Generators, transformers, motors, wireless power, MRI — all are application territory the capstone draws on. The grid as the "macroscopic Faraday machine" is a natural capstone vignette.

**Adjacent chapter connections:**
- **Ch 9 → Ch 10.** Ch 9 supplies the *static* B-field from currents; Ch 10 makes that B *change* and watches the consequences. The pair are the two halves of magnetostatics-meets-time-dependence.
- **Ch 10 → Ch 11.** The asymmetry Maxwell noticed in 1861 is between Faraday's law (which Ch 10 establishes) and the un-augmented Ampère's law (Ch 9). Ch 11's displacement current restores the symmetry. Ch 10 should *flag* the asymmetry without resolving it — Ch 11's payoff depends on the asymmetry being felt as a missing piece.

---

## D. Current state of the field

**Settled:**
- Faraday's law (integral and differential forms), Lenz's law, motional EMF, sinusoidal generator output, mutual and self-inductance, transformer turns/current ratios in the ideal limit, exponential RL dynamics, magnetic energy density u_B = B²/(2μ₀). All textbook physics for 160+ years and confirmed in every working power grid.
- The historical priority dispute Faraday/Henry was settled by the late 19th century: Faraday first to publish, Henry independent and first on self-inductance. The henry unit honors Henry; the farad and the law honor Faraday.
- Transformer efficiency >98% achievable in large units; this is a mature engineering envelope.
- AC line frequencies (50 Hz Europe/Africa/most of Asia; 60 Hz North America, much of Japan, parts of South America) are settled by installed infrastructure.

**Contested or emerging:**
- **HVDC vs. HVAC transmission.** Historically AC won (the "war of currents," Tesla–Westinghouse vs. Edison) because of the transformer. High-voltage DC has been re-emerging since the 1950s for long-distance transmission (lower line losses, no skin effect, easier subsea), with solid-state converters at each end. The 2019 Changji–Guquan ±1100 kV DC line in China is currently the world's most powerful; commissioned 2019 with a 3300 km route and 12 GW capacity. For continental-scale interconnection (e.g., the proposed Sun Cable from Australia to Singapore), HVDC is the only practical choice. Faraday's law still runs both ends — generation is AC, conversion to DC happens after generation. ([verify Sun Cable status: as of late 2025, the project was undergoing ownership changes; check current state])
- **Grid-scale flywheel energy storage.** Spin a heavy rotor up using an induction motor, retrieve the energy by running the same machine as a generator. Round-trip efficiency ~85–90%, response time milliseconds. Increasingly deployed for grid frequency regulation as renewable penetration rises. Beacon Power's 20 MW Stephentown plant (2011) was an early flagship; the technology has matured since. The induction motor/generator is the Faraday law of this chapter, run in both directions.
- **Wireless EV charging.** SAE J2954, finalized in its current form in 2020, specifies inductive coupling at 85 kHz for vehicles up to 11 kW (J2954/1, light-duty) and is being extended to 50 kW+ for heavy-duty (J2954/2, in development as of 2025). Pad-to-vehicle gaps of 100–250 mm are routine; alignment is the engineering frontier. The standard sits on top of Faraday induction exactly as Qi does at smaller scale.
- **Magnetohydrodynamic (MHD) generators.** Run a conducting fluid (ionized gas, liquid metal, plasma) through a magnetic field; the Lorentz force separates charges and you tap the EMF off the channel walls. Faraday's first 1832 paper actually proposed running such an experiment in the Thames; the conductivity of river water was insufficient. Modern interest is in topping-cycle MHD on fossil/nuclear plants and in fusion-reactor exhaust energy recovery. No commercial-scale MHD plant currently operates; research-scale experiments continue (e.g., the High-Performance Demonstration Experiment at NETL).
- **The 2019 SI redefinition of the ampere.** Reframes the SI base unit of current via the fixed value of the elementary charge. This doesn't change Faraday's law but does change how transformers, generators, etc. are formally calibrated. Ch 9 flags this; Ch 10 needs to be consistent.

**Key references:**

1. **Faraday, M.** "Experimental Researches in Electricity. First Series." *Phil. Trans. R. Soc.* 122, 125–162 (1832). The primary source. https://royalsocietypublishing.org/doi/10.1098/rstl.1832.0006
2. **Henry, J.** "On the production of currents and sparks of electricity from magnetism." *Am. J. Sci. Arts* 22, 403–408 (1832). Co-discovery and self-inductance.
3. **Maxwell, J. C.** "A dynamical theory of the electromagnetic field." *Phil. Trans. R. Soc.* 155, 459–512 (1865). The mathematical formulation of Faraday's law. https://royalsocietypublishing.org/doi/10.1098/rstl.1865.0008
4. **Serway, R. A. & Jewett, J. W.** *Physics for Scientists and Engineers*, Chapters 31 (Faraday) and 32 (Inductance). The canonical undergraduate presentation.
5. **Griffiths, D. J.** *Introduction to Electrodynamics*, 4th ed., Chapter 7. Cleaner derivations than Serway; the standard for advanced undergraduate work.
6. **Feynman, R. P., Leighton, R. B., & Sands, M.** *The Feynman Lectures on Physics, Vol. II*, Chs 16–17. Especially §17-2 on the "two laws masquerading as one" (motional EMF + flux rule) and the homopolar paradox.
7. **Williams, L. P.** *Michael Faraday: A Biography.* Basic Books, 1965. Definitive history of Faraday's working life and the 1831 discovery in context.
8. **Lucia, O. et al.** "Induction heating technology and its applications." *IEEE Trans. Industrial Electronics* 61(5), 2509–2520 (2014). The engineering survey for induction cooktops and industrial induction heating.
9. **Kurs, A. et al.** "Wireless power transfer via strongly coupled magnetic resonances." *Science* 317, 83–86 (2007). The magnetic-resonance trick that extended wireless power beyond the few-mm Qi regime.
10. **US EIA.** "Electricity Explained" and Electric Power Monthly. https://www.eia.gov/energyexplained/electricity/. For current US grid statistics.
11. **SAE International.** J2954 standard. https://www.sae.org/standards/content/j2954/. For wireless EV charging.

**Recent developments (last 3 years):**

- **Qi2 (December 2023).** Wireless Power Consortium release adopting magnetic alignment (the Apple MagSafe ring) as the alignment mechanism for 15 W charging. Reduces user error and improves coupling efficiency.
- **SAE J2954/2 in active development.** Heavy-duty wireless EV charging at 50–500 kW.
- **High-voltage DC line buildout.** China's State Grid commissioned the world's first ±1100 kV DC line (Changji–Guquan) in 2019; multiple new HVDC lines are being built worldwide to integrate large remote renewable plants. The transformer is no longer the only voltage-conversion technology — but generation still depends on Faraday induction.
- **Magnetic-resonance wireless transfer for medical implants.** Cochlear implants, deep-brain stimulators, and emerging "leadless" cardiac pacemakers use percutaneous resonant inductive links. Beating standard Qi for these biomedical applications because of separation and alignment constraints.
- **The 2019 ampere redefinition** continues to filter through engineering pedagogy and instrument calibration documentation.

---

## E. Teaching considerations

**Where students get stuck:**

- **Confusing flux with field magnitude.** The most common conceptual error. Φ_B = BA cos θ has *three* factors, and a change in *any* of them produces an EMF. Students will compute ε = −dB/dt and forget about the area, or compute ε = B dA/dt and forget about the angle. Recommendation: explicitly drill all three modes (changing B, changing A, changing θ) before any application.
- **Thinking induction requires motion.** A stationary loop in a changing B (e.g., next to a wire carrying ramping AC) experiences an EMF; nothing has to move mechanically. Transformer secondary is exactly this geometry. Recommendation: present the iron-ring (Faraday 1831) experiment as the first example, *before* the more memorable bar-magnet-through-coil demo, precisely because the iron-ring case has no moving parts.
- **Lenz's law as a separate principle.** Pedagogically convenient, conceptually wrong. The minus sign in Faraday's law *is* Lenz's law. Recommendation: derive Lenz from energy conservation, then state Faraday's law with the explicit minus sign, then say "the minus sign here is what we just derived." Avoid presenting them as two laws.
- **Right-hand rule sign confusion.** "Which way is the induced current?" requires combining three right-hand-rule applications: the direction of B from the source, the direction of the area vector A, the direction of the induced current relative to A. Students lose the chain. Recommendation: do worked examples that step through each rule explicitly; don't collapse the reasoning to "by Lenz, the current goes this way."
- **Self-inductance as paradoxical.** "A coil opposes a current — but the same current produced the field in the first place!" The non-paradox: the field is fine, what the coil opposes is *change* in the field, which means *change* in the current. At steady state, dI/dt = 0, no back-EMF, no opposition. Recommendation: emphasize that the inductor's back-EMF is proportional to dI/dt, not I.
- **RL circuit time constant direction.** Students apply RC intuition (bigger R → slower) and get the RL constant backwards (in RL, bigger R → *faster*, because τ = L/R). Recommendation: derive τ from the ODE, don't import the RC formula.
- **Where the energy comes from in a motional-EMF circuit.** Students see I²R dissipating in the resistor and ask "where did that energy come from? The magnetic field?" No — from the mechanical work done against the Lenz-law retarding force on the moving rod. Recommendation: compute mechanical power and electrical power side-by-side in the worked example, show they balance exactly.

**Analogies and framings that work:**

- **"The coil is a small magnetic generator that just woke up."** When flux through a coil changes, the coil's induced current flows in whichever direction makes the coil *itself* a magnet opposing the change. The framing makes Lenz's law intuitive: "the coil pushes back."
- **"An inductor is a flywheel for current."** A spinning flywheel resists changes in rotational speed; an inductor resists changes in current. Both store energy in motion (mechanical for the flywheel, magnetic-field for the inductor). The analogy fails at higher harmonics (the inductor has no "moment of inertia tensor"), but for the basic τ = L/R intuition it works.
- **"A capacitor stores energy in the electric field; an inductor stores it in the magnetic field; that's the whole symmetry."** This sets up the Ch 11 punchline that EM waves carry equal energy in **E** and **B**.
- **The transformer as a coupled pair of inductors with shared flux.** Once self-inductance and mutual inductance are defined, the transformer is just M-coupling with N₁ and N₂ turns. Calling it a "transformer" rather than "two coupled inductors" sometimes obscures the underlying mechanism.

**Exercises that build the target skill:**

- **Square loop entering a uniform B (TIKTOC Worked Example #1).** A square loop of side L, resistance R, enters a region of uniform B at velocity v. Compute (a) the EMF as a function of position, (b) the induced current, (c) the force on the loop from the field, (d) the mechanical power required to push the loop in. Tests every piece — flux from BA, time-derivative as the loop crosses the boundary, Lenz-law force direction, energy ledger. Bloom: Apply + Analyze.
- **Generator output (TIKTOC Worked Example #2).** N = 100 turns, A = 0.01 m², B = 0.5 T, ω = 60π rad/s. Find peak EMF and frequency. Answer: ε₀ = NBAω = 100·0.5·0.01·60π = 30π ≈ 94 V; f = ω/(2π) = 30 Hz. Direct application of ε(t) = NBAω sin ωt. Bloom: Apply.
- **RL circuit (TIKTOC Worked Example #3).** L = 2 H, R = 10 Ω, ε = 20 V. (a) Final current ε/R = 2 A. (b) Time constant τ = L/R = 0.2 s. (c) Time to 90%: t = τ ln 10 = 2.303·0.2 = 0.46 s. (d) Energy stored at steady state: U = ½LI² = ½·2·4 = 4 J. Bloom: Apply + Analyze.
- **Transformer voltage and current ratios (phone charger).** Primary 1000 turns at 120 V, secondary delivering 5 V at 2 A. Find secondary turns and primary current. N₂ = 1000·(5/120) = 42; I₁ = (5·2)/120 = 83 mA. The arithmetic is the lesson: voltage steps down by 24×, current steps up by 24×. Bloom: Apply.
- **Falling magnet in a copper tube (qualitative + estimate).** Drop a small neodymium magnet down a 1 m copper tube of inner diameter slightly larger than the magnet. The magnet takes ~10× longer to fall than a non-magnetic object. Estimate the induced EMF and the dissipated power. Tests Lenz reasoning, eddy-current physics, and energy bookkeeping. Bloom: Analyze + Synthesize.
- **Why transformers laminate their cores.** Compare eddy-current loss in a solid iron rod of radius a in a sinusoidal B-field B₀ sin ωt vs. the same volume of iron split into N thin laminations. Solid-rod loss scales as a²; lamination loss scales as (a/N)². The factor N² reduction is the punchline. Bloom: Synthesize.
- **Faraday-disk (homopolar) generator.** A copper disk of radius R rotates at ω in a uniform axial B. Each radial element of the disk moves at v(r) = ωr; the motional EMF from the rim to the axle is ε = ∫₀^R Bωr dr = ½BωR². Numerical: R = 0.1 m, B = 1 T, ω = 100 rpm = 10.5 rad/s gives ε ≈ 0.05 V. Connects to Ch 11 (Maxwell's view of where the EMF "comes from") and to MHD generators. Bloom: Analyze. (This is TIKTOC Exercise 23.13 in the archived draft; keep in some form.)
- **Specification exercise.** Given a 50 Hz transmission line carrying 500 MW at 400 kV, compute (a) the line current, (b) the line resistance that would give 1% power loss, (c) the same calculation if the voltage were 40 kV. The 100× difference in loss for the same wire is the lesson. Bloom: Apply + Evaluate.

**The simulation `10-faraday-induction.html` should let students:**
- Drag a bar magnet (with N/S labeled) toward and away from a coil at controlled velocity.
- Adjust coil turns N and coil area A.
- See the flux Φ_B(t) through the coil as a time-series trace.
- See the induced EMF ε(t) = −N dΦ_B/dt as a parallel trace.
- See the induced current direction (arrow on the coil, color-coded for Lenz prediction).
- An ammeter reading that updates in real time.

The student is expected to verify: faster motion → larger EMF; reversed motion → reversed current direction; doubling N doubles EMF; doubling A doubles EMF (at constant B). A stretch goal is a "reverse-engineer" mode where the simulation moves the magnet and the student predicts the induced current direction before seeing the answer.

---

## F. Library files relevant to this chapter

None directly relevant. (Library scan documented in pantry/README.md.)

---

## G. Gaps and flags

- **FLAG — Faraday/Henry priority.** Present both names. Faraday for discovery and the law; Henry for the unit and self-inductance. Do not call Faraday the "sole" discoverer.
- **FLAG — "99% of US electricity from Faraday induction."** The TIKTOC bullet overstates the current fraction; with PV solar at ~15% of US generation in 2024, the more accurate phrasing is "the vast majority — roughly 85% in 2024, and >95% globally — comes from spinning generators that obey Faraday's law." Adjust the prose accordingly. Cite EIA.
- **FLAG — The asymmetry between Faraday (Ch 10) and Ampère (Ch 9).** Faraday's law says changing B drives circulating E; the un-augmented Ampère's law says current (only) drives circulating B. *Mention* this asymmetry at the end of Ch 10 ("a missing piece — we'll see in Ch 11 that there's a third source of B that's been hiding in plain sight") so Ch 11's payoff lands. Do NOT resolve it in Ch 10; the displacement current belongs to Ch 11.
- **FLAG — The flux-rule failure case (Feynman's homopolar paradox).** Mention in a single sentence or footnote: ε = −dΦ_B/dt assumes a well-defined circuit boundary; subtler cases require returning to ∮**E**·d**ℓ** plus motional terms. Do not derail into the full analysis.
- **GAP — The archived OpenStax chapter conflates Ch 10 with AC circuits.** That archived chapter (chapters/_archive/09-electromagnetic-induction-ac-circuits-and-electrical-technologies.md) covered Faraday + Lenz + inductance + RL + RLC resonance + impedance + the AC grid in one chapter. The TIKTOC version for *this* book pulls AC circuits out (they're either earlier in Ch 7 or absent depending on TIKTOC scope) and stops at the inductor and RL. Do not import the RLC-resonance material from the archive; that's not in the Ch 10 TIKTOC scope. Inductive reactance (X_L = ωL) can be *named* in passing but not developed.
- **GAP — Transformer ideal-limit assumptions are buried in the archived chapter.** Spell them out in Ch 10: (i) all primary flux passes through the secondary (no leakage); (ii) core has infinite permeability (no magnetizing current required); (iii) no resistance in either winding (no copper loss); (iv) no eddy currents or hysteresis in the core. Real transformers violate each by 1–3%; the cumulative real efficiency 98–99% is what the ideal model predicts when those losses are small.
- **GAP — Motional EMF derivation pathway.** Two paths are equivalent: (a) Faraday on the loop with growing area, (b) Lorentz force on charges in the moving rod. Show both, state they agree. Don't pick one and ignore the other — the equivalence is itself a teachable moment and a foreshadowing of relativity (Ch 12 / capstone).
- **FLAG — 2019 SI redefinition consistency.** Ch 9 commits to teaching the post-2019 ampere (elementary charge fixed). Ch 10 should be consistent: when defining the henry (H = V·s/A), do not anchor to the pre-2019 "force-between-parallel-wires" definition of the ampere.
- **GAP — One specific chapter exercise on PER-tested misconception.** The "stationary loop with changing B produces an EMF" claim is a known sticking point. Include at least one exercise where motion is *explicitly* absent and the EMF comes from a time-varying B (e.g., a small loop inside an MRI scanner during a gradient switch). This forces students to confront the misconception directly. PER work by Maloney, McKagan, and others has documented this; see Maloney, D. P. et al., "Surveying students' conceptual knowledge of electricity and magnetism," *Am. J. Phys.* 69, S12 (2001).
- **FLAG — Hand-off to Ch 11.** The closing sentence of Ch 10 should plant the seed: "Changing magnetic flux makes an electric field. By symmetry, you might ask: does a changing electric flux make a magnetic field? Maxwell asked, and the answer turned out to predict light." That sentence is the bridge.

---

*End of research notes for Chapter 10 — Electromagnetic Induction and Faraday's Law.*
