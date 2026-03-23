# Agent Prompt 2 — "The Sentiment Arena"

## Your Role

You are an expert in NLP education and gamified learning. Your task is to design a **detailed, concrete plan** for a Google Colab notebook exercise where managers learn prompt engineering through **customer review classification**.

## Context

Read `brainstorming_prompt_engineering_exercises.txt` and `CLAUDE.md` in this repository for full audience and project context. In brief:

- **Audience**: Business managers (40s–50s) at ETH Zurich with zero Python experience
- **Format**: Google Colab notebook, completable in **30 minutes**
- **Topic**: Prompt engineering with the Anthropic Claude API
- **Interaction model**: Students only edit prompt strings — all code is pre-built

## The Concept You Must Develop

Design a **competitive classification challenge** structured in 3 progressive rounds. Students write a single prompt template that instructs Claude to classify customer reviews into sentiment categories. The notebook runs their prompt against a set of reviews and scores accuracy.

### Round Structure

- **Round 1 — "Easy Street"** (~8 min): 8 clearly positive/negative reviews. Target: 8/8.
- **Round 2 — "The Grey Zone"** (~10 min): 10 reviews including sarcasm, mixed sentiment, backhanded compliments, neutral/ambiguous. Target: ≥ 8/10.
- **Round 3 — "Global Voices"** (~10 min): 8 reviews mixing English, German, and French. Some with cultural nuance. Target: ≥ 6/8.

A final "Championship Score" combines all three rounds.

## What Your Plan Must Include

1. **The complete review dataset** for all 3 rounds:
   - Write out every single review (realistic, European/Swiss-flavored business contexts: hotels, banks, consulting firms, airlines, SaaS products)
   - Assign ground-truth labels: positive / negative / neutral (and for Round 2, possibly mixed)
   - Explain WHY each tricky review is tricky (for the instructor guide)

2. **Validation mechanism**:
   - The prompt template must contain a `{review}` placeholder
   - The notebook substitutes each review, calls Claude, and extracts the label from the response
   - Scoring: exact match of extracted label vs ground-truth
   - Define how the label is extracted from Claude's response (e.g., first word must be "POSITIVE", "NEGATIVE", or "NEUTRAL")
   - Show per-review results: ✅ or ❌ with the review text and expected vs actual label

3. **Overall success criterion**:
   - Final score = total correct across all 3 rounds (out of 26)
   - Clear thresholds: Bronze (≥ 18), Silver (≥ 22), Gold (≥ 25), Perfect (26)
   - A congratulations cell with their medal and score breakdown per round

4. **Scaffolding code outline**:
   - Setup cell structure
   - Per-round structure: intro markdown → prompt editing cell → run & score cell → results display
   - A "strategy tips" sidebar between rounds (teaching zero-shot vs few-shot, output formatting, etc.)

5. **Timing plan**: Minute-by-minute breakdown of the 30-minute session

## Diversity Directive

Focus on **data quality and scoring clarity**. The reviews are the heart of this exercise — make them realistic, diverse, and progressively tricky. The scoring must be bulletproof: the student should never wonder "did I get this right or not?" Every review must have ONE correct answer. Avoid ambiguity in the ground-truth labels.

## Deliverable

Produce a detailed plan document (not code) that another agent could use to implement the full notebook. Write out all reviews, all labels, all scoring logic, and the exact prompt template structure the student interacts with.
