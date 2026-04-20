# Top 3 Bellman-Intuition Classroom Games (v2 — Learnability Fix)

Ranked output of the v2 committee (see `bellman_committee_log_v2.md`).

## Why v2

v1's winners (Restaurant Row, Patient Gardener, Hiker's Dilemma) exercised
only the outer max of the Bellman equation. Their rewards came from
pre-generated sequences with no exploitable stationary pattern, so students
could not *learn the environment* across plays — they could only learn
"don't be greedy." That is reservation-sampling, not Bellman.

v2 requires a **hidden but stationary regularity** that past observations
reveal, so that optimal play requires BOTH halves of

$$V(s) = \max_a \Bigl[\,r(s,a) + \gamma\, \mathbb{E}_{s' \sim p(\cdot\mid s,a)}\,V(s')\,\Bigr]:$$

- estimate $\mathbb{E}[r(s,a)]$ and/or $p(s'\mid s,a)$ from played history, and
- maximize cumulative expected future reward given those estimates.

A student who plays greedy fails because they don't discount against the
future. A student who blind-reservation-samples (wait for a big number)
fails because the optimal threshold depends on the *learned* reward
distribution. Both failure modes are independently observable on the
classroom scoreboard, and the correct strategy is "learn the regularity
from play 1, then plan with it in play 2."

---

## #1 — Colored Restaurant Row (v3b)

### Story / setup

A student walks past 8 restaurants. Each restaurant displays a visible
**color tag** (white, gray, or black) **before the student commits to eat
or skip**. The *rating itself* is revealed only after EAT/SKIP. The tag
color predicts the rating's distribution — but the students are never told
that explicitly. They discover it by playing.

### Complete rules (60-second brief)

1. 8 restaurants in a row. At each one:
   - The instructor announces the **color** first (W, G, or B).
   - The student writes EAT or SKIP on their strip.
   - The instructor announces the **rating** (integer 1–10).
   - If EAT: student adds the rating to their running score and crosses
     off a slot.
2. Students have **3 EAT slots** for the full row.
3. Score = sum of ratings at restaurants where EAT was chosen.
4. Play twice with different (color, rating) sequences drawn from the same
   underlying distributions.

### State / action / reward

- **State.** $s = (t,\ \text{slots\_left},\ \text{color}_t)$ where color is
  the color announced for the *current* restaurant (already visible).
- **Action.** $a \in \{\text{EAT},\text{SKIP}\}$ (EAT requires slots_left > 0).
- **Reward.** The rating $r_t$ if EAT, 0 if SKIP. The rating is drawn from
  the color-specific distribution $p(r_t \mid \text{color}_t)$.
- **Transition.** Deterministic for $t$ and slots_left; the *next*
  restaurant's color is revealed after the action.

### The explicit hidden regularity

Three stationary reward distributions, one per color:

| Color | Distribution             | Mean | Notes |
|-------|--------------------------|------|-------|
| W (white) | Uniform on {1, 2, 3, 4} | 2.5 | cheap diner |
| G (gray)  | Uniform on {3, 4, 5, 6, 7} | 5.0 | middling |
| B (black) | Uniform on {6, 7, 8, 9, 10} | 8.0 | high-end |

These tables are **fixed for the whole classroom session** and identical
across play 1 and play 2. Students must discover the ranking
$\mathbb{E}[r\mid B] > \mathbb{E}[r\mid G] > \mathbb{E}[r\mid W]$.

### How students discover the regularity across plays

The student's strip has a **per-color tally panel** on the side with
columns for (count, running sum, running mean) for W, G, B. Every EAT
observation updates the tally for that color. SKIP observations still see
the rating revealed, so they also update the tally (which is important —
the tally is a passive inference tool, not an action-contingent one).

- **Play 1 (~8 observations total, 2–3 per color):** most students form a
  rough ranking B > G > W, but overlap between G and B can be misread if
  the student happens to draw a weak B sample. Histogram of play-1 scores
  is wide.
- **Between plays:** instructor asks students to announce their running
  color means. The class collectively pools ~150-200 observations per
  color. The ranking becomes unambiguous.
- **Play 2:** Students with a locked-in model skip every W on sight, save
  slots for B, and spend G slots only if blacks look scarce ahead.
  Histogram sharpens and mean score rises visibly.

### Greedy-trap

A greedy student eats the first rating ≥ 6 regardless of color. On a
sequence like colors [W, B, G, W, B, W, G, B] and ratings [3, 7, 5, 4, 6,
2, 7, 9] (example), greedy eats at position 2 (7), position 5 (6), position
7 (7) — slots full, score = 20. Black at position 8 (9) is unreachable.
Optimal skips the gray, saves slots for blacks, scoring 7 + 6 (if black) +
9 = ~22 — but more importantly, in play 2 with different draws, the color-
aware policy wins reliably while greedy's score is variance-driven.

### Blind-reservation trap

A student who uses "wait for any 9 or 10" ignores the color. In
sequences where blacks run 6-7-8 mostly, blind reservation sees no 9 until
very late and forfeits slots. Blind reservation also eats low ratings in
panic at the end of the row. Scores hover around 12–16. The optimal
threshold is color-conditional (eat any black, eat gray only if 7+, never
eat white), which the blind-reservation student cannot derive without
learning the color map.

### Debrief script (play-to-Bellman)

1. Put play-1 scores on a sticky-note histogram. Note wide spread and
   modest mean.
2. Ask: "What did you write in your color tally? What did you notice?"
   Elicit: "white was usually low, black was usually high."
3. Ask: "In play 2, did you change what you did? Why?" Elicit: "I skipped
   whites on sight. I saved slots for blacks."
4. Name what happened: "You **learned** an expected reward conditional on
   a state feature. You estimated $\mathbb{E}[r \mid \text{color}]$ from
   about 8 observations in play 1, refined it with the pooled class data
   between plays, then used those estimates to pick actions."
5. Put play-2 histogram next to play-1's. The distribution sharpens and
   shifts right. **"This is what it looks like when a population of agents
   learns a reward model and uses it in policy."**
6. Write on the board: $V(s) = \max_a [\,\mathbb{E}[r(s,a)] + \gamma\,V(s')\,]$.
   Note that the max requires you to have an estimate of $\mathbb{E}[r(s,a)]$
   for each action — which is exactly what the tally produced.
7. Greedy-no-tally = no reward model = fails. Blind-reservation = wrong
   threshold = fails. Color-aware Bellman = right threshold given right
   model = wins.
8. Generalize: state features (colors here) stand in for any signal the
   agent uses to predict reward — features in a neural network, the
   previous few words in a language model, visual features in a robot.

### Materials

- One slide with rules (60s read).
- Whiteboard to announce (color, rating) pairs.
- Per-student strip: 8 rows × 5 columns [color, rating, EAT/SKIP,
  slots_left, running_score], plus a 3-row color tally panel [count,
  sum_rating, mean] for W / G / B.
- Instructor's hidden (color, rating) list, pre-generated from the three
  distributions.
- Sticky notes for the scoreboard histogram.

### Time budget

15 minutes total:

| Segment | Time |
|---|---|
| Rules | 1:00 |
| Play 1 (8 reveals × ~22s) | 3:00 |
| Histogram + pool color means | 1:30 |
| Debrief (derive Bellman, expected-reward framing) | 3:30 |
| Play 2 | 3:00 |
| Play-2 histogram vs play-1 | 1:00 |
| Close (generalize to agents/LLMs/RL) | 2:00 |

### Rank justification (#1)

Colored Row is the **cleanest** of the three at exhibiting all three
pedagogical targets simultaneously: cumulative-future-reward reasoning (3
slots across 8 restaurants), past-matters (running color means are the
whole policy), and **learnability** (visible per-color tally is a physical
representation of the learned reward model). Greedy and blind reservation
both visibly fail. The debrief's mapping from "per-color tally" to
"$\mathbb{E}[r(s,a)]$ inside the Bellman equation" is the most direct link
in the committee's design space. Students can finish the game and explain
the equation in their own words within 60 seconds.

---

## #2 — Mood Market (v3)

### Story / setup

A student watches a market's 16-step trading day. At each step, a price
rating (1–10) is revealed. The student picks BUY or SKIP. 6 BUYs allowed
across the 16 steps. Goal: maximize sum of ratings of purchased positions.
The hidden regularity is that the market has an unobserved **mood** (bull
vs bear) that persists across steps.

### Complete rules (60-second brief)

1. 16 trading steps. At each step:
   - Instructor reveals a rating (1–10).
   - Student writes BUY or SKIP.
2. 6 BUYs available in total.
3. Score = sum of ratings on BUY steps.
4. Play twice with fresh sequences drawn from the same hidden process.

### State / action / reward

- **State.** $s = (t,\ \text{buys\_left},\ r_{t-1})$ — position, resources,
  and the most recent observed rating (which is a noisy signal of the
  hidden mood).
- **Action.** $a \in \{\text{BUY},\text{SKIP}\}$.
- **Reward.** $r_t$ if BUY, 0 if SKIP.
- **Transition.** The hidden mood $m_t \in \{\text{bull, bear}\}$ transitions
  as a Markov chain with $p(m_{t+1} = m_t) = 0.8$ (persistent).
  The rating $r_t$ is drawn from $\text{Unif}\{7,8,9,10\}$ if $m_t$ is bull,
  $\text{Unif}\{1,2,3,4\}$ if bear.

### The explicit hidden regularity

A two-state hidden Markov reward chain:
- Transition: $P(\text{bull}\to\text{bull}) = 0.8$, $P(\text{bear}\to\text{bear}) = 0.8$.
- Emission: bull ratings ~ U{7–10}, bear ratings ~ U{1–4}.

Both the transition matrix and the emission distributions are stationary
across plays.

### How students discover the regularity across plays

The strip has a **last_rating** column that students fill in. Within one
play, the running sequence of ratings makes regime persistence visible:
once you've seen three 8s or higher in a row, the next step is almost
certainly also bull. Between plays, students confirm that "high follows
high and low follows low" is a durable feature of the market.

- **Play 1 (16 observations):** students feel the runs — ratings cluster
  into high-sequences and low-sequences. After a single play, most have
  internalized "when last was high, next is probably high."
- **Play 2:** students explicitly wait for a high rating to "call" the
  bull regime, buy aggressively while in it, and stop buying the moment
  they see a bear signal.

### Greedy-trap

Buy anything ≥ 5. Early bull runs look attractive, so greedy burns all
6 buys in the first bull stretch, then misses a later, longer bull stretch
because out of buys. Also buys the first 4 that kicks off a bear regime,
wasting a slot.

### Blind-reservation trap

Wait for a 10. In a play where the bull regime never happens to emit a 10
(e.g., bull regime emits 7, 8, 9 only), blind reservation never buys and
scores zero. Blind reservation is also forced to dump its buys on random
mid-range values in the last 2 steps. The optimal threshold depends on
the bull-regime mean (mean 8.5), which blind reservation doesn't use.

### Debrief script (play-to-Bellman)

1. Histogram.
2. "What did you notice about how ratings related to each other?"
   Elicit: "they came in runs. High tended to follow high."
3. "Did you use that in play 2?" Elicit: "Once I saw a high rating, I
   committed to buying for a while. When I saw a low, I waited."
4. Name it: "You estimated a **transition model**: given the previous
   rating, what is the distribution of the next? You inferred the market
   has a persistent hidden mood."
5. Write: $V(s) = \max_a [\, r(s,a) + \gamma\, \mathbb{E}_{s' \sim p(\cdot
   \mid s,a)}[V(s')]\,]$. Point at the expectation: the probability
   distribution $p(s' \mid s, a)$ is what you learned.
6. Play-2 histogram sharpens and shifts. Same message as Colored Row:
   "this is learning and planning, together."
7. Generalize: the hidden mood is a *latent state*. Many real systems —
   weather, consumer sentiment, pandemic spread — have latent states that
   persist. Agents must infer them from observations.

### Materials

- One slide with rules.
- Per-student strip: 16 rows × 6 columns [step, rating, BUY/SKIP,
  buys_left, running_score, last_rating].
- Instructor's hidden sequence: a 16-step (mood, rating) list pre-generated
  from the Markov model. (In practice: flip a coin biased 0.8 toward
  staying in the current mood each step, then draw from the appropriate
  uniform.)
- Sticky notes for histograms.

### Time budget

| Segment | Time |
|---|---|
| Rules | 1:00 |
| Play 1 (16 steps × 15s) | 4:00 |
| Histogram | 0:30 |
| Debrief (derive Bellman, transition-model framing) | 3:30 |
| Play 2 | 4:00 |
| Histogram compare + close | 2:00 |

### Rank justification (#2)

Mood Market teaches the **transition-model** side of Bellman with rare
clarity: students feel the persistence of hidden state and transfer that
feeling into both within-play and across-play learning. It ranks #2, not
#1, because: (a) the debrief must introduce the concept of an expectation
over next states, which is a small step up in mathematical load compared
to Colored Row's expected reward; (b) some students never see enough
regime transitions in a 16-step play to feel the Markov structure (if the
random seed keeps them in one mood for the whole play). For mixed or
finance-oriented audiences, however, Mood Market can edge out Colored Row
on relevance.

---

## #3 — Mystery Gardener

### Story / setup

Two plots in a garden — one **red**, one **blue**. Student manages both
across 6 turns with a budget of 8 coins. At each turn, the student takes
one action: PLANT a seed in an empty plot (cost 2), WATER a plot (cost 1,
stochastically advances stage), or HARVEST a plot (free, scores based on
stage, resets plot to empty). Stages: empty → seedling → flower → ripe.
Harvest value: 0 / 3 / 8 (seedling / flower / ripe). Hidden: watering
succeeds with plot-specific probability.

### Complete rules (60-second brief)

1. 2 plots (red and blue), 6 turns, budget 8.
2. Each turn, one action: PLANT (cost 2, plot empty → seedling), WATER
   (cost 1, if it succeeds plot advances one stage, if it fails plot
   stays), HARVEST (free, gain 0/3/8 for seedling/flower/ripe, plot → empty).
3. Watering succeeds with probability that depends on **which plot you're
   watering** — unknown to students.
4. Unharvested ripe plots auto-harvest for full value at end.
5. Score = total harvest value.
6. Play twice (or 3 times if time) with the plot probabilities unchanged.

### State / action / reward

- **State.** $s = (t,\ \text{budget},\ \text{R\_stage},\ \text{B\_stage})$.
- **Action.** $a \in$ {Plant_R, Plant_B, Water_R, Water_B, Harvest_R,
  Harvest_B} subject to legality.
- **Reward.** 0 for Plant/Water, 0/3/8 for Harvest depending on stage.
- **Transition.** Plant and Harvest deterministic. Water on red:
  advances with p_red; on blue: advances with p_blue (independent Bernoulli
  each water attempt).

### The explicit hidden regularity

Per-plot watering success probabilities, stationary across plays:
- $p_{\text{red}} = 0.5$
- $p_{\text{blue}} = 0.9$

### How students discover the regularity across plays

The student's sheet has a `water_result` column where each watering attempt
is marked ✓ or ✗. After play 1 students pool their per-plot water success
counts and form an empirical estimate of each probability.

- **Play 1 (~4-6 water attempts):** each student individually has
  noisy evidence but notices "blue seems to work, red is iffy." Pooled
  class evidence resolves this.
- **Play 2:** students focus all plant-water chains on blue; red is used
  only if the blue plot is already committed to a ripening chain.

### Greedy-trap

A greedy student harvests at flower stage every time they have a flower,
scoring 3 per harvest. Because watering red is stochastic, they often fail
to advance red past seedling, harvesting it at 0. Net score stays around
6–9.

### Blind-reservation trap

"Blind reservation" doesn't directly apply here (no explicit reservation
sampling), but its analog — **blind blue/red mixing** — does. A student
who splits attention between plots without tracking which one is reliable
wastes ~half of their water attempts on the low-p plot. Score suffers
symmetrically to greedy's.

### Debrief script (play-to-Bellman)

1. Histogram.
2. "What did your water-result column show you?" Elicit: "blue worked
   most of the time; red often failed."
3. "What did you do differently in play 2?" Elicit: "I only planted blue,
   or I planted blue first and put leftover budget into red."
4. Name it: "You estimated a **transition probability**: given the action
   Water_blue and a seedling, what is the probability the next state is a
   flower?"
5. Write: $V(s) = \max_a [\, r(s,a) + \gamma\, \sum_{s'} p(s'\mid s,a)\,V(s')\,]$.
   Note that watering a blue seedling has expected value
   $0 + 0.9 \cdot V(\text{blue flower}) + 0.1 \cdot V(\text{blue seedling
   still})$. Watering a red seedling has expected value
   $0.5 \cdot V(\text{red flower}) + 0.5 \cdot V(\text{red seedling still})$.
   The difference in expected value is how you derived the blue-first
   policy.
6. Play-2 histogram sharpens and shifts.
7. Generalize: this is exactly how a model-based RL agent plans once it
   has learned a transition model.

### Materials

- One slide with rules.
- Per-student 2-plot sheet: 6 rows (turns) × 7 columns [turn, action,
  water_result ✓/✗, R_stage, B_stage, budget, score].
- Instructor's pre-generated per-attempt water-result sequence OR a coin/
  die flipped live (0.5 for red: pair of coin flips, success iff HH or HT
  — actually just a fair coin; 0.9 for blue: a d10, success iff ≠ 10).
- Sticky notes.

### Time budget

| Segment | Time |
|---|---|
| Rules | 1:00 |
| Play 1 (6 turns × 35-40s) | 4:00 |
| Histogram + water-success pool | 1:00 |
| Debrief (transition model + Bellman) | 4:00 |
| Play 2 | 4:00 |
| Close | 1:00 |

### Rank justification (#3)

Mystery Gardener teaches **Bellman with stochastic transitions** — the
most textbook-faithful MDP structure of the three. It ranks third because:
(a) the per-play evidence on watering success is thin (~4-6 attempts per
student per play), requiring class-wide pooling to pin down probabilities;
(b) the debrief must introduce a summation-over-next-states expectation,
which is the heaviest math of the three; (c) students who fixate on the
plant/water/harvest arithmetic can lose sight of the learning dimension.
For a CS / RL-oriented course it is the deepest of the three; for a first
introduction to Bellman it is the most demanding.

---

## Summary comparison

| Game | Hidden regularity | Learnability surface | Best audience |
|---|---|---|---|
| Colored Row v3b | $\mathbb{E}[r\mid\text{color}]$ per color | per-color tally column | general, first exposure |
| Mood Market v3 | 2-state Markov on rating regime | last-rating column + feel for runs | finance/time-series minded |
| Mystery Gardener | Per-plot watering success $p$ | water-result column per plot | CS/RL-heavy |

All three fix v1's defect: the optimal policy is contingent on a learned
quantity, so pure blind-reservation fails alongside pure greedy, and the
behavior change between play 1 and play 2 is the visible pedagogical
payload.
