# Manager Panel — Critique of the Lecture Notes

Five manager personas audit the notes produced by the math writer and
YouTube presenter. Both authors then join the roundtable and are given
a chance to **defend, clarify, or concede** each critique. A moderator
orchestrates the discussion and issues a final report with prioritized
edits — especially for the analogies.

## Cast

**Panel (critics):**
1. `persona1_cfo.md` — Maria, CFO of a mid-cap manufacturing firm.
   Numbers-native, ROI-focused, hype-averse.
2. `persona2_cmo.md` — David, CMO of a consumer-tech company.
   Storytelling brain, equation-averse, cares about stickiness.
3. `persona3_generalist_ceo.md` — Aisha, CEO of a family-owned retail
   chain. No tech background. "Can my mother follow this?"

**Authors (defenders):**
4. `author_math_writer.md` — same voice as the original math writer.
   Defends mathematical correctness; may concede intuition gaps.
5. `author_showman.md` — same voice as the YouTube presenter.
   Defends and refines analogies; may propose replacements on the fly.

**Moderator:**
6. `moderator.md` — runs the roundtable, produces `panel_report.md`.

## Pipeline

```
Round 1:  persona1..5  ─────▶  reaction_<persona>.md  (parallel)
Round 2:  author_math + author_showman read all 5 reactions
           and produce  author_response_math.md,
                        author_response_showman.md        (parallel)
Round 3:  moderator reads the notes + all 5 reactions
           + both author responses  ─▶  panel_report.md
```

All artifacts land in this folder.

## Inputs everyone shares

- `../prediction_compression_intelligence_notes.tex` (and the compiled
  PDF in the same directory)
- `../OUTLINE.md` (so everyone references sections by the same names)

## What `panel_report.md` must contain

1. A 1-paragraph roundtable summary — who was convinced, who wasn't.
2. An **analogy-by-analogy verdict table**: for each of the ~15
   analogies in the notes, mark ✅ keep / ✏ refine / ❌ replace, with a
   one-sentence rationale drawn from the discussion.
3. A prioritized edit list (P0 = must fix before using the notes, P1 =
   strong improvement, P2 = nice to have). Each edit specifies the
   target section from `OUTLINE.md` and the exact change.
4. An "unresolved disagreements" section where the math writer and
   showman could not agree with a panelist, with both positions
   recorded so the human editor can break the tie.
