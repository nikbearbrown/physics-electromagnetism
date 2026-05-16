# Physics +1: Electromagnetism

**Author:** Nik Bear Brown
**Series:** Physics +1 (Volume 3)
**Publisher:** Bear Brown, LLC
**Status:** Draft

---

## About this book

*Electromagnetism as the unification project.* This is where the Physics +1 series pays off hardest, because the fields themselves are invisible in nature — and the +1 layer (interactive D3 simulations) gives the student something close to X-ray vision for what charges and currents are doing to the space around them. The narrative arc is the historical one Maxwell completed: separate sciences of electricity and magnetism, then a single field theory with light as its consequence.

Every concept moves from specific scene to first-principles mechanism to named trade-off. Coulomb's law is built from a kite-string experiment in a 1752 thunderstorm and a tank of cleaning fluid in a Russian basement; field lines are introduced as a *tool* and tested against where they break down; Maxwell's equations are aimed at, not asserted.

Audience: intro-physics students who have completed classical mechanics and have working algebra and vector calculus. The 10 chapter drafts in `chapters/` cover the standard E&M sequence (OpenStax-derived); `outline.md` proposes an 8-chapter curation including a new Maxwell's-Equations chapter for the published volume.

## How this directory is organized

```
book.md              ← one-sentence pitch, argument, gap, reader, high-level outline (planning)
outline.md           ← working TOC with D3 simulation notes per chapter
vision.md            ← Tic TOC Phase 1: vision and positioning
architecture.md      ← Tic TOC Phase 2: learning architecture
chapters-spec.md     ← Tic TOC Phase 3: per-chapter specifications
risks.md             ← Tic TOC Phase 4: scope, comparables, adoption risks
pantry/              ← scratch storage for fragments and snippets
chapters/            ← drafts (this is where the book lives)
images/              ← figures and hero images per chapter
styles/              ← Kindle-bound CSS (shared base + book-specific overrides)
build.sh             ← compile the EPUB
graphs.sh            ← process figure-placeholder comments into images/tables
```

## Detailed Table of Contents

### Front Matter

| File | Section |
|------|---------|
| `chapters/00-frontmatter.md` | Title page, copyright, dedication, preface |
| `chapters/00b-introduction.md` | Book-level introduction (template placeholder) |

### Chapters

| # | File | Title |
|---|------|-------|
| 1 | `chapters/01-electric-charge-and-electric-field.md` | Electric Charge and Electric Field |
| 2 | `chapters/02-static-electricity.md` | Static Electricity |
| 3 | `chapters/03-electric-potential-and-electric-field.md` | Electric Potential and Electric Field |
| 4 | `chapters/04-electrical-circuits.md` | Electrical Circuits |
| 5 | `chapters/05-electric-current-resistance-and-ohm-s-law.md` | Electric Current, Resistance, and Ohm's Law |
| 6 | `chapters/06-magnetism.md` | Magnetism: How Moving Charges Make the World Spin |
| 7 | `chapters/07-circuits-and-dc-instruments.md` | Circuits and DC Instruments |
| 8 | `chapters/08-magnetism.md` | Magnetism |
| 9 | `chapters/09-electromagnetic-induction-ac-circuits-and-electrical-technologies.md` | Electromagnetic Induction, AC Circuits, and Electrical Technologies |
| 10 | `chapters/10-electromagnetic-waves.md` | Electromagnetic Waves |

### Back Matter

| File | Section |
|------|---------|
| `chapters/99-back-matter.md` | Acknowledgments, About the Author, References, Index |

## Notes on the chapter set

Chapters 1 & 2 (*Electric Charge and Electric Field* / *Static Electricity*) and chapters 6 & 8 (*Magnetism* / *Magnetism*) are parallel drafts of the same topic from different source textbooks. They are kept side-by-side for now — the curated published outline (see `outline.md`) collapses each pair and adds a new Chapter 8: Maxwell's Equations.

## Build

```bash
./build.sh
```

Output lands in `output/` (gitignored).

## Figures

```bash
./graphs.sh
```

Processes `<!-- → [TYPE: description] -->` comments throughout the chapters:
tabular figures become classed markdown tables; non-tabular figures become
placeholder images in `images/`, ready to replace; CSS log appends to
`styles/kindle-book.css` on each run.

## Publish

Upload `output/physics-plus-one-electromagnetism.epub` to [KDP](https://kdp.amazon.com).
