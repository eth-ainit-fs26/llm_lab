# git_llm_lab

## Project Purpose

This repository contains a **prompt engineering lab exercise** for a continuing education programme at **ETH Zurich**. The target audience is **managers in their 40s–50s** who are taking a course on AI/LLMs and have **essentially no Python programming experience**.

## Audience Profile

- Business managers and executives (CAS/DAS programme at ETH Zurich)
- Age range: 40s–50s
- Technical level: beginners — they can run a Jupyter cell but should not be expected to write or debug Python
- Motivation: understand how to use LLMs effectively in their professional context

## Exercise Constraints

- **Duration**: ~30 minutes
- **Format**: Google Colab notebook (.ipynb, opened in-browser — no local install)
- **Interaction model**: Students only edit **prompt strings** in designated cells; all Python/API code is pre-built and hidden behind helper functions
- **LLM provider**: Anthropic Claude API (using the `anthropic` Python SDK)
- **Gamification**: Every exercise must have automated scoring, clear feedback, and ideally a competitive/progressive element (scores, levels, leaderboards)

## Key Design Principles

1. **Zero Python required** — Students interact only by typing natural language prompts into clearly marked cells
2. **Immediate feedback** — Running a cell produces a score, a pass/fail, or a visual result instantly
3. **Business-relevant scenarios** — All tasks should feel directly useful to managers (emails, summaries, reports, customer feedback, contracts)
4. **Progressive difficulty** — Start easy, build confidence, then introduce subtlety
5. **Self-contained** — The notebook should have no external dependencies beyond the API key; all data is embedded in the notebook

## Repository Structure

```
git_llm_lab/
├── CLAUDE.md                                    # This file — project context for AI agents
├── README.md                                    # Student-facing instructions
├── brainstorming_prompt_engineering_exercises.txt # Landscape scan + 7 original ideas
├── agent_prompt_1_escape_room.md                # Agent brief: Prompt Escape Room exercise
├── agent_prompt_2_sentiment_arena.md            # Agent brief: Sentiment classification exercise
├── agent_prompt_3_prompt_golf.md                # Agent brief: Target-matching golf exercise
├── agent_prompt_4_ceo_briefing.md               # Agent brief: Multi-axis CEO briefing exercise
├── agent_prompt_5_email_rewriter.md             # Agent brief: A/B email rewriting exercise
├── exercise.ipynb                               # The main exercise notebook (to be created)
└── solutions.ipynb                              # Instructor solutions (to be created)
```

## Agent Prompts

Five agent prompt files (`agent_prompt_*.md`) each describe a different exercise concept in detail. Each is designed so that an independent agent can read it + `brainstorming_prompt_engineering_exercises.txt` and produce a complete, detailed plan for a Google Colab notebook. The 5 exercises are:

1. **Prompt Escape Room** — Narrative-driven, 4–5 locked rooms with business scenarios
2. **Sentiment Arena** — 3-round customer review classification with accuracy scoring
3. **Prompt Golf** — 4-hole target-matching game with transparent scoring breakdown
4. **CEO Briefing Challenge** — Multi-axis radar chart scoring on executive summaries
5. **Email Rewriter** — A/B prompt comparison on business email rewrites

All exercises share the same hard requirements: Google Colab notebook, 30 minutes, zero Python for students, fully automated deterministic validation.

## Brainstorming Summary

The file `brainstorming_prompt_engineering_exercises.txt` contains:
- A landscape scan of 10 existing prompt engineering exercises/resources from the internet
- 7 original exercise ideas designed for this audience
- A ranked shortlist of the top 3 recommended approaches
- Critical requirements around validation and assessment

## Technical Notes for Implementing Agents

- Use `anthropic` Python SDK for all LLM calls
- Wrap API calls in helper functions (e.g., `call_llm(prompt)`, `score(response, target)`)
- Use `IPython.display` for rich output (Markdown, HTML) in the notebook
- Consider `ipywidgets` for interactive elements (text areas, buttons, progress bars) if appropriate
- Scoring functions should be deterministic where possible (keyword matching, exact match, regex) rather than relying on another LLM call for evaluation
- All fictional business data should be realistic but clearly fictional
- Include a setup cell at the top that: installs `anthropic`, validates the API key, and defines all helper functions
- Include a "Prompt Engineering Cheat Sheet" appendix at the end of the notebook

## Style & Tone

- Professional but approachable — these are experienced professionals, not students
- No condescension; assume intelligence but not technical knowledge
- Swiss-international context: use examples that are culturally neutral or European-flavoured
- English language (the programme is taught in English)
