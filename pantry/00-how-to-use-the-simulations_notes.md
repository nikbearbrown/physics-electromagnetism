# Research Notes: Chapter 00 — How to Use the Simulations

**Source:** TIKTOC.md chapter entry (Chapter 00)
**Notes file:** 00-how-to-use-the-simulations_notes.md
**Corresponding chapter:** chapters/00-how-to-use-the-simulations.md (not yet written)
**Generated:** 2026-05-14

---

## Chapter summary (from TIKTOC.md)

Pre-chapter / setup. Get the student from zero to a working, modifiable D3 electromagnetic field visualization before they encounter any new physics. Student produces `CLAUDE.md`, `DESIGN.md`, `PROJECT.md` plus a working point-charge field-line visualizer (`00-point-charge.html`). Introduces the four-move prompt (Show / Say / Constrain / Verify) and the Brutalist file system.

Core deliverables for the student by end of chapter:
- Three Brutalist governing files in their working directory
- A working point-charge field-line simulator they can modify
- A mental model of how every subsequent chapter's LLM Exercise will work

---

## A. Conceptual foundations

### The Brutalist three-file system

Three governing markdown files travel with the project across the whole semester. They are not chapter content; they are *constraints on Claude's output* that the student maintains.

- **CLAUDE.md** — coding constitution. Names library (D3 v7), file conventions (single HTML, inline CSS+JS, no external dependencies), physics constants (ε₀, μ₀, k, c), numerical methods (RK4 for field-line integration, finite differences for gradients), animation idioms (`requestAnimationFrame`, pause/play, slider→`input` event for live update), and a verification checklist (does it run? does the physics work in limits?).
- **DESIGN.md** — visual constitution. Color conventions (positive = red, negative = blue, E-lines = dark gray, equipotentials = green dashed, B-lines = purple, current = orange), canvas sizes (700×500 for fields, 700×400 for time-series), font/typography, dark-mode behavior (`prefers-color-scheme`).
- **PROJECT.md** — project state. List of simulations built so far, current chapter, open TODOs. Updated by the student after each chapter.

**Why three files, not one:** the instruction budget. If you cram coding, visual, and state instructions into one file Claude reads on every prompt, the per-prompt context overhead grows linearly with the project. Splitting them lets the student point Claude at only the file relevant to the current move ("read CLAUDE.md and the prompt below" vs. "read DESIGN.md when restyling").

**Common misconception:** that the Brutalist files are "documentation." They are not. They are *prompts to be loaded* — the file *is* the instruction. A `CLAUDE.md` that doesn't change Claude's output isn't doing its job.

### The four-move prompt structure: Show / Say / Constrain / Verify

The atomic unit of work in every chapter's LLM Exercise. Each prompt has four sections in order:

1. **Show** — paste the reference. A wave function, a force law, a desired output picture. Concrete, not abstract.
2. **Say** — name the task in one sentence. "Render the electric field of a point charge as a vector field on a 2D grid."
3. **Constrain** — list the rules. Library (D3 v7), file format (single HTML), variables (q, k, grid resolution), physics (E = kq/r² r̂), what to avoid (no external dependencies, no animation libraries beyond D3).
4. **Verify** — name what the student will check. Does it open in a browser? Do arrows point outward from a positive charge and inward to a negative charge? Does field strength fall as 1/r²?

The student copies the four-move prompt verbatim into Claude. Claude returns code. The student saves to `00-point-charge.html` and opens it.

**Why four moves and not three:** Verification is the move students skip. Without Verify in the prompt, the student doesn't know what "working" means and accepts whatever Claude returns. Naming the verification criteria *in the prompt* trains the diagnostic-reading habit that the textbook teaches in subsequent chapters.

### D3 v7 for field visualization

D3 v7 (released June 2021) is the current major version. Key idioms for E&M visualization:
- SVG canvas: `d3.select('svg').attr('viewBox', '0 0 700 500')`
- Scales: `d3.scaleLinear` for coordinate mappings, `d3.scaleSequential(d3.interpolateRdBu)` for charge-color mapping
- Lines and paths: `d3.line()` with `.curve(d3.curveCatmullRom)` for smooth field lines
- Contours (used in Ch 4 for potentials): `d3.contours()` over a value grid
- Animation: combine `requestAnimationFrame` with D3 selections rather than `.transition()` for live parameter response

Field-line integration is RK4 (4th-order Runge–Kutta) starting from points on a small circle around each charge:

```
For each starting point p₀:
  while p is inside canvas and |E(p)| > ε:
    k₁ = E(p) / |E(p)|
    k₂ = E(p + h k₁/2) / |E(p + h k₁/2)|
    k₃ = E(p + h k₂/2) / |E(p + h k₂/2)|
    k₄ = E(p + h k₃) / |E(p + h k₃)|
    p = p + h (k₁ + 2k₂ + 2k₃ + k₄) / 6
    append p to path
```

Step size h is typically a few pixels. Termination conditions: leave canvas, |E| below threshold (line ended in empty space), or step into another charge.

**Source:** Observable, "Vector field" example, https://observablehq.com/@d3/vector-field ; D3 documentation https://d3js.org/

### The point charge as the first simulation object

Why the point charge: the simplest possible field object. One number (q), one position. Field is radial: E = kq/r² r̂. Field lines are exactly straight radial spokes. The student can verify by eye that lines emerge from a positive charge and converge on a negative charge, that doubling q doubles the line count (under a flux-proportional density rule), and that fields fall off with distance.

**Common misconception:** that field-line density "shows" the field magnitude. In 2D it does, approximately, if line count is chosen proportional to |q|. In 3D rendered to 2D it does not. This is honest to acknowledge in Chapter 2; for Chapter 0 the simplification ("more lines means stronger field") suffices.

### Worked example (the simulation Claude will produce)

The Chapter 0 simulation should:
- Take charge magnitude q from a slider (allow positive and negative)
- Render the charge as a red (+) or blue (−) circle at canvas center
- Compute 16 starting points on a small circle of radius r₀ ≈ 10 px around the charge
- Integrate RK4 outward (or inward for negative charge) until each line exits the canvas
- Draw paths as dark gray SVG `<path>` elements

This is achievable in ~80 lines of HTML+CSS+JS. The student verifies by flipping the sign and watching lines reverse direction.

---

## B. Domain examples and cases

### Case: PhET's Charges and Fields simulation as benchmark

The University of Colorado Boulder PhET simulation "Charges and Fields" (https://phet.colorado.edu/en/simulations/charges-and-fields) is the canonical benchmark for what intro-physics electric-field visualization should do: drag-and-drop charges, field arrows on demand, equipotential lines you can drop with a click. It's the gold standard, and it's the right reference for Chapter 0 to position against — the student is not trying to replicate PhET; they're building a simpler, modifiable, *their own* version that they understand the code for and can extend.

Where PhET succeeds: instant feedback, intuitive controls, robust physics, free, runs in browser. Where the +1 layer adds something PhET doesn't: students *build* the simulation rather than use a black box, so they end up with code they can read and modify for any subsequent topic.

### Case: Coulomb-force simulator (Ch 01 preview)

The Ch 01 simulation will reuse the point-charge file as a building block: multiple charges, force vectors on each, arrows colored by attraction/repulsion. Chapter 0 teaches the student to write the first one; Chapter 1 teaches them to extend it. The architecture (CLAUDE.md drives the file structure; DESIGN.md drives the colors; PROJECT.md tracks state) means the Chapter 1 prompt is incremental, not a from-scratch rewrite.

### Failure case: prompting without constraints

A common student failure mode that this chapter must train against: pasting "make me a simulation of a point charge with field lines" into Claude with no Constrain section. Claude returns *something* — possibly using Three.js, or matplotlib in a Jupyter cell, or a static PNG. The output is unusable for the project, but Claude hasn't done anything wrong; the student didn't constrain. The four-move prompt's purpose is to make constraint a habit before the student needs it.

---

## C. Connections and dependencies

**Prerequisites (what reader must already know):**
- Basic familiarity with terminal/file system (saving an HTML file, opening it in a browser)
- Awareness that Claude/ChatGPT/Gemini can generate code (no prior coding experience required for this book)
- Algebra; the point charge is the only physics in this chapter

**Unlocks (what this chapter makes possible):**
- Every subsequent chapter's LLM Exercise depends on CLAUDE.md/DESIGN.md/PROJECT.md being in place
- The four-move prompt is the cognitive scaffolding for diagnostic prompting through the rest of the book

**Adjacent chapter connections:**
- Ch 1 (Electric Charge and Coulomb's Law): extends the point-charge sim to multi-charge force computation
- Ch 2 (The Electric Field): the same point-charge geometry, now as a full vector-field grid
- All chapters: the verification habit (Verify move) generalizes across every simulation

---

## D. Current state of the field

**Settled:**
- D3 v7 is stable and the right tool for browser-based E&M visualization (Bostock's library, used widely in journalism and education)
- The "render as SVG, animate with requestAnimationFrame, drive parameters with input events" idiom is mature
- LLM-assisted coding (Claude, ChatGPT) is reliable for D3 v7 tasks at the complexity of intro-physics simulations

**Contested or emerging:**
- The pedagogical value of student-built simulations versus pre-built sims (PhET) is actively researched; no clean consensus, but the diagnostic-reading frame (see Quantum Mechanics companion guide for related argument) supports student-built
- Best LLM model for code generation moves quarterly; the book should avoid pinning to "Claude" specifically and allow students to substitute ChatGPT/Gemini

**Key references:**
1. Bostock, M., D3: Data-Driven Documents. https://d3js.org/ — Library home; the v7 documentation is authoritative.
2. PhET Interactive Simulations, "Charges and Fields." https://phet.colorado.edu/en/simulations/charges-and-fields — The benchmark E&M sim.
3. Wieman, C., "PhET: Interactive Simulations for Teaching and Learning Physics." Phys. Teach. 44, 18 (2006). — Pedagogical rationale for sim-based intro physics.

**Recent developments (last 3 years):**
- Claude 3.5 Sonnet and successors generate D3 v7 code reliably at this complexity level
- Browser performance for SVG at 60 fps with 50+ animated elements is essentially solved on modern hardware

---

## E. Teaching considerations

**Where students get stuck:**
- Saving the file with the wrong extension (`.txt` instead of `.html`) — name the extension explicitly in CLAUDE.md
- Opening the file from a non-`file://` context (e.g., trying to load it inside Cowork) — instruct to open in browser directly
- Expecting the simulation to update without re-running RK4 when a slider changes — the live-update idiom needs explicit demonstration

**Analogies and framings that work:**
- "CLAUDE.md is your taste in code, written down once. DESIGN.md is your taste in visuals." — anchors the files as personal artifacts, not configuration
- "The four-move prompt is the recipe; Claude is the kitchen" — anchors the cognitive labor as the student's, not Claude's

**Exercises that build the target skill:**
- *Flip the sign* (Bloom: Apply) — change q from +1 to −1, observe field lines reverse. Tests that the student can locate q in the code and modify it.
- *Add a second charge* (Bloom: Apply) — copy the charge definition, place it elsewhere, render both. Sets up Ch 1's multi-charge sims.
- *Change the color* (Bloom: Apply) — edit DESIGN.md to use a different palette, re-prompt for a restyle. Demonstrates that DESIGN.md is a live instruction, not documentation.

---

## F. Library files relevant to this chapter

None directly relevant. The shared MD library at `/Users/bear/Documents/CoWork/bear-textbooks/MD` is heavy on non-physics trade books; no E&M-pedagogy material that would help this chapter.

---

## G. Gaps and flags

- FLAG: The Brutalist three-file system is documented in Bear's own `brutalist.art` ecosystem but not in widely-cited academic literature. The chapter should be honest that this is the author's framework, not a standard pedagogy term. Cite Brutalist as the author's own work.
- GAP: Best practices for LLM-prompt structure in education are an emerging area; no canonical published rubric exists yet. The four-move prompt should be presented as the author's own synthesis, not a citation-backed standard.
- FLAG: Browser compatibility. The chapter should specify a modern browser (Chrome, Firefox, Safari, Edge — all post-2022) and warn that ancient browsers may not support certain SVG features.
