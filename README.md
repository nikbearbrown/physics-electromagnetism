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

---

## What This Book Is

<!-- TODO: populate from chapter content -->

---

## Who This Book Is For

<!-- TODO: populate from chapter content -->

---

## How to Read It

<!-- TODO: populate from chapter content -->

---

## Table of Contents

| Chapter | Title | File |
|---------|-------|------|
| 0 | Chapter 0 — How to Use the Simulations | [chapters/00-how-to-use-the-simulations.md](chapters/00-how-to-use-the-simulations.md) |
| Intro | Introduction | [chapters/00b-introduction.md](chapters/00b-introduction.md) |
| 1 | Chapter 1 — Electric Charge and Coulomb's Law | [chapters/01-electric-charge-coulombs-law.md](chapters/01-electric-charge-coulombs-law.md) |
| 2 | Chapter 2 — The Electric Field | [chapters/02-electric-field.md](chapters/02-electric-field.md) |
| 3 | Chapter 3 — Gauss's Law | [chapters/03-gauss-law.md](chapters/03-gauss-law.md) |
| 4 | Chapter 4 — Electric Potential | [chapters/04-electric-potential.md](chapters/04-electric-potential.md) |
| 5 | Chapter 5 — Capacitance and Dielectrics | [chapters/05-capacitance-dielectrics.md](chapters/05-capacitance-dielectrics.md) |
| 6 | Chapter 6 — Electric Current and Resistance | [chapters/06-current-resistance.md](chapters/06-current-resistance.md) |
| 7 | Chapter 7 — DC Circuits | [chapters/07-dc-circuits.md](chapters/07-dc-circuits.md) |
| 8 | Chapter 8 — Magnetism and the Magnetic Force | [chapters/08-magnetism-magnetic-force.md](chapters/08-magnetism-magnetic-force.md) |
| 9 | Chapter 9 — Sources of Magnetic Fields | [chapters/09-sources-magnetic-fields.md](chapters/09-sources-magnetic-fields.md) |
| 10 | Chapter 10 — Electromagnetic Induction and Faraday's Law | [chapters/10-electromagnetic-induction.md](chapters/10-electromagnetic-induction.md) |
| 11 | Chapter 11 — Maxwell's Equations and Electromagnetic Waves | [chapters/11-maxwells-equations.md](chapters/11-maxwells-equations.md) |
| 12 | Chapter 12 — Capstone: Light, Radiation, and the Unified Field | [chapters/12-capstone-unified-field.md](chapters/12-capstone-unified-field.md) |

---

## Signature Simulations

| Chapter | Topic | Simulation |
|---------|-------|------------|
|  | Chapter 0 | LLM Exercise |
| 1 | Chapter 1 | LLM Exercise |
| 2 | Chapter 2 | LLM Exercise |
| 3 | Chapter 3 | LLM Exercise |
| 5 | Chapter 5 | LLM Exercise |
| 7 | Chapter 7 | LLM Exercise |
| 8 | Chapter 8 | LLM Exercise |
| 9 | Chapter 9 | LLM Exercise |
| 12 | Chapter 12 | LLM Exercise |

---

## The +1 Layer

This book contains a chapter explaining how to use the LLM Exercise blocks embedded across the chapters. Each exercise is a structured prompt the reader can paste into an LLM tool of their choice; the chapter explains the pattern and when each variant applies.

---

## Copyright

Copyright © 2026 Nik Bear Brown. All rights reserved.

Published by Bear Brown, LLC.

No part of this publication may be reproduced, distributed, or transmitted
in any form or by any means without the prior written permission of the
publisher, except in the case of brief quotations in critical reviews and
certain other noncommercial uses permitted by copyright law.

ISBN: [INSERT ISBN]

