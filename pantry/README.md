# Pantry Index

Last updated: 2026-05-16

Scratch storage for fragments, snippets, research notes, and material not yet ready for `chapters/`.
Nothing here is compiled into the book. Move material into `chapters/` when it's ready.

## Research notes

Two passes have been run:
- **Pass 1 (2026-05-14):** Six new-content chapters researched (Chs 00, 03, 05, 09, 11, 12).
- **Pass 2 (2026-05-16):** Three missing TIKTOC chapters researched after chapters/ cleanup archived 10 OpenStax-named duplicates/leftovers — Chs 04, 06, 10. The new chapters/ folder is now TIKTOC-aligned: Ch 01, 02, 03, 05, 07, 08, 09, 11, 12 have drafted chapters; Chs 00, 04, 06, 10 have research notes only and need chapter prose written; the 10 archived files in `chapters/_archive/` are source material for the missing-chapter writers.

| File | Chapter | Description |
|------|---------|-------------|
| `00-how-to-use-the-simulations_notes.md` | Ch 00 | Brutalist three-file system, four-move prompt, D3 v7 vector-field rendering, point-charge first simulation |
| `03-gauss-law_notes.md` | Ch 03 | Flux, Gauss's law derivation from Coulomb via solid angle, symmetry-based Gaussian surfaces, conductor properties, Faraday cage, Earnshaw's theorem, PER on symmetry recognition |
| `04-electric-potential_notes.md` | Ch 04 | ∇×E = 0 → scalar potential exists (independent of Gauss); V = U/q as scalar; equipotential surfaces; eV as unit; clinical/applied cases (ECG, EEG, membrane Nernst, accelerators, HVDC); ~5,650w |
| `05-capacitance-dielectrics_notes.md` | Ch 05 | C = Q/V for canonical geometries, energy density u = ½ε₀E² (energy in the field), dielectric polarization and κ, RC circuit dynamics, modern supercapacitor research |
| `06-electric-current-resistance_notes.md` | Ch 06 | Drude 1900 derivation of Ohm's law; four-speeds-of-electricity (Fermi ~10⁶, thermal ~10⁵, drift ~10⁻⁴, signal ~10⁸ m/s); resistivity table; superconductivity from Onnes 1911 through BCS 1957 through LK-99 2023 retraction; ~6,200w |
| `09-sources-magnetic-fields_notes.md` | Ch 09 | Biot-Savart and Ampère's law, infinite wire and solenoid derivations, parallel-wires force, 2019 SI redefinition of the ampere (e fixed), magnetic materials, magnetic monopole status |
| `10-electromagnetic-induction_notes.md` | Ch 10 | Faraday's law and Lenz as energy conservation; motional EMF; AC/DC generator geometry; transformer math; RL circuit τ = L/R; magnetic energy density; eddy currents; modern applications (Qi/MagSafe, EV wireless charging, MHD); ~6,300w. Flags TIKTOC's "99% US electricity" claim as overstated post-PV. |
| `11-maxwells-equations_notes.md` | Ch 11 | Displacement-current motivation (charging-capacitor inconsistency), wave-equation derivation from curl-of-curl, plane-wave geometry, Poynting vector and energy density, EM spectrum, Hertz 1887–1888 confirmation |
| `12-capstone-unified-field_notes.md` | Ch 12 | Geometric and wave optics from Maxwell, antenna radiation and Larmor formula, photoelectric effect as Maxwell's breakdown, Maxwell-Lorentz covariance and the historical motivation for special relativity, wireless communication |

Each notes file follows the seven-section structure: chapter summary → conceptual foundations → domain examples → connections → field state → teaching considerations → library files → gaps/flags.

## Library files (copied from shared MD library)

None. The shared MD library at `/Users/bear/Documents/CoWork/bear-textbooks/MD` was scanned (272 files); no files were sufficiently E&M-relevant to copy. The library is heavy on non-physics trade books, biographies, and economics/finance — useful for other Bear-textbooks projects but not for this one.

## Other pantry contents

- `README.md` — this file.

## Chapters with substantive existing drafts (no new research needed for this pass)

The following are already in `chapters/` from earlier work and were not re-researched:

| TIKTOC Ch | Existing chapter file | Status |
|---|---|---|
| Ch 1 (Electric Charge / Coulomb) | `chapters/01-electric-charge-and-electric-field.md` | Draft exists |
| Ch 2 (Electric Field) | `chapters/02-static-electricity.md` | Parallel draft from second source |
| Ch 4 (Potential) | `chapters/03-electric-potential-and-electric-field.md` | Draft exists (will need renumber to 04) |
| Ch 6 (Current/Resistance) | `chapters/05-electric-current-resistance-and-ohm-s-law.md` | Draft exists (renumber to 06) |
| Ch 7 (DC Circuits) | `chapters/04-electrical-circuits.md` + `chapters/07-circuits-and-dc-instruments.md` | Two parallel drafts to merge |
| Ch 8 (Magnetic Force) | `chapters/06-magnetism.md` + `chapters/08-magnetism.md` | Two parallel drafts to merge |
| Ch 10 (Faraday) | `chapters/09-electromagnetic-induction-ac-circuits-and-electrical-technologies.md` | Draft exists (renumber to 10) |

A subsequent chapter-writing pass should: (1) draft Ch 0, 3, 5, 9, 11, 12 from the notes here; (2) reconcile and renumber existing drafts to match TIKTOC's order; (3) consolidate the parallel drafts (06+08 → Ch 8; 04+07 → Ch 7; 01+02 → Ch 1+2).

## Flags worth surfacing at chapter-writing time

- **Ch 0 — Brutalist three-file system** is the author's own framework; cite as his work (no academic-pedagogy citation exists). The "four-move prompt" structure is similarly the author's synthesis.
- **Ch 3 — Symmetry recognition** is the hardest skill in Gauss's law; the chapter should teach it explicitly via a symmetry-diagnosis exercise (which symmetric distribution → which Gaussian surface) before any computation.
- **Ch 5 — Series-vs-parallel directionality** is *inverted* relative to resistors; address explicitly and with a derivation.
- **Ch 9 — 2019 SI ampere redefinition** is recent; many textbooks still teach only the 1948 definition. Teach both.
- **Ch 11 — Displacement current motivation** must be physical (charging-capacitor surface-choice problem), not just mathematical. Hertz 1887–1888 deserves a paragraph.
- **Ch 12 — Maxwell-Lorentz covariance** is the chapter's most ambitious thread; keep to one carefully-worked example (current-carrying wire seen from a moving frame) and don't attempt a full tensor presentation.
