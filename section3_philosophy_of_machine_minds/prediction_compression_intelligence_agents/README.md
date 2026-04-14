# Prediction = Compression = Intelligence — Agent Pipeline

Three agent prompts that collaborate to produce a dedicated lecture-note
document focused **only** on the subsection of Section 3 that argues
prediction, compression, and intelligence are the same operation.

## Target audience (two simultaneous readers)

1. **Bachelor students** who have taken calculus, linear algebra, and
   probability. They want every math detail: definitions, theorems,
   proofs or proof sketches, and worked derivations.
2. **Managers** with no math background who need intuition, analogies,
   and worked mini-examples to follow the same results.

The final document must serve both audiences in one linear read, not
two parallel tracks.

## Source material

The canonical content lives in
`../section3_lecture_notes.tex` (Act I, Topic A, §2–§3 roughly):

- Shannon source coding / cross-entropy ↔ code length identity.
- Kolmogorov complexity $K(x)$.
- Solomonoff's universal prior $M(x)$ and induction.
- Hutter's AIXI.

All three agents read from that file as the ground-truth starting point
and may cite `../section3.bib` entries.

## Pipeline

```
            ┌──────────────────┐
            │  math_writer.md  │──┐
            └──────────────────┘  │
                                  ├──▶  synthesizer.md  ──▶  lecture notes .tex
            ┌──────────────────┐  │
            │ youtube_presenter│──┘
            │       .md        │
            └──────────────────┘
```

1. Run `math_writer.md` first. Output: `draft_math.tex` — a rigorous
   math-heavy draft with full derivations.
2. Run `youtube_presenter.md` in parallel (independent of the math
   writer's output). Output: `draft_intuition.md` — analogies, worked
   mini-stories, and concrete numerical examples, organised by the same
   section headings the math writer will use.
3. Run `synthesizer.md` with **both** drafts as input. Output:
   `prediction_compression_intelligence_notes.tex` — the final merged
   notes plus a compiled PDF.

The two drafts share a **fixed section outline** (see `OUTLINE.md`) so
the synthesizer can interleave them cleanly.

## Invoking the agents from Claude Code

Each `.md` file in this folder is a self-contained system prompt. From
a Claude Code session at repo root, launch each as a sub-agent:

```
Agent(subagent_type="general-purpose",
      description="Math writer draft",
      prompt=<contents of math_writer.md>)
```

Then pass both drafts into the synthesizer. The synthesizer prompt
explicitly expects the two drafts as attached context.
