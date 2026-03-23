# Agent Prompt 5 — "The Email Rewriter Challenge"

## Your Role

You are a business communication trainer who designs hands-on AI literacy workshops. Your task is to design a **detailed, concrete plan** for a Google Colab notebook exercise where managers learn prompt engineering by rewriting bad business emails into professional ones — with automated A/B testing and scoring.

## Context

Read `brainstorming_prompt_engineering_exercises.txt` and `CLAUDE.md` in this repository for full audience and project context. In brief:

- **Audience**: Business managers (40s–50s) at ETH Zurich with zero Python experience
- **Format**: Google Colab notebook, completable in **30 minutes**
- **Topic**: Prompt engineering with the Anthropic Claude API
- **Interaction model**: Students only edit prompt strings — all code is pre-built

## The Concept You Must Develop

Design a **before/after rewriting challenge** structured as a "Communication Repair Shop." Students receive broken, poorly written, or inappropriate business emails and must craft prompts that instruct Claude to rewrite them into professional communications. Each rewrite is auto-scored on concrete criteria.

The twist that makes this different from the other exercises: **students must engineer TWO prompts per challenge — a "quick fix" prompt and a "deep rewrite" prompt — and the notebook compares them side by side**, showing which approach scored higher and why. This teaches that prompt specificity matters.

### Structure: 4 Challenges

**Challenge 1 — "The Angry Reply-All"** (~6 min):
- Input: A rude, emotional reply-all email from a department head complaining about budget cuts
- Task: Rewrite as a professional, constructive email to the CFO
- Quick fix prompt: student's first attempt (likely vague, like "make this professional")
- Deep rewrite prompt: student's refined attempt after seeing the score
- Scoring: tone score + required content elements

**Challenge 2 — "The Jargon Bomb"** (~7 min):
- Input: A technical product update email stuffed with acronyms and insider language
- Task: Rewrite for the board of directors (non-technical audience)
- Scoring: readability score + key information preserved

**Challenge 3 — "The Vague Request"** (~8 min):
- Input: A wishy-washy email asking for "some help with the project sometime soon"
- Task: Rewrite as a clear, actionable request with specific asks, deadlines, and owners
- Scoring: presence of concrete elements (date, name, specific action, metric)

**Challenge 4 — "The Cross-Cultural Minefield"** (~7 min):
- Input: An email from HQ in New York to the Zurich office, written in an overly casual American style with idioms that don't translate well
- Task: Rewrite for a Swiss/European professional audience
- Scoring: formality score + removal of idioms + preservation of core message

## What Your Plan Must Include

1. **For each challenge, write out**:
   - The complete "bad email" (realistic, 100–200 words each)
   - The scoring criteria with exact keyword/phrase lists
   - What a "good" rewrite looks like (reference output for instructor guide)
   - The comparison logic: how are "quick fix" vs "deep rewrite" scores displayed?

2. **Scoring rubric — fully deterministic for each challenge**:
   - **Tone score**: List of banned words/phrases (rude, informal, emotional) + list of required professional phrases. Score = (required_present / total_required) * 60 + (1 - banned_present / total_banned) * 40
   - **Content preservation**: List of key facts that must survive the rewrite. Score = facts_preserved / total_facts * 100
   - **Specificity score** (Challenge 3): Checklist of concrete elements (a date? a person's name? a number? an action verb?). Score = elements_found / 5 * 100
   - **Readability** (Challenge 2): Banned jargon list + required plain-English equivalents
   - **Combined score** per challenge: weighted average of applicable criteria

3. **The A/B comparison mechanism**:
   - Student writes Prompt A (quick fix), runs it, sees score
   - Then writes Prompt B (deep rewrite), runs it, sees score
   - Side-by-side display: Prompt A output | Prompt B output, with score bars
   - Delta shown: "Your refined prompt improved by +23 points!"
   - This is the core pedagogic moment: shows that prompt specificity matters

4. **Overall success criterion**:
   - Total score = sum of best scores across 4 challenges (max 400)
   - Average improvement from quick fix → deep rewrite (measures learning)
   - Grade: Intern (< 200), Associate (200–279), VP (280–349), Partner (350+)
   - Final report card showing per-challenge best score + improvement delta

5. **Scaffolding code outline**:
   - Per-challenge: bad email display → Prompt A cell → score A → Prompt B cell → score B → comparison display
   - Cumulative scoreboard updating after each challenge
   - Final summary cell

6. **Timing plan**: How the 30 minutes are divided

## Diversity Directive

Focus on **the power of before/after comparison and the A/B testing mechanic**. This exercise is the most directly relevant to managers' daily work — everyone writes emails. The A/B comparison is what makes this unique: it physically demonstrates that a vague prompt ("make it better") underperforms a specific one ("rewrite in a formal tone, preserve the 3 budget figures, address the CFO by name, and propose a meeting date"). The improvement delta is the key metric that proves the student learned something.

## Deliverable

Produce a detailed plan document (not code) that another agent could use to implement the full notebook. Include all bad emails, all scoring criteria with exact word lists, the A/B comparison display logic, and the grading system.
