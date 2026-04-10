================================================================================
  AGENT PROMPTS — AGENTIC AI: MATHEMATICAL FRONTIER
  Generated: April 2026
================================================================================

This directory contains six agent prompt files, each targeting a different
mathematically rigorous frontier of agentic AI.  The agents are designed to
produce lecture-ready LaTeX documents (article class, amsmath/amsthm/amssymb)
suitable for a Master's level Machine Learning course at ETH Zurich.

FILES:
  01_universal_intelligence.txt        — AIXI, Kolmogorov complexity, Gödel Machines
  02_embedded_agency.txt               — Logical induction, FDT, Löb's theorem, Cartesian frames
  03_active_inference.txt              — Free energy principle, Markov blankets, Bayesian mechanics
  04_multiagent_game_theory.txt        — CFR, Nash equilibria, mean-field games, Cicero
  05_world_models_mesa_optimization.txt — Dreamer, MuZero, inner alignment, deceptive alignment
  06_foundations_rl_planning.txt       — Reward hypothesis, distributional RL, successor features

USAGE:
  Spawn one agent per file.  Each agent should produce a complete, compilable
  LaTeX document with:
    - Formal definitions, theorems, and proof sketches (theorem environments)
    - Full equation derivations (align environments)
    - Named researchers and precise citations (author, year, venue or arXiv ID)
    - Connections to modern LLM-based agentic AI systems
    - Open problems and an annotated bibliography

  The six agents can run in parallel — their topics are independent but
  cross-reference each other.  Suggested output directory:

      agentic_ai_frontier/
        01_universal_intelligence.tex
        02_embedded_agency.tex
        03_active_inference.tex
        04_multiagent_game_theory.tex
        05_world_models_mesa_optimization.tex
        06_foundations_rl_planning.tex

  Recommended timeout: ≥ 30 minutes per agent (the documents are substantial).

  Example (Claude Code CLI):
    claude -p "$(cat 01_universal_intelligence.txt)" --output ../../../agentic_ai_frontier/01_universal_intelligence.tex

================================================================================
