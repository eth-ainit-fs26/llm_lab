# HANDOFF — Section 5 lecture for ETH managers

**Branch:** `claude/agentic-ai-research-agents-nZnmj`
**Last updated:** 2026-04-12 by the web Claude Code session
**Status:** 4 of 6 deliverables committed; 2 remaining (lecture notes + Beamer slide deck)

---

## Context for Claude Code on the laptop

You (Claude Code) are picking up work on a 90-minute executive lecture for ETH Zurich.

**Audience:** senior managers, analytical backgrounds, no ML specialisation.

**Title:** *"How Close Are We to AGI? A Reality Check for Decision-Makers"*

**The user previously worked on this via a web Claude Code session. That session could not complete two long LaTeX documents due to response-length and timeout limits. Finish them locally, where you don't have those constraints.**

---

## What's already in the repo (under `section5_agi_for_managers/`)

| File | Status | Purpose |
|---|---|---|
| `section5.bib` | ✅ Done | BibTeX for all references |
| `section5_quiz.tex` | ✅ Done | 15-question calibration quiz with answer key |
| `section5_agi_for_managers_companion.txt` | ✅ Done | Session overview, FAQ, discussion Qs, reading list |
| `section5_annotated_bibliography.tex` | ✅ Done | Annotated bibliography (6 anchor + 17 supporting refs) |
| `section5_agi_for_managers_notes.tex` | ❌ **TO DO** | Long-form lecture notes (prose) |
| `section5_agi_for_managers.tex` | ❌ **TO DO** | Beamer slide deck (~30 slides) |

Read the 4 completed files first — they define the voice, structure, and
references. The remaining two must be consistent with them.

---

## The 6 anchor references (the lecture is shaped around these)

1. **Morris et al. (DeepMind), "Levels of AGI"** — arXiv:2311.02462 / ICML 2024
2. **Bubeck et al. (Microsoft), "Sparks of AGI"** — arXiv:2303.12712
3. **Trinh et al. (DeepMind), "AlphaGeometry"** — *Nature* 625, 476–482 (2024)
4. **METR, "Measuring the ability of autonomous agents to complete tasks"** — 2024–2026
5. **Grace et al., "Thousands of AI Authors on the Future of AI"** — arXiv:2401.02843
6. **Bengio, Hinton, Russell et al., "Managing extreme AI risks amid rapid progress"** — *Science* 384, 842–845 (2024)

Full BibTeX entries are in `section5.bib`.

---

## The 90-minute narrative (5 acts)

| Act | Minutes | Anchor | "wait, WHAT?" moment |
|---|---|---|---|
| 1. What IS AGI? | 15 | Morris et al. | DeepMind's own framework puts today's frontier models at "Emerging General AGI" |
| 2. Sparks + specialist breakthroughs | 20 | Bubeck + AlphaGeometry | IMO gold-medal geometry AI, trained on 0 human proofs |
| 3. From chatbots to agents | 20 | METR | Task-horizon doubles every ~7 months |
| 4. When will AGI arrive? | 15 | Grace et al. | HLMI forecast shifted 13 years earlier in one year |
| 5. Managing the transition | 15 | Bengio–Hinton–Russell | Nobel + Turing laureates co-sign governance ask in *Science* |
| Close + Q&A | 5 | — | Revisit opening prediction |

---

## TASK 1 — Write `section5_agi_for_managers_notes.tex` (long-form lecture notes)

**Style reference:** match the existing lecture notes in the repo
(`section1_when_models_surprise_us/section1_lecture_notes.tex`,
`section2_inside_the_black_box/section2_inside_the_black_box_notes.tex`,
etc.). Prose, speaker-ready paragraphs, footnoted citations, no bullet lists.

**Format:**
- `\documentclass[11pt,a4paper]{article}` with `amsmath, amssymb, hyperref, geometry`
- Use `\bibliography{section5}` (the .bib file is already in the same folder)
- Target 15–20 pages compiled

**Structure:**
- Preface (1 paragraph — who this is for)
- §1 What Do We Mean by AGI? (Morris et al. framework; Chollet counterweight)
- §2 Sparks and Specialist Breakthroughs (Bubeck; AlphaGeometry — include the 100M synthetic theorems + 25/30 IMO result; note AlphaProof silver medal 2024)
- §3 From Chatbots to Agents (ReAct → Reflexion → computer-use; METR methodology; the doubling curve; caveats on extrapolation)
- §4 When Will AGI Arrive? (Grace et al. — 2778 researchers, 50% HLMI by 2047, 13-year shift, 38% give ≥10% to extreme outcomes)
- §5 Managing the Transition (Bengio et al. Science 2024; the four governance asks; manager playbook)
- Closing: "The question is not whether AGI is coming. The question is whether your organisation has the evaluation capability to tell — month by month, workflow by workflow — what these systems can and cannot do for you."

**Tone:** conversational but precise. Assume an intelligent, skeptical, busy manager. Earn their attention.

---

## TASK 2 — Write `section5_agi_for_managers.tex` (Beamer slide deck)

**Style reference:** match the existing decks in the repo (e.g.,
`section1_when_models_surprise_us/section1_when_models_surprise_us.tex`).

**Format:**
- `\documentclass{beamer}` with Metropolis theme
- One idea per slide, large fonts, generous whitespace
- Use TikZ/pgfplots for diagrams (the METR doubling curve is the key visual)
- Include `\note{}` speaker notes on every content slide (2–4 sentences)
- `\bibliography{section5}` at the end for the reading-list slides

**Slide count:** ~28–32 frames for a 90-min talk (roughly 3 min per slide).

**Slides to include (recommended order):**

1. Title slide
2. Session overview (the 5 acts)
3. Act 1 section-header slide
4. The question everyone is asking
5. Morris et al. 5×2 matrix (build a TikZ table)
6. Where frontier models sit today (Emerging General AGI)
7. Counterweight: Chollet's "Measure of Intelligence"
8. Act 1 takeaway
9. Act 2 section-header
10. Bubeck "Sparks" — the claim
11. Sparks — honest caveats (cherry-picking, early-access)
12. AlphaGeometry setup — the problem
13. AlphaGeometry — architecture (neuro-symbolic hybrid diagram)
14. AlphaGeometry — 25/30 IMO result (bar chart)
15. AlphaGeometry — 100M synthetic theorems (no human proofs)
16. The pattern: domains with verifiers fall fast
17. Act 3 section-header
18. What is an "agent"? (ReAct → Reflexion → computer use)
19. METR methodology (task-horizon metric)
20. METR doubling curve (pgfplots log-scale)
21. Extrapolation: 2027 = workday, 2029 = workweek
22. Honest caveats on extrapolation
23. Act 4 section-header
24. Grace et al. survey — 2778 researchers
25. The 13-year shift (2060 → 2047)
26. The disagreement IS the signal
27. Act 5 section-header
28. Bengio–Hinton–Russell consensus (with signatory headshots or names)
29. The four governance asks
30. Manager playbook (Monday-morning checklist)
31. Closing slide: "The question is not whether AGI is coming..."
32. Reading list / thank-you / Q&A

**Critical visuals to nail:**
- The 5×2 Morris matrix (TikZ table)
- The METR doubling curve (pgfplots)
- The IMO score comparison (bar chart: Bronze 15.2, Silver 22.9, Gold 25.9, AlphaGeometry 25)

---

## Also verify

- `section5.bib` compiles cleanly with biblatex or natbib (the existing decks use natbib).
- All references you cite in notes/slides are in the .bib file. If you need a new reference, add it to `section5.bib` and commit that too.
- Build both PDFs: `latexmk -pdf section5_agi_for_managers_notes.tex && latexmk -pdf section5_agi_for_managers.tex` (or equivalent). Commit the `.pdf` outputs alongside the `.tex` sources — the other sections of this repo do this.

---

## Commit + push when done

```bash
git add section5_agi_for_managers/section5_agi_for_managers_notes.tex \
        section5_agi_for_managers/section5_agi_for_managers.tex \
        section5_agi_for_managers/*.pdf
git commit -m "Add Section 5 lecture notes and Beamer slide deck"
git push
```

---

## When this handoff is no longer needed

Delete `HANDOFF.md` in the final cleanup commit.
