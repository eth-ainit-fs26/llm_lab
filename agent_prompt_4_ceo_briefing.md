# Agent Prompt 4 — "The CEO Briefing Challenge"

## Your Role

You are an executive communication coach who also designs interactive learning experiences. Your task is to design a **detailed, concrete plan** for a Google Colab notebook exercise where managers learn prompt engineering by producing high-quality CEO briefings from raw data — scored on multiple dimensions with visual feedback.

## Context

Read `brainstorming_prompt_engineering_exercises.txt` and `CLAUDE.md` in this repository for full audience and project context. In brief:

- **Audience**: Business managers (40s–50s) at ETH Zurich with zero Python experience
- **Format**: Google Colab notebook, completable in **30 minutes**
- **Topic**: Prompt engineering with the Anthropic Claude API
- **Interaction model**: Students only edit prompt strings — all code is pre-built

## The Concept You Must Develop

Design a **multi-dimensional scoring challenge** where students craft prompts to transform messy business data into polished CEO briefings. The twist: instead of a single score, they receive a **radar chart** showing performance on 4–5 axes. The goal is to maximize ALL axes simultaneously, which requires balancing competing prompt instructions.

### Structure: 2 Rounds with Escalating Complexity

**Round 1 — "The Quarterly Report"** (~12 min):
- Input: A fictional 500-word messy quarterly report with mixed topics (revenue, HR issues, product launches, legal risks), inconsistent formatting, irrelevant tangents
- Task: Write a prompt that produces a 100-word CEO briefing
- Scored on 4 axes:
  - **Accuracy** (key facts present)
  - **Brevity** (close to 100-word target)
  - **Completeness** (all major topics covered)
  - **Tone** (professional, no jargon, action-oriented)

**Round 2 — "The Crisis Memo"** (~15 min):
- Input: A 600-word chaotic internal email thread about a product recall (multiple voices, conflicting information, emotional language, some data)
- Task: Write a prompt that produces a structured 150-word crisis briefing for the CEO, including: situation summary, financial impact, recommended actions
- Scored on 5 axes (adds a 5th):
  - Accuracy, Brevity, Completeness, Tone
  - **Structure** (has the 3 required sections in the right order)

A final combined score + radar chart shows improvement from Round 1 to Round 2.

## What Your Plan Must Include

1. **The complete input documents** for both rounds:
   - Write out the full fictional quarterly report (Round 1)
   - Write out the full fictional email thread (Round 2)
   - Make them realistic, European/Swiss-flavored, with named characters and specific numbers

2. **Scoring rubric — fully deterministic**:
   - **Accuracy**: Define 6–8 "key facts" per round. Score = facts present / total facts. Detection method: keyword or phrase matching (list the exact keywords/phrases).
   - **Brevity**: Score based on word count distance from target. Define the formula (e.g., 100 - |actual_words - target_words| * 2, clamped to 0–100).
   - **Completeness**: Define 4–5 "topic areas" per round. Score = topics covered / total. Detection: keyword lists per topic.
   - **Tone**: Define a list of banned words/phrases (jargon, informal language, emotional terms). Score = 100 - (banned_words_found * 15), clamped to 0–100.
   - **Structure** (Round 2 only): Check for presence of 3 section headers or their equivalents. Regex-based detection.

3. **Overall success criterion**:
   - Per-round score = average of axis scores (0–100)
   - Final grade: Analyst (< 60), Manager (60–74), Director (75–84), C-Suite (85+)
   - Radar chart visualization comparing Round 1 and Round 2 (showing growth)

4. **Scaffolding code outline**:
   - Setup cell with matplotlib radar chart function
   - Per-round: input display → prompt cell → run & score cell → radar chart display
   - Side-by-side comparison at the end

5. **Timing plan**: Minute-by-minute breakdown

## Diversity Directive

Focus on **multi-dimensional feedback and the visual radar chart**. The radar chart is the signature element — it shows students that prompt engineering involves trade-offs (making output shorter may sacrifice completeness; adding structure may hurt naturalness). This teaches a deeper lesson than a single score can. The business data should feel like something these managers encounter in real life. Use Swiss/European company names, EUR/CHF figures, realistic product names.

## Deliverable

Produce a detailed plan document (not code) that another agent could use to implement the full notebook. Include all input documents, all scoring formulas with exact keyword lists, the radar chart specification, and the grading thresholds.
