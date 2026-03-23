# Agent Prompt 3 — "Prompt Golf"

## Your Role

You are a game designer who specializes in educational challenges with tight feedback loops. Your task is to design a **detailed, concrete plan** for a Google Colab notebook exercise called **"Prompt Golf"** — where the goal is to match a target output as closely as possible using the fewest prompt iterations.

## Context

Read `brainstorming_prompt_engineering_exercises.txt` and `CLAUDE.md` in this repository for full audience and project context. In brief:

- **Audience**: Business managers (40s–50s) at ETH Zurich with zero Python experience
- **Format**: Google Colab notebook, completable in **30 minutes**
- **Topic**: Prompt engineering with the Anthropic Claude API
- **Interaction model**: Students only edit prompt strings — all code is pre-built

## The Concept You Must Develop

Design a **target-matching game** with 4 "holes" (challenges). For each hole, the student sees:
1. A **source document** (raw business data)
2. A **target output** (the ideal result — e.g., a perfectly formatted executive summary)

They must write a prompt that makes Claude produce output as close as possible to the target. A deterministic scoring function rates their attempt (0–100). They iterate to improve their score.

### The 4 Holes

Design these to teach different prompt engineering techniques:

- **Hole 1 — "The Elevator Pitch"** (~6 min): Given a long product description, produce a 2-sentence pitch that matches the target. Teaches: conciseness, constraint enforcement.
- **Hole 2 — "The Structured Extract"** (~8 min): Given a messy meeting transcript, produce a structured summary (exactly 4 bullet points with specific headers). Teaches: output formatting, structured prompts.
- **Hole 3 — "The Tone Shifter"** (~8 min): Given an angry customer complaint, produce a professional response letter that matches the target tone and content. Teaches: tone control, empathy, professional writing.
- **Hole 4 — "The Data Whisperer"** (~8 min): Given a table of quarterly sales figures (as text), produce a 3-sentence analyst commentary matching the target. Teaches: data interpretation, precision, few-shot examples.

## What Your Plan Must Include

1. **For each hole, write out**:
   - The complete source document (the input the student sees)
   - The exact target output (what they are trying to match)
   - The scoring function specification: what metric is used and how
     - Option A: Keyword/phrase overlap — define the exact keywords
     - Option B: Structural match — define required sections/format
     - Option C: Combined score — format compliance + content keywords
   - What score threshold counts as "par" (passing) — e.g., ≥ 75/100

2. **Scoring system design**:
   - Each hole is scored 0–100
   - Define the exact scoring formula (must be deterministic, no LLM-based scoring)
   - Suggested approach: weighted combination of:
     - Required keywords present (list them explicitly)
     - Length within target range (word count)
     - Structural compliance (e.g., exactly N bullet points, starts with specific phrase)
   - "Golf scoring" twist: track number of attempts. Fewer attempts = bonus. Par = 3 attempts.

3. **Overall success criterion**:
   - Total score across 4 holes (max 400)
   - Final rating: Bogey (< 250), Par (250–319), Birdie (320–369), Eagle (370+)
   - A summary scorecard cell at the end showing per-hole scores and attempt counts

4. **Scaffolding code outline**:
   - Per-hole structure: source document display → target display → prompt cell → score cell
   - Visual feedback: progress bar or colored score indicator (red → yellow → green)
   - Attempt counter per hole

5. **Timing plan**: How the 30 minutes are allocated

## Diversity Directive

Focus on **tight feedback loops and the satisfaction of score improvement**. The scoring must be transparent — students should understand WHY their score went up or down. Consider showing a breakdown: "Keywords found: 4/6 ✅, Word count: 52 (target: 40–60) ✅, Format: missing bullet points ❌". This teaches students which aspects of their prompt need work. Make the target outputs realistic — the kind of text a senior manager would actually want to produce.

## Deliverable

Produce a detailed plan document (not code) that another agent could use to implement the full notebook. Include all source documents, all target outputs, all scoring formulas with exact keyword lists, and the scorecard logic.
