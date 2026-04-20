# Top 3 Bellman-Intuition Classroom Games

Ranked output of the 20-round committee (see `bellman_committee_log.md`).

Each game follows the same template: story, rules, state/action/reward, greedy-trap, past-matters, debrief script, materials, time budget, and a one-line rank justification.

---

## #1 — Restaurant Row (Reactive Chef)

### Story / setup
The student walks down a row of 8 restaurants on the way home. Each restaurant's rating is revealed only as the student arrives at it. The student may eat at most 4 of them. But there is a twist: chefs are nervous — each time the student eats, the next restaurant's rating is lowered by 2 (minimum 1). If the student skips, the next chef is unaffected. The goal is to maximize the sum of ratings of the restaurants where the student ate.

### Complete rules
1. The class (each student individually) will see 8 ratings revealed one at a time on the whiteboard (values 1-10).
2. At each reveal, every student marks **EAT** or **SKIP** on a paper strip before the next reveal.
3. You may EAT at most 4 times total across the 8 restaurants.
4. After each **EAT**, the instructor announces the *next* rating with -2 applied (minimum 1). After each **SKIP**, the next rating appears unmodified.
5. Your score = sum of ratings at the restaurants where you chose EAT.
6. 25 seconds per decision; ~4 minutes of play.

### State / action / reward
- **State.** $s = (t, \text{eats\_left}, r_t)$ where $t$ is the current position (1..8), eats_left is the number of EAT choices remaining, and $r_t$ is the rating *as it appears to you at $t$*.
- **Action.** $a \in \{\text{EAT}, \text{SKIP}\}$ (EAT requires eats_left > 0).
- **Transition.** If EAT: $t \to t+1$, eats_left -= 1, $r_{t+1} \leftarrow \max(1, r_{t+1}^{raw} - 2)$. If SKIP: $t \to t+1$, eats_left unchanged, $r_{t+1} \leftarrow r_{t+1}^{raw}$.
- **Reward.** $r_t$ if EAT, 0 if SKIP.

### Greedy trap (why short-sighted play fails)
Greedy eats at the first decent rating (say a 7 early in the row), which (a) burns one of only four eat-slots on a mediocre meal and (b) lowers the next rating by 2, compounding the loss. With a sequence like [5, 7, 6, 4, 9, 3, 8, 10], greedy scores ~16 (eats 5, 5, 4, 2 after chef effect); optimal scores ~34 (eats 7, 9, 8, 10). The gap is *caused* by the short-horizon choice, not by luck.

### Past matters
The state variables `eats_left` and `r_t` are both functions of the history of choices. Two students who arrive at position 5 with different histories face genuinely different decisions: one may see a 9 with 3 eats remaining; the other sees a 7 with 1 eat remaining. You cannot play well by looking only at the current rating; you must integrate what you've already done.

### Debrief script (from play to the Bellman equation)
1. Put every student's final score on a sticky-note histogram. Note the bimodality: a greedy cluster around 16-22, a far-sighted cluster around 30-34.
2. Ask two high-scorers and two low-scorers to describe their strategy. The low-scorers will say something like "I ate whenever the rating looked good." The high-scorers will say "I saved slots for later."
3. Write on the board: **value of EAT at position $t$ = rating now $+$ effect on what I can still get**.
4. Define $V(s)$ as the best score still achievable from state $s$. Walk through the recursion:
   $$V(t, \text{eats\_left}, r_t) = \max\begin{cases} r_t + V(t+1, \text{eats\_left}-1, \max(1,r_{t+1}^{raw}-2)) & \text{EAT} \\ 0 + V(t+1, \text{eats\_left}, r_{t+1}^{raw}) & \text{SKIP} \end{cases}$$
5. Generalize by stripping the restaurant-specific labels: the action changed the state, the state determines future reward, and the best action maximizes *immediate + future*.
6. Write the Bellman equation: $V(s) = \max_a [\,r(s,a) + \gamma V(s')\,]$. Name it. Tell the class this is the recursive structure they just played.
7. Run play 2 with a new rating sequence. Watch the histogram shift toward the high cluster. Say: "That shift is what it looks like when a population of agents learns $V(s)$."

### Materials
- One slide with the six rules.
- Whiteboard to write the revealed-rating sequence.
- Paper strip per student with 8 boxes (columns: raw_rating, seen_rating, EAT/SKIP, eats_left_after, running_score).
- Sticky notes for the histogram.

### Time budget
15 minutes total: 1 min rules, 4 min play 1, 1 min histogram, 3 min debrief, 4 min play 2, 1 min second histogram, 1 min closing.

### Rank justification
#1 because it produced the single cleanest behavior change between play 1 and play 2 in committee playtesting, and students named their own mistake in exactly the language of the Bellman equation ("I ate too early" = "I underestimated $V(s')$").

---

## #2 — The Patient Gardener

### Story / setup
The student manages two plots in a garden across 6 turns. Each turn they take one action: **PLANT** a seed (cost 2, the plot becomes a seedling), **WATER** a plot (cost 1, advances stage), or **HARVEST** (free, gain value based on stage, plot resets to empty). Stages progress empty → seedling → flower → ripe and auto-harvest at ripe on the next turn. Seedlings score 0, flowers score 3, ripe scores 8. The student has a budget of 8 coins to spend on actions. Goal: maximize total harvested value.

### Complete rules
1. Two plots, 6 turns, budget 8.
2. Each turn choose ONE action: PLANT plot (cost 2, empty → seedling); WATER plot (cost 1, seedling → flower or flower → ripe); HARVEST plot (free, score depends on stage, resets plot).
3. If a plot reaches ripe and is not harvested next turn, it auto-harvests for full value 8 (no penalty in this simplified version — rule-minimal).
4. Running out of budget ends the game; remaining plots auto-harvest at current stage value.
5. Score = total value harvested.

### State / action / reward
- **State.** $s = (t, \text{budget}, \text{plot1\_stage}, \text{plot2\_stage})$.
- **Action.** $a \in \{\text{PLANT}_1, \text{PLANT}_2, \text{WATER}_1, \text{WATER}_2, \text{HARVEST}_1, \text{HARVEST}_2\}$, subject to legality.
- **Reward.** HARVEST yields 0/3/8 for seedling/flower/ripe; PLANT and WATER yield 0 immediately.
- **Transition.** Deterministic stage progression.

### Greedy trap
A greedy student harvests at flower stage (score 3) every time, because waiting feels risky. Over 6 turns with budget 8, a flower-harvest strategy nets ~9 points. An investment strategy — PLANT, WATER, WATER, HARVEST (ripe, +8) on one plot while parallelizing with the other — nets 16+. The greedy failure is *attributing value to immediate harvest only*, which is exactly the Bellman failure mode.

### Past matters
Each plot's current stage encodes the full history of prior actions on that plot. To decide whether to water plot 1 or plant plot 2, the student must consult the stage records (visible on their sheet). Two students at turn 4 with the same budget but different stage histories face different optimal moves.

### Debrief script
1. Histogram of scores. Contrast flower-harvesters (low) with ripe-harvesters (high).
2. Ask: "Why did planting score you points when the plant action itself paid 0?"
3. Student answer: "Because it sets up the harvest later."
4. Write: "value(PLANT) = 0 + value(next state with a seedling)."
5. Chain: "value(WATER seedling) = 0 + value(next state with flower)."
6. Collapse: "the value of any action is its immediate reward plus the value of the state it takes you to."
7. Formalize: $V(s) = \max_a [r(s,a) + \gamma V(s')]$.
8. Name it. Play 2 with a different budget or turn count.

### Materials
- One slide with rules.
- Per-student sheet with 6 rows (turns) × 5 columns (action, plot1_stage, plot2_stage, budget, score).
- Sticky-note histogram.

### Time budget
15 minutes: 1 min rules, 5 min play 1, 1 min histogram, 3.5 min debrief, 4 min play 2, 0.5 min close.

### Rank justification
#2 because the investment metaphor is universally intuitive (especially for mixed audiences with non-CS students), and the PLANT → WATER → HARVEST chain is a visible, physical instance of the Bellman backup. Slightly more complex state-tracking than Row puts it in second place.

---

## #3 — The Hiker's Dilemma

### Story / setup
The student hikes a 10-checkpoint trail. At each checkpoint, a reward (1-10) is revealed on arrival. The student may **MARCH** (spend 1 energy, collect the reward, advance) or **REST** (gain +2 energy, skip the reward, advance). Start energy = 3. If energy reaches 0 mid-trail, the student is stuck and collects nothing more. The game ends after checkpoint 10. Maximize total reward collected.

### Complete rules
1. 10 checkpoints, start energy 3.
2. Each checkpoint: reward revealed, choose MARCH or REST.
3. MARCH: collect the reward, energy -= 1, advance.
4. REST: skip the reward, energy += 2, advance.
5. If energy = 0, remaining checkpoints are inaccessible.
6. Score = sum of collected rewards.

### State / action / reward
- **State.** $s = (t, \text{energy}, r_t)$.
- **Action.** $a \in \{\text{MARCH}, \text{REST}\}$ (MARCH requires energy > 0).
- **Reward.** $r_t$ if MARCH, 0 if REST.
- **Transition.** MARCH: t += 1, energy -= 1. REST: t += 1, energy += 2.

### Greedy trap
Greedy MARCHes on every reveal, exhausts energy by checkpoint 3 or 4, misses the bigger rewards later. With a sequence like [3, 8, 2, 9, 1, 10, 4, 7, 6, 5], greedy scores ~13 (marches until stuck). Optimal rests at low-reward checkpoints, preserving energy for the 9, 10, 7, etc., scoring ~40+.

### Past matters
Energy is the integral of all prior MARCH/REST decisions. The student's current energy is *nothing but history summarized into one number*. Two students at checkpoint 5 with different histories face genuinely different decisions.

### Debrief script
1. Histogram. Many scores clustered low (stuck early) and a tail of higher scores.
2. Ask: "Why is resting valuable when it gives you zero reward right now?"
3. Student answer: "Because +2 energy lets me collect more later."
4. Write: "value(REST) = 0 + (best reward I can still collect with +2 energy)."
5. Formalize $V(s)$ and write the Bellman equation.
6. Caveat: emphasize to the class that "resting for future rewards" is the same principle as "skipping a mediocre restaurant" or "planting a seed" — the specific game is a vehicle.
7. Play 2.

### Materials
- One slide.
- Per-student strip with 10 boxes × 4 columns (reward, MARCH/REST, energy_after, running_score).
- Sticky-note histogram.

### Time budget
15 minutes: 1 min rules, 4 min play 1, 1 min histogram, 3 min debrief, 4 min play 2, 2 min close (with the reframing caveat).

### Rank justification
#3 because the lesson is pedagogically real but students consistently frame their loss as "resource mismanagement" rather than "short-horizon value estimation." The debrief must *re-frame* their experience to land the Bellman insight, a small but real cost versus Row and Gardener, where students frame the lesson correctly on their own.
