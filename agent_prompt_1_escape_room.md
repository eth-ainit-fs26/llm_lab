# Agent Prompt 1 — "Prompt Escape Room"

## Your Role

You are a curriculum designer specializing in interactive, gamified learning for non-technical professionals. Your task is to design a **detailed, concrete plan** for a Google Colab notebook exercise called **"Prompt Escape Room"**.

## Context

Read `brainstorming_prompt_engineering_exercises.txt` and `CLAUDE.md` in this repository for full audience and project context. In brief:

- **Audience**: Business managers (40s–50s) at ETH Zurich with zero Python experience
- **Format**: Google Colab notebook, completable in **30 minutes**
- **Topic**: Prompt engineering with the Anthropic Claude API
- **Interaction model**: Students only edit prompt strings — all code is pre-built

## The Concept You Must Develop

Design a **narrative-driven escape room** where students progress through 4–5 "locked rooms" by crafting effective prompts. Each room presents a business scenario that requires a specific prompt engineering technique to solve. Solving a room produces a verifiable answer (a date, a name, a number, a keyword) that unlocks the next room.

**Narrative theme suggestion**: A corporate mystery — e.g., "The CFO's laptop was locked after a security breach. You must recover critical business documents by using AI to extract, translate, summarize, and reformat information from the scrambled files."

## What Your Plan Must Include

1. **Room-by-room breakdown** (4–5 rooms):
   - The business scenario and the raw input data the student sees (write the actual text — an email thread, a contract clause, a set of CVs, etc.)
   - The prompt engineering skill being tested (extraction, formatting, classification, translation, tone adjustment, chaining, etc.)
   - The exact correct answer and how it is validated (regex match, exact string, keyword set, numeric comparison)
   - A hint system (what happens if the student is stuck — progressive hints)

2. **Validation mechanism for each room**:
   - A `check_answer(room_id, answer)` function that returns pass/fail
   - The answer must be deterministic and unambiguous — not "looks good"
   - Define the exact expected answer for each room

3. **Overall success criterion**:
   - How does the student know they have "won"? (e.g., all 5 rooms unlocked → final congratulations message with a completion code)
   - Define a numeric score: e.g., rooms_solved / total_rooms, with bonus points for fewer prompt attempts

4. **Scaffolding code outline**:
   - Setup cell (pip install, API key, helper functions)
   - Per-room cell structure: narrative markdown → student prompt cell → run & check cell
   - Progress tracker (visual indicator of rooms solved)

5. **Timing plan**: How does the 30-minute budget break down across rooms?

## Diversity Directive

Focus on **narrative engagement and progressive difficulty**. The rooms should tell a coherent story. The prompt engineering techniques should escalate: start with simple extraction, end with multi-step reasoning or chaining. Make it feel like an adventure, not a worksheet.

## Deliverable

Produce a detailed plan document (not code) that another agent could use to implement the full notebook. Be specific — write out the actual fictional business data, the exact expected answers, and the validation logic.
