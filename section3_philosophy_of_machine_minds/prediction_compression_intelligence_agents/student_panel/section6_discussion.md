# Section 6 student-panel discussion: AIXI

## Narrative synthesis (20 rounds, condensed)

The section defines AIXI as expectimax planning against a
Solomonoff-weighted universal mixture of environments, and declares the
resulting agent Pareto-optimal. The four student critics ganged up on
three recurring gaps: (1) Maria hammered the uncomputability issue and
refused to accept "north star" as a substitute for falsifiable claims;
(2) Aisha said the regional-manager analogy is cute but that the
intuition box blurs what "optimal" actually buys the reader; (3) Leo
walked out mentally at the expectimax sum — nested max/sum notation
with no tree picture killed him; (4) Yuki kept losing the thread between
"compression" and "action" because the two concepts fuse in one
paragraph without a worked bridge.

The three proposers responded with: a vivid auditor-with-infinite-manuals
story, a TikZ expectimax tree drawn explicitly to three plies, a
hand-computable two-hypothesis worked example, a Pareto-frontier 2D
picture, a Python micro-AIXI on a 4-state world, and a two-armed bandit
classroom game. Math writer defended keeping equation (eq:aixi-rule)
intact but agreed to annotate each symbol inline the first time it
appears and to add a concrete "plug in these numbers" companion.

## Critics' complaints

| Critic | Round | Complaint |
|---|---|---|
| Maria (CFO) | 1 | Pareto-optimality is nearly vacuous — being un-dominated everywhere is cheap. What is the decision-relevant claim? |
| Maria | 3 | "Uncomputable" is buried in one sentence. What does that mean operationally for a CFO evaluating AI vendors? |
| Maria | 5 | No numbers. Give me one decision where AIXI's prescription differs from a bounded heuristic. |
| Aisha (CEO) | 1 | The manager analogy promises plain English but then the intuition box uses "lower-semicomputable." Pick a lane. |
| Aisha | 3 | I cannot tell whether AIXI is a definition, a theorem, or a product claim. Put a one-line summary at the top. |
| Leo (bored) | 1 | Nested max-sum lost me by the second $\sum$. Draw the tree or lose me. |
| Leo | 5 | The "two-armed bandit" paragraph is told, not shown. Give me numbers I can follow. |
| Leo | 7 | There is no activity. I want to play, not read. |
| Yuki (distracted) | 3 | How does "compression" become "action"? The paragraph asserts the link; it does not build it. |
| Yuki | 7 | Every two paragraphs I need a concrete handle. The prose goes four paragraphs without one. |

## Proposers' solutions

| Proposer | Round | Contribution |
|---|---|---|
| Storyteller | 2 | AIXI as "the auditor who reads every audit manual in every language before approving one expense report" — reuses Aisha's plain-English demand. |
| Storyteller | 6 | Reframe Pareto-optimality: "no other agent beats AIXI across every world, but many agents beat it in the world we actually live in." |
| Math writer | 4 | Keep eq:aixi-rule; annotate each symbol with a footnote-style gloss on first appearance; add a companion equation showing the 2-step, 2-action unrolled form. |
| Math writer | 8 | Add an explicit 2-hypothesis worked computation as Example box — forces the expectimax to reduce to arithmetic. |
| Math writer | 10 | Add Pareto-frontier schematic to defend thm:aixi-opt visually for Maria. |
| Activity Brainstormer | 2 | Two-armed bandit classroom game (20 rounds, simple vs. complex advisor). |
| Activity Brainstormer | 6 | TikZ expectimax tree, 2 actions x 2 percepts, 2 plies, with xi-weights on leaves. |
| Activity Brainstormer | 8 | Python snippet: 4-state cycle vs. uniform world, 10-line agent. |
| Activity Brainstormer | 10 | Worksheet: hand-compute AIXI action on a 2-step, 2-hypothesis world. |

## Activities shortlist (Brainstormer's final pick)

1. **TikZ expectimax tree (built in).** Helps Leo — finally a picture of the
   nested sum. Helps Yuki — concrete handle right next to the equation.
2. **Two-armed bandit classroom game (activity box).** Helps Leo — play,
   don't read. Helps Yuki — ties "simple theory vs. complex theory" to
   an action the body physically takes.
3. **Hand-computation worksheet (Example environment).** Helps Maria —
   numbers. Helps Leo — arithmetic, not notation.
4. **Python micro-AIXI snippet (activity box).** Helps Yuki — concept
   becomes code in 15 lines. Helps Maria — falsifiable: run it.

Dropped for space: Pareto-frontier 2D plot (kept as short prose plus a
one-line tikzpicture), auditor story (folded into intuition box).

## Unresolved tensions

- **Maria vs. the section's thesis.** Maria's deepest objection —
  "uncomputability makes this a philosophical not an engineering claim"
  — is conceded rather than refuted. The revised section is explicit
  that AIXI is a *reduction* ("intelligence = Solomonoff prior +
  expectimax"), not a blueprint. A CFO who refuses the reduction will
  still refuse the section.
- **Pareto-optimality is weak.** Every competent reader will notice
  Pareto-optimality does not mean "best on average." The revised
  section now says this out loud instead of hiding it. Some instructors
  may want to replace thm:aixi-opt with a stronger self-optimisation
  statement; Math writer argued against that scope creep.
- **The Solomonoff prior's dependence on a universal Turing machine**
  is still not addressed. Flagged as future work; not in scope for one
  section.
