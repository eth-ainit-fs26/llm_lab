# CLLAUDE — session handoff notes

**Branch:** `claude/agentic-ai-research-agents-nZnmj`
**Last session:** 2026-04-12 (local Claude Code, laptop)
**Last commit on branch:** `42f1fae` — "Add Section 5 lecture notes and Beamer slide deck"

---

## What got finished in the last session

Section 5 of the ETH executive lecture ("How Close Are We to AGI? A
Reality Check for Decision-Makers") is now complete and pushed. All six
deliverables under `section5_agi_for_managers/` exist and are committed:

| File | Status |
|---|---|
| `section5.bib` | done (prior session) |
| `section5_quiz.tex` | done (prior session) |
| `section5_agi_for_managers_companion.txt` | done (prior session) |
| `section5_annotated_bibliography.tex` | done (prior session) |
| `section5_agi_for_managers_notes.tex` + `.pdf` | **done (this session)** — 10 pp |
| `section5_agi_for_managers.tex` + `.pdf` | **done (this session)** — 43 Beamer frames |

`HANDOFF.md` has been deleted, as the original handoff instructed.

The previous web session's handoff doc suggested the notes target 15–20
pages. They came out at 10 pp of dense prose. If the user wants a longer
build (more depth in any act, worked example boxes, a manager's
glossary, etc.), that is the first thing to offer.

---

## Build / compile notes (landmines to avoid)

### Beamer deck

- **Document class option must include `table`** for `\rowcolor` in the
  overview table: `\documentclass[aspectratio=169, 12pt, xcolor={dvipsnames,table}]{beamer}`.
  Without the `table` option you get cascading "Not allowed in LR mode"
  errors that mask the real cause.
- **Do not name a TikZ style `step`.** `step` is a reserved TikZ key
  (used by `\draw ... step ...;` grids). Using it as a node style name
  causes `Package pgfkeys Error: The key '/tikz/step' requires a value`
  with cascading "Not allowed in LR mode" errors. I renamed the agent-
  lineage style from `step` to `stage` — keep it that way.
- The reading-list frame uses `allowframebreaks` because the bibliography
  is too long for one slide. Expect 2–3 pages there.
- Metropolis's `\section{}` command automatically inserts a section-
  header slide on top of my explicit plain section-header slides. That
  is why the deck renders as 43 pages for ~30 logical frames. Not a
  bug, but if someone wants exactly 30 frames, delete either the
  `\section{...}` commands **or** the explicit plain section-header
  frames — not both.

### Lecture notes

- Uses `natbib` with `\citep`/`\citet` and `plainnat` bibliography style,
  matching the convention the existing decks use.
- Builds clean with `latexmk -pdf`. No warnings worth acting on.

### Repo convention

- Other sections commit the `.pdf` alongside the `.tex`. Section 5 now
  follows suit. If the user wants to drop the PDFs and rely on CI build,
  that's a repo-wide conversation, not a section-5 one.

---

## Things a fresh session might want to pick up

Nothing is blocked. Possible next moves, in rough priority order:

1. **User review of Section 5 PDFs.** They are rendered on GitHub at
   `section5_agi_for_managers/section5_agi_for_managers_notes.pdf` and
   `section5_agi_for_managers/section5_agi_for_managers.pdf` on the
   branch above. Iterate based on their feedback (length of notes, tone,
   additional visuals, a live-demo slide, etc.).
2. **Merge `claude/agentic-ai-research-agents-nZnmj` into `main`.** The
   branch currently carries: the agentic-AI research agent prompts
   (`3988e8c`), Section 5 companion + bib + quiz + annotated
   bibliography (`89508df`), and now the notes + deck. A PR to `main`
   would wrap up the Section 5 strand.
3. **Unified presentation consistency.** The repo has a
   `unified_presentation/` directory. Check whether Section 5 needs to
   be stitched in there, or if it's independent.

---

## Repo map (quick orientation for a fresh session)

```
git_llm_lab/
├── README.md
├── section1_when_models_surprise_us/   # scaling, emergence, CoT, grokking
├── section2_inside_the_black_box/       # mech-interp, ICL, reversal curse
├── section3_philosophy_of_machine_minds/
├── section4_the_dark_side/
├── section5_agi_for_managers/           # <-- just completed
├── agentic_ai_frontier/                 # research-agent prompts (Apr commit)
├── shared/
└── unified_presentation/
```

Each section follows the same pattern: a Beamer `.tex` deck, a
`_notes.tex` long-form companion, a `.bib`, a `companion.txt` with
discussion questions and a reading list, and compiled PDFs checked in.
Use `section1_when_models_surprise_us/` or
`section2_inside_the_black_box/` as the style reference when writing
new material.

---

## Working style the user has validated

- They want LaTeX sources + committed PDFs, both pushed, with GitHub
  URLs handed back so they can review in-browser.
- They prefer the "web session starts it, laptop session finishes it"
  split when the work exceeds a single session's comfortable output
  length. A short handoff file (this one, or the prior `HANDOFF.md`) is
  the mechanism.
- They are comfortable with `git push` without asking each time on this
  branch. Do not assume that generalises to `main` — ask before pushing
  anything to `main` or force-pushing.
