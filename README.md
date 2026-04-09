# llm_lab

Lecture materials for an executive-level lecture on intriguing emergent
properties of large language models. Everything lives on `main` — no need to
hop between branches anymore.

## Layout

```
section1_when_models_surprise_us/     Section 1: When Models Surprise Us
section2_inside_the_black_box/        Section 2: Inside the Black Box
section3_philosophy_of_machine_minds/ Section 3: The Philosophy of Machine Minds
section4_the_dark_side/               Section 4: The Dark Side
unified_presentation/                 50-slide deck combining all four sections
shared/                               agent prompts, research notes, proposals
```

Each section folder contains:
- `*_lecture_notes.tex` / `.pdf` — full lecture notes (long-form prose)
- `*_<title>.tex` / `.pdf` — Beamer slide deck (≈30-minute talk)
- `*_companion.txt` — speaker notes / companion document

## Section index

### Section 1 — When Models Surprise Us
- `section1_when_models_surprise_us/section1_lecture_notes.tex` (+ `.pdf`)
- `section1_when_models_surprise_us/section1_when_models_surprise_us.tex` (+ `.pdf`)
- `section1_when_models_surprise_us/section1_when_models_surprise_us_companion.txt`

### Section 2 — Inside the Black Box
- `section2_inside_the_black_box/section2_inside_the_black_box_notes.tex` (+ `.pdf`) — lecture notes
- `section2_inside_the_black_box/section2_inside_the_black_box.tex` (+ `.pdf`) — original slide deck
- `section2_inside_the_black_box/section2_icl_mesa_reversal.tex` (+ `.pdf`) — focused slide deck on ICL, OPRO, mesa-optimizers, reversal curse
- `section2_inside_the_black_box/section2_inside_the_black_box_companion.txt`

### Section 3 — The Philosophy of Machine Minds
- `section3_philosophy_of_machine_minds/section3_lecture_notes.tex` (+ `.pdf`)
- `section3_philosophy_of_machine_minds/section3_philosophy_of_machine_minds.tex` (+ `.pdf`)
- `section3_philosophy_of_machine_minds/section3_philosophy_of_machine_minds_companion.txt`

### Section 4 — The Dark Side
- `section4_the_dark_side/section4_the_dark_side_lecture_notes.tex` (+ `.pdf`)
- `section4_the_dark_side/section4_the_dark_side.tex` (+ `.pdf`) — slide deck (uses `section4_the_dark_side.bib`)
- `section4_the_dark_side/section4_the_dark_side_companion.txt`

### Unified deck
- `unified_presentation/unified_presentation.tex` (+ `.pdf`) — 50-slide combined deck

## Provenance

This consolidation pulls the latest tip of each of the following branches into
`main`. The branches still exist as backups:

| Folder | Source branch |
|---|---|
| `section1_when_models_surprise_us/`     | `vk/e82c-section-1-intrig` |
| `section2_inside_the_black_box/`        | `vk/da4b-section-2-intrig` |
| `section3_philosophy_of_machine_minds/` | `vk/6a61-section-3-intrig` |
| `section4_the_dark_side/`               | `vk/d111-section-4-intrig` |
| `unified_presentation/`                 | `vk/ef3b-intriguing-emerg` |
| `shared/`                               | identical across all section branches |
