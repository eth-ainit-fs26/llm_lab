# Bellman Committee Log v2 — 20 Rounds (Learnability Fix)

## Why v2 exists

v1 converged on Restaurant Row (reactive chef), Patient Gardener, and Hiker's
Dilemma. Reviewing the transcript later, the committee caught a structural
defect: rewards were drawn from a pre-generated sequence with no exploitable
stationary pattern. Greedy failed, far-sighted play won — but students could
not **learn** the environment from one play to the next. Any lesson drawn was
"don't eat too early," not "use what I saw earlier to predict what's coming."
That is reservation-sampling / secretary-problem intuition, not Bellman.

The Bellman equation has two halves:

$$V(s) = \max_a \bigl[\,r(s,a) + \gamma\, \mathbb{E}_{s' \sim p(\cdot\mid s,a)}\,V(s')\,\bigr]$$

- **Outer max**: pick the action with highest sum of immediate plus discounted future.
- **Inner expectation**: know $p(s'\mid s,a)$ and $r(s,a)$ — i.e., have a *model*.

A v1-style game exercises only the outer max. v2 must force students to *also*
estimate the inner expectation from observed history. The banned design is
i.i.d. rewards with no structure. The required design is a hidden but
stationary regularity — a Markov reward process, color-coded distributions, a
biased coin/die, a deck with unknown composition — whose parameters students
infer from play and exploit the next play.

**Three-pronged target, restated:**
1. Value-of-future dominates value-now (unchanged from v1).
2. Past matters for action choice (unchanged from v1).
3. **NEW**: past matters *predictively* — observing the first half of a play
   lets you forecast the second half better than a student who started late
   can.

**Hard dual failure condition:**
- Pure greedy underperforms.
- Pure blind reservation-sampling ("wait for a big number, then grab") also
  underperforms, because the optimal threshold depends on the hidden
  parameters the student is learning.

The committee now runs 20 rounds under the new charter.

---

## Round 1

**MODERATOR.** Three-pronged goal: (a) value-of-future beats value-now,
(b) look-at-past for action choice, (c) **LEARNABILITY** — the environment
has a hidden but stationary regularity that past observations reveal. Banned:
i.i.d. noise. Encouraged: hidden Markov rewards, hidden reward distributions
by visible tag, unknown deck composition, biased coin/die.

**DESIGNER_A — "Colored Restaurant Row."** Row v3s structure, but each
restaurant now wears a visible *color tag* (red, blue, green). The rating is
drawn from a color-specific distribution hidden from students: red ~ N(3,1),
blue ~ N(6,1), green ~ N(8,1) (truncated to 1-10). The instructor announces
the color of a restaurant *one step ahead* (before decision) while the rating
itself is revealed only on arrival. Students must learn the mapping color →
reward across plays, and within a play use the color lookahead to plan
EAT/SKIP. Greedy eats on any 6+; blind reservation ignores the color signal.
Far-sighted + color-aware wins. Hidden regularity: the three color→mean
mappings. Plays across time make this discoverable; 8 restaurants per play
gives ~8 labeled observations per play.

**DESIGNER_B — "Suit-Stream Solitaire."** A shuffled 24-card deck (A, 2-9 of
four suits, minus some). Each turn instructor reveals top card. Student
chooses KEEP (score += rank, lose 1 of 3 keeps) or PASS. But hearts pay
double on KEEP, and clubs pay the rank **plus the rank of the previous card
kept**. Hidden regularity: the deck is *stacked* — the instructor
pre-shuffles so that hearts cluster in the back half, clubs in the first
half. Students who notice the suit-ordering bias on play 1 can exploit it on
play 2 (save keeps for hearts at the end). Greedy grabs the first high card;
blind reservation waits for any ≥8 regardless of suit.

**PLAYTESTER.**
- *Colored Row:* Promising. With 8 restaurants per play, a student sees
  roughly 2-3 restaurants of each color in play 1 — enough to notice green >
  blue > red in mean, but variance σ=1 can make single observations
  misleading. Across 2-3 plays the color mean becomes robust. Within a play,
  the one-step color lookahead lets students anticipate. Greedy fails: eating
  a red 5 burns a slot. Blind reservation fails: waiting for a 9 ignores that
  a green 7 is a signal of an even better green ahead.
- *Suit-Stream:* Pattern is "deck stacking." That's a *specific* puzzle, not
  a stationary environment property. Also stacking is either noticed
  instantly or never — bimodal discoverability, bad pedagogy.

**STUDENT_VOICE.** Colored Row: "so the colors tell me something about how
good the food will be? I can work with that." Suit-Stream: "was the deck
rigged? wait, am I supposed to count cards?"

**MODERATOR synthesis.** Colored Row is aligned with the new charter: visible
feature → hidden distribution, learnable in 1-2 plays. Suit-Stream is either
too cryptic or reduces to card-counting. Next round: push on Colored Row;
also bring a non-restaurant alternative to diversify the search.

---

## Round 2

**MODERATOR.** Stay on Colored Row. Second designer bring something
non-restaurant with the same structural property: visible tag predicts hidden
reward.

**DESIGNER_A — "Colored Row v2."** Tighten to two colors (red, blue) with
more separated means to make the regularity easier to spot: red ~
Uniform{1,2,3,4}, blue ~ Uniform{5,6,7,8,9,10}. 8 restaurants, each flagged
with a color BEFORE reveal. Student sees color, then decides EAT/SKIP before
rating is announced. EAT uses a slot (4 slots); lowered next rating by 2
(the reactive-chef carry-over from v1) preserved. Hidden regularity: two
distributions per color. Across plays students learn "blue is always in the
5-10 range, red is always 1-4." Within a play: skip reds, save slots for
blues. Greedy eats on any first reveal; reservation waits for ≥8 ignoring
color information.

**DESIGNER_B — "Weather Walker v2."** 10-day trip. Each day weather is
revealed (sun/cloud/rain) *before* the student commits to OUTSIDE/INSIDE.
OUTSIDE yields a reward that depends on weather *and* the 2-state hidden
climate regime (summer vs winter) which is constant throughout a single trip
but resampled between plays. In "summer" regime: sun=+8, cloud=+3, rain=-2.
In "winter" regime: sun=+3, cloud=0, rain=-6. INSIDE yields +1 always.
Student does not know the regime; must infer from the first few days of
outcomes. Across plays, students learn both reward tables; within a play,
the first 2-3 OUTSIDE outcomes pin down the regime, and then the remaining
days should be played according to it.

**PLAYTESTER.**
- *Colored Row v2:* Red vs blue is easy to learn — maybe too easy. After 1
  full play with 8 reveals, even a student glancing at their notes sees
  "reds have been 2, 3, 1, 4; blues have been 6, 9, 7." Play 2 becomes a
  purely optimization task (allocate 4 slots to blues, skip reds). That is
  Bellman-optimal but the learning phase collapses to one play. Still,
  bimodal scoreboard should be visible.
- *Weather Walker v2:* Two layers of learning (regime inference + value
  policy). Richer but risks overload: students are doing Bayesian updating
  and planning simultaneously. The Bellman framing gets diluted by the
  regime inference.

**STUDENT_VOICE.** Colored Row v2: "wait, red is always bad? then I just skip
all reds." That's the correct insight. "But do I know the distribution is
stable across plays?" — that's the meta-learning question and it's exactly
what we want them to realize. Weather Walker: "am I doing Bayes or DP?"

**MODERATOR synthesis.** Colored Row v2 — the learning collapsing to one play
is a *feature*, not a bug, for a 15-minute classroom block. Weather Walker is
too rich. Next round: is Colored Row's regularity too trivial? Make it harder
without breaking the brief.

---

## Round 3

**MODERATOR.** Pressure test: is Colored Row v2's regularity too easy to spot?
Try variants with more colors or with overlapping distributions.

**DESIGNER_A — "Colored Row v3 (three colors, overlapping)."** Three colors
— white, gray, black. White mean 3, gray mean 5, black mean 7, all σ=1.5.
10 restaurants per play, 5 slots, reactive-chef off (too many moving parts).
The overlap makes one-play learning noisier; students need 2 plays to nail
ranking. Within a play, use the running sample mean per color as the
prediction.

**DESIGNER_B — "Marked Deck."** A deck of 40 cards: 10 red (value ~
Uniform{1-4}), 10 yellow (value ~ Uniform{3-6}), 10 green (value ~
Uniform{5-8}), 10 blue (value ~ Uniform{7-10}). Deck shuffled. Each turn,
top card's *color* revealed; student chooses TAKE (score += value, lose 1 of
4 takes, card value revealed) or PASS (card discarded face-down). 12 cards
per play. Hidden regularity: color → value-range mapping, AND the deck
composition means later in the deck each remaining color is a bit rarer
(light card-counting). But the main hidden structure is color → range, just
like Colored Row, but in card-game costume.

**PLAYTESTER.**
- *Colored Row v3:* Overlapping gaussians make the first play's inference
  uncertain. On play 1 students who glimpsed a few whites and blacks might
  nail the ranking; students who happened to see bad blacks and good whites
  will mis-rank. Play 2 is the clarifying play. Good: 2 plays is the
  pedagogical sweet spot.
- *Marked Deck:* Same structure as Colored Row but the card metaphor might
  resonate better for non-food-loving students. Also the "deck depletion"
  effect (slight card counting) adds a layer. Worried it's too similar to
  Colored Row and we're just reskinning.

**STUDENT_VOICE.** Colored Row v3: "three colors is one more to remember but
doable." Marked Deck: "so colors on cards do the same thing as colors on
restaurants. Same game different clothes."

**MODERATOR synthesis.** v3 is the right tightness. Marked Deck is a reskin.
Next round: push in a direction that's not distribution-by-visible-tag —
something like a hidden Markov reward chain.

---

## Round 4

**MODERATOR.** Explore hidden Markov rewards: reward value at step t depends
on reward value at step t-1. That makes history predictive of future in a
time-series sense, not a color-lookup sense.

**DESIGNER_A — "Mood Market."** A 10-step trading game. Each step shows a
numeric rating (1-10) and the student chooses BUY (score += rating, lose 1
of 4 buys) or SKIP. The hidden regularity: rating at time t+1 is *correlated*
with rating at time t. Specifically, there's an unobserved "market mood"
which is a 2-state Markov chain (bull vs bear). Ratings in bull mood are
drawn from {7,8,9,10} uniform; in bear mood from {1,2,3,4} uniform. Mood
transitions: bull → bull w.p. 0.8, bear → bear w.p. 0.8. So runs of high
ratings beget more high ratings; runs of lows beget lows. Students must
recognize regime from history and use a regime-conditional policy.

**DESIGNER_B — "Traffic Chooser."** 8-intersection commute. At each
intersection, student picks LEFT, STRAIGHT, or RIGHT. Each direction yields a
time cost (1-10). Hidden regularity: costs are correlated across directions
at the same intersection — if LEFT cost was high at intersection t,
STRAIGHT cost is likely low at intersection t, because there's a hidden
"traffic flow" variable. Goal: minimize total cost across 8 intersections.
Students learn the anti-correlation across plays.

**PLAYTESTER.**
- *Mood Market:* The Markov-regime structure is beautiful and it genuinely
  fits the Bellman frame — state must include recent history. Three things
  to watch: (a) with only 10 steps and a 2-state chain, within-play evidence
  is thin; (b) bull↔bear switches during a play are rare (0.2 per step) so
  most plays spend most time in one regime; (c) students might not notice
  the Markov property if the play starts in a stable regime.
- *Traffic Chooser:* The anti-correlation trick is cute but intersection-by-
  intersection it's a 1-step game; no cumulative reasoning. Also teaches
  "read the pattern" not "value future reward."

**STUDENT_VOICE.** Mood: "after 4 high ratings I feel like the next will be
high too — is that right? Yes!" Traffic: "I just pick the lowest, no?"

**MODERATOR synthesis.** Mood Market has the right theoretical shape (hidden
Markov regime, stationary transition parameters, learnable across plays) but
within-play evidence density is a concern. Next round: fix the evidence
density problem.

---

## Round 5

**MODERATOR.** Mood Market is structurally elegant but thin on evidence per
play. Options: lengthen the play, use a 3-state chain, or make the regime
observable-but-indirect.

**DESIGNER_A — "Mood Market v2."** Keep the 2-state Markov mood, but lengthen
to 16 steps with 6 buys. Now within a play, students will see 4-5 regime
transitions on average, which is enough to feel the "runs happen" property.
Play 2 with a new random instance lets them confirm the transition
probabilities are stable. State: (step, buys_left, last_rating). Optimal
policy: buy when last_rating was high (persistence of bull regime) AND
buys_left × future_steps justifies it; skip when last_rating was low (bear
persistence).

**DESIGNER_B — "Die of Many Faces."** A custom d10 with hidden bias (the
instructor has actually written the numbers so that 3 faces show 1, 3 faces
show 10, 4 faces show middle values — but students don't know the
distribution). 12 rolls per play. After each roll the student may BANK
(score += last roll, lose 1 of 4 banks) or ROLL_AGAIN. Students must infer
the die's distribution from observed rolls and decide whether to bank
intermediate values. Hidden regularity: die's face distribution is
stationary across plays, so students carry learned knowledge forward.

**PLAYTESTER.**
- *Mood Market v2:* Yes — 16 steps with a 0.2 transition probability
  delivers about 3 transitions per play. A student can feel the
  bull-streak/bear-streak pattern. Across plays, they confirm the
  transition structure is consistent. Blind reservation (wait-for-8) does
  okay in bull regimes and terribly in bear regimes; regime-aware play
  dominates.
- *Die of Many Faces:* This is classic bandit-with-stopping. Students
  estimate the die's reward distribution and set an optimal threshold. But
  the game is a single-arm stopping problem — no state transition, no value
  propagation. It exercises reward-model learning but not the Bellman
  recursion over states. Rejecting for our target.

**STUDENT_VOICE.** Mood Market v2: "once I saw two 9s in a row, I felt the
regime was set and I just waited for my buy chance in the 9-run." Die:
"I'm learning the die, but it doesn't feel like a sequence decision."

**MODERATOR synthesis.** Mood Market v2 has the learnability-plus-Bellman
shape we want. Die-of-Many-Faces exercises reward model inference alone,
which we want to *combine with* Bellman, not replace. Next round: try a game
that combines hidden distribution (like Colored Row v3) with hidden state
transitions (like Mood Market) and see if the combination enriches or
overloads.

---

## Round 6

**MODERATOR.** Either combine Colored Row and Mood Market, or stage them as
separate candidates and compare.

**DESIGNER_A — "Colored Row v4."** Each restaurant has a color (red or blue)
flagged before the student commits. Hidden regularity: color mean is fixed
per play (red low, blue high, say red ~ U{1-5}, blue ~ U{5-10}), BUT
consecutive restaurants of the same color have correlated ratings (σ
shrinks). So runs of blues tend to be similarly rated. This adds a mild
Markov layer within color. Probably overloaded.

**DESIGNER_B — "Mood Market v3 with color coding."** Each step shows both a
rating (hidden until decision) and a visible "mood indicator" color (gold
for bull regime, navy for bear). The color IS the regime, made visible.
Simplifies the learning problem: students don't need to infer the regime,
only the regime-conditional reward distribution (which is easy) and the
regime-conditional optimal policy. Wait — this over-simplifies, because now
the regime is observed and the student only has to learn two reward
distributions, turning this into a slightly more elaborate Colored Row.

**PLAYTESTER.**
- *Colored Row v4:* Runs-of-color-with-correlated-ratings is elegant in
  theory but hard to notice. Students would fixate on "blue = good, red =
  bad" and miss the within-color correlation. Two layers of hidden structure
  — one layer discoverable in 2 plays, second layer discoverable maybe in
  5 plays — doesn't fit the time budget.
- *Mood Market v3:* Exposing the regime through color reduces the game to
  Colored Row v3. Defeats the point of Mood Market's hidden-state elegance.

**STUDENT_VOICE.** Colored Row v4: "so the colors AND the ratings both have
patterns? which one am I supposed to focus on?" Mood Market v3: "okay so
gold is good, navy is bad. Got it, nothing new."

**MODERATOR synthesis.** Combining is a trap. Keep Colored Row v3 and Mood
Market v2 as two distinct candidates. Next round: generate a third candidate
with a different flavor — perhaps a sampling-with-replacement / hidden-
composition game.

---

## Round 7

**MODERATOR.** Third candidate with a different kind of hidden regularity —
unknown composition or biased probability.

**DESIGNER_A — "Coin-Flip Caravan."** A 10-step caravan route. Each step, the
instructor flips a coin behind a shield and announces HEADS (+5 reward if
student chose ADVANCE, 0 if CAMP) or TAILS (-3 if ADVANCE, 0 if CAMP). The
student chooses ADVANCE or CAMP at each step. Hidden regularity: the coin is
biased (maybe 0.7 for heads, maybe 0.3 — unknown to students). Students must
infer the bias from observed outcomes and choose accordingly. Budget of 4
CAMPs (otherwise forced to ADVANCE). Also: a high-reward "oasis" at step 10
(+20 if student is alive with score ≥ 0).

**DESIGNER_B — "Two-Box Bandit Walk."** A 12-step game. At each step
student picks box LEFT or box RIGHT; a reward is drawn from a box-specific
unknown distribution and added to score. Each box has a stationary
(but hidden) mean reward. Students learn which box is better from
experience. Standard multi-armed bandit with reward-model learning.

**PLAYTESTER.**
- *Coin-Flip Caravan:* Interesting — biased-coin inference plus a terminal-
  reward state. The optimal policy depends on the learned bias: high bias =
  keep advancing, low bias = camp strategically. But camp-vs-advance is a
  binary choice with a budget — reduces to a simple threshold on belief
  about the bias. Too thin.
- *Two-Box Bandit Walk:* Classic two-armed bandit. Exercises reward model
  learning and exploration-exploitation but not cumulative-future value
  propagation through states. No state transitions mean no Bellman recursion.
  Rejecting for our target (as we rejected Die-of-Many-Faces in round 5).

**STUDENT_VOICE.** Coin-Flip: "so I'm guessing if the coin is fair? this is a
statistics question." Two-Box: "I just pick whichever box has the higher
average so far."

**MODERATOR synthesis.** Both rejected. Bandits and simple coin-inference
don't exercise the Bellman recursion. For learnability to be *Bellman
learnability*, the hidden regularity must touch either (a) transition
probabilities or (b) the reward function in a way that compounds across a
multi-step decision chain. Next round: revive the Gardener design with a
learnable twist.

---

## Round 8

**MODERATOR.** Revisit v1's Gardener with a learnability layer.

**DESIGNER_A — "Mystery Gardener."** Gardener v3 from v1 (2 plots, 6 turns,
budget 8, plant-water-harvest). New twist: watering advances plot stage
*stochastically* with a hidden success probability. Specifically, each
watering succeeds (advances stage) with probability p_plot, where p_red = 0.5
for red-marked plots, p_blue = 0.9 for blue-marked plots. Plots are marked
visibly. Students don't know p at first. Across plays, they infer
p_blue > p_red. Within a play, optimal policy: plant on blue plot first
(high success rate of watering chain), water twice, harvest ripe.

**DESIGNER_B — "Weather-Linked Investment."** 6-turn investment game. Each
turn, weather (known in advance one turn ahead) is sunny or cloudy. Actions:
PLANT_SEED (cost 1, grows to fruit in 2 sunny turns, or 3 cloudy turns, or
indeterminate mix), HARVEST (free, +5). Hidden regularity: weather is an iid
Bernoulli with a fixed unknown bias — students learn bias from play 1 and
use it to plan in play 2. The optimal policy is contingent on bias: high-
sun prob → plant early; low-sun prob → shorter investment horizons.

**PLAYTESTER.**
- *Mystery Gardener:* The learnability is clean (inferring water success
  probability from count of successful waters per plot per play), and the
  Bellman recursion over plot stages is unchanged from v1. Within-play
  learning is real: after 2-3 waterings on each plot a student has a Beta
  posterior they can feel. Across-play learning is rock-solid: the two
  probabilities are fixed. Greedy "harvest at flower" ignores the watering
  success issue; blind reservation doesn't apply meaningfully because
  there's no reservation. But blind policy without learning the colors gets
  unlucky on red plots. Good.
- *Weather-Linked Investment:* Cool but the weather announcement one turn
  ahead means the learning task is "Bayesian update on the weather bias"
  which is an intellectual side-quest distinct from the Bellman planning.

**STUDENT_VOICE.** Mystery Gardener: "So the BLUE plots are better? Let me
track the success rates." Weather Invest: "I'm tracking weather frequencies
and planning harvests at the same time — overload."

**MODERATOR synthesis.** Mystery Gardener is a clean evolution of v1's
Gardener with the learnability patch. Candidate pool now: Colored Row v3,
Mood Market v2, Mystery Gardener. Next round: simulate play-through of each
and report on whether greedy AND blind-reservation both fail.

---

## Round 9

**MODERATOR.** Head-to-head simulation. For each of the three candidates,
describe a concrete play sequence, greedy's score, blind-reservation's score,
and the Bellman-aware optimal score.

**DESIGNER_A — "Colored Row v3 simulation."**
- Setup: 10 restaurants, 5 slots, colors {white, gray, black}, means {3, 5,
  7}, σ ≈ 1.5.
- Concrete play: colors [W, G, B, W, G, B, B, G, W, B], ratings drawn from
  those distributions come out as [3, 5, 7, 2, 6, 7, 8, 4, 4, 9].
- Greedy (eat any ≥ 6): eats 5 (wait, ≥6, so eats 6, 7, 7, 8 on positions
  3, 6, 7 — actually positions 3 (B, 7), 5 (G, 6), 6 (B, 7), 7 (B, 8) — uses
  4 slots, score = 28. Then sees 4, 4, 9 and has 1 slot left, eats 9,
  score = 37. Greedy with ≥6 threshold lucky here.
- Greedy eats any ≥5: fills slots fast on 5, 7, 6, 7, 8 = 33. Plus the 9 if
  slot remains. Mixed.
- Blind reservation (wait for any ≥8): sees no 8+ until position 7 (8),
  eats. Then position 10 (9), eats. Then has 3 slots unused = forfeited.
  Score = 17 plus any leftover 0's = 17. Failure.
- Optimal (color-aware): skip all W's (mean 3, almost certainly < 5); save
  slots for G's and especially B's. Here B positions are 3, 6, 7, 10 (ratings
  7, 7, 8, 9) — eat all four = 31. Then one extra slot used on best G:
  position 5 (6) = 37 total, maybe 38 with 8 at position 7 and 9 at 10.
  Color-aware easily matches or beats greedy, and dominates blind
  reservation.

**DESIGNER_B — "Mood Market v2 simulation."**
- Setup: 16 steps, 6 buys, 2-state Markov mood (bull/bear, p_stay = 0.8).
  Rewards: bull ~ U{7-10}, bear ~ U{1-4}.
- Concrete play: mood sequence B, B, B, b, b, B, B, B, b, B, B, B, b, b, B,
  B (B=bull, b=bear). Ratings [7, 9, 10, 4, 2, 8, 9, 10, 1, 8, 7, 8, 3, 2,
  10, 9].
- Greedy (buy anything ≥5): burns 6 buys on positions 1, 2, 3, 6, 7, 8 =
  7+9+10+8+9+10 = 53. Accident of good run at the start.
- Greedy (buy anything ≥3): fires at position 1 (7), 2 (9), 3 (10), 4 (4) —
  score 30 after 4 buys, wasted a buy on a 4 that signals bear regime.
  Finishes 30 + 8 + 9 = 47 if lucky with remaining buys.
- Blind reservation (wait for 10): sees 10 at position 3 (buy), position 8
  (buy), position 15 (buy), position 16 (buy if 9 counts as ≥ threshold) —
  scores 40 with 2 buys unused. Failure to fully use budget.
- Optimal (regime-aware): use last-rating as regime estimate. After step 1
  (7, high), probably bull, prepare to buy. After step 4 (4, low), regime
  flipped to bear, stop buying; wait. After step 6 (8, back to bull), buy
  aggressively. Use 6 buys distributed across observed bull runs = score
  closer to 55+. Dominates blind reservation AND greedy.

**PLAYTESTER.** Both play out cleanly. Mood Market's regime-dependence is
visceral — students genuinely feel "I just saw a bear streak, the next one
is probably bear too." Colored Row's tag-learning is concrete and
algorithmic. Mystery Gardener is structurally more complex to simulate by
hand; next round will cover it.

**STUDENT_VOICE.** Both simulations: "I can see why waiting for a 10 only
works if 10s are common — it's terrible when they're rare."

**MODERATOR synthesis.** Both pass the dual-fail test cleanly. Mystery
Gardener simulation deferred. Next round cover that and compare all three.

---

## Round 10 (midpoint check)

**MODERATOR.** Halfway. Simulate Mystery Gardener and then rank.

**DESIGNER_A — "Mystery Gardener simulation."**
- Setup: 2 plots (one red, one blue), 6 turns, budget 8. Plant cost 2, water
  cost 1, harvest free. Water success: p_red = 0.5, p_blue = 0.9.
- Concrete play 1 (students don't know p): student plants red (t=1,
  budget=6), plants blue (t=2, budget=4), waters red (t=3, budget=3, flip
  internal coin: fail, stage stays seedling), waters blue (t=4, budget=2,
  succeeds, blue is flower), waters red (t=5, budget=1, flip: succeed, red
  flower), waters blue (t=6, budget=0, succeeds, blue is ripe, but game
  ending). Auto-harvest at end: blue ripe = 8, red flower = 3. Total 11.
  Student observes: 2 attempts on red, 1 success (50%); 2 attempts on blue,
  2 successes (100%). Noticeable asymmetry.
- Play 2 (armed with p estimate): student plants blue first, waters blue,
  waters blue (both succeed, now ripe), harvests blue = 8. Plants blue again
  (since red is risky), waters... no budget. Alternatively: plant blue,
  plant red, water blue, water blue, harvest blue (8), harvest red-seedling
  = 0. Total 8. Actually the right strategy is: focus budget on blue,
  ignore red. Plant blue (2), water (1), water (1), harvest (0) = 8 with
  budget used = 4; with 4 remaining: plant blue (2), water (1), water (1),
  harvest not possible within 6 turns anymore. Actually you hit turn limit.
  Final policy: plant blue, water, water, harvest (4 turns, 4 budget, score
  8). Then plant blue, water, water (turns 5-6 and budget 4 more = 8 total
  used) — harvests auto at end for ripe = 8. Total 16 from blue alone. Much
  better than 11.
- Greedy: harvest at flower stage (value 3) each time. On red plots often
  fails to advance (stuck at seedling). Scores low, maybe 6.
- Blind reservation: unclear what that even means here — not applicable.
- Optimal: always plant blue, ignore red. Play 1 noisy due to learning; play
  2 clean.

**DESIGNER_B — "Ranking proposal."**
1. Colored Row v3 — visible tag → hidden distribution, easy to explain in
   60s, learnable in 1-2 plays.
2. Mood Market v2 — hidden Markov regime, rich Bellman structure, but
   requires more explanation.
3. Mystery Gardener — elegant but 6-turn investment game has less room for
   felt learning per play.

**PLAYTESTER.** Agree with ranking. Mystery Gardener's learnability is real
but shallow per play — only 4-6 watering attempts total, which is thin
evidence. Mood Market's learnability is continuous across 16 steps. Colored
Row's learnability is explicit and labeled.

**STUDENT_VOICE.** "Colored Row was the easiest to explain to my roommate
after class."

**MODERATOR synthesis.** Leader: Colored Row v3. Strong second: Mood Market
v2. Third: Mystery Gardener. Next round: stress-test Colored Row's
discoverability — is the color pattern too obvious or is it just right?

---

## Round 11

**MODERATOR.** Discoverability audit on Colored Row v3. Is one play enough
to see the pattern? Is it too few? Should we push to 3 colors with more
overlap?

**DESIGNER_A — "Colored Row v3a: 2 colors, 2 plays."** 8 restaurants, red
(U{1-5}) and blue (U{5-10}). 4 slots. Color announced before decision. Play
1 with one sequence of (color, rating) pairs, play 2 with a fresh sequence.
Learnability audit: after play 1, a student sees ~4 restaurants of each
color. Observed reds might be [2, 4, 3, 5], blues [8, 6, 9, 7]. Easy to spot
blue > red. Play 2 confirmed.

**DESIGNER_B — "Colored Row v3b: 3 colors, 3 plays."** 9 restaurants, white
(U{1-4}), gray (U{3-7}), black (U{6-10}). 4 slots. Overlap between gray and
neighboring colors makes single-play inference ambiguous. Students see ~3 of
each color per play, pooled across 2-3 plays = 6-9 observations per color,
which is enough for a reliable ranking.

**PLAYTESTER.**
- *v3a (2 colors, 2 plays):* After play 1 most students know blue > red.
  Play 2 is the optimization play. Clean. Risk: too easy — students feel no
  uncertainty. Debrief doesn't need to address "how confident was your
  model"; the model was obvious.
- *v3b (3 colors, 3 plays):* After play 1, black > white clear, gray
  ambiguous. After play 2, gray clearer. Play 3 is full optimization. BUT
  3 plays is ~12 minutes of play alone, tight for a 15-minute block.

**STUDENT_VOICE.** v3a: "easy." v3b: "I had to combine observations from
plays 1 and 2 to trust my gray estimate." — this is the good reaction.

**MODERATOR synthesis.** v3b's 3-color, 3-play structure is richer but tight
on time. Consider a 15-minute budget: 1 rules + 3 * 3-min plays + 5 min
debrief + 2 min play-2-vs-play-3 histogram comparison = 16 min. 1 minute
over. Tradeoff: v3a fits comfortably, teaches "learn then optimize";
v3b pushes the time but teaches "continuously refine your estimates across
plays." Next round: decide.

---

## Round 12

**MODERATOR.** Commit: v3a or v3b?

**DESIGNER_A — "Go with v3b (3-color 3-play)."** The slightly-too-easy v3a
risks students missing the learnability lesson ("the colors told me
everything, I didn't really LEARN"). v3b forces them to feel the update —
"after play 1 I thought gray was mid-tier, but play 2 showed me gray is
basically the same as black. I updated." That's the Bellman-learnability
lesson: you are building a model from experience, and your policy improves
as your model sharpens.

**DESIGNER_B — "Concession and refinement."** Agree with A on v3b, but trim
to 8 restaurants per play (not 9), drop to 2 plays with an optional 3rd, and
announce during the rules that students should track running per-color
averages on their sheet. The tracking sheet makes the learning visible and
saves time.

**PLAYTESTER.** v3b with 8 restaurants, 3 slots, per-color tally column on
the sheet, 2 plays guaranteed, 3rd if time: fits in 15 minutes. After play 1
the histogram is wide (students mis-rank gray frequently); after play 2 the
histogram sharpens (most have learned the ranking). The *shift in histogram
sharpness* is the pedagogical payload — it's what "learning $V(s)$" looks
like across a cohort.

**STUDENT_VOICE.** "The per-color average column was the single most useful
piece of paper in the game — I literally watched my estimates get better."

**MODERATOR synthesis.** Committed: Colored Row v3b with 8 restaurants, 3
slots, 3 colors with overlapping means, per-color tally column on the
student sheet, 2 plays (optional 3rd). Next round: strengthen or drop Mood
Market and Mystery Gardener.

---

## Round 13

**MODERATOR.** Mood Market v2 and Mystery Gardener — final forms.

**DESIGNER_A — "Mood Market v3 (final)."** 16 steps, 6 buys, 2-state Markov
mood (bull/bear, p_stay = 0.8). Bull rewards U{7-10}, bear rewards U{1-4}.
Student sheet has columns: step, rating revealed, BUY/SKIP, running score,
**last_rating (as regime indicator)**. The last_rating column is the
crucial visualization — it makes the regime visible to the student.
Decision rule candidates: if last_rating ≥ 5, probably bull, buy when above
some threshold. If last_rating ≤ 4, probably bear, always skip unless down
to last buys.

**DESIGNER_B — "Mystery Gardener final."** 2 plots (red and blue), 6 turns,
budget 8. Water success: p_red = 0.5, p_blue = 0.9. Student sheet: turn,
action (Plant_R/Plant_B/Water_R/Water_B/Harvest_R/Harvest_B), result (for
watering: success/fail), plot stages, budget, score. The "result" column for
watering is where students accumulate evidence. Across 3 plays they pin
down both probabilities.

**PLAYTESTER.**
- *Mood Market v3:* Excellent. The last_rating column does all the work —
  students see the signal. Transition to bull is signalled by high last_rating
  persistence; same for bear. Blind reservation (wait for 10) now visibly
  fails in bear-long plays; greedy (buy anything ≥ 5) fails when bear regime
  drops in and the student keeps buying threshold-crossings. Regime-aware
  policy dominates in simulation and in expected group play.
- *Mystery Gardener final:* Works but only if students play 3+ times. In 2
  plays, evidence on p_red vs p_blue is 4-6 observations per plot per play
  = 8-12 total per plot after 2 plays, enough for a Bayesian to see a
  difference but students don't compute Bayes. Qualitatively, students will
  say "blue worked more often." Good enough.

**STUDENT_VOICE.** Mood: "once I noticed the high numbers come in clusters,
the game became controllable." Gardener: "blue plots grew better, I
remember that for next time."

**MODERATOR synthesis.** Both in top-3 territory. Next round: a 4th
candidate that might displace one — specifically something with a hidden
state that isn't reward-related directly but transition-related.

---

## Round 14

**MODERATOR.** Fourth candidate: hidden transition structure (not reward
structure).

**DESIGNER_A — "Slippery Staircase."** 10-step staircase. Each step student
chooses CLIMB or PUSH. CLIMB advances one step with probability p_success
(hidden, fixed within a play, drawn from {0.5, 0.7, 0.9} at start of play).
CLIMB fail means staying at current step. PUSH always advances but costs 1
of 3 energy tokens. Reward: value of the step you finish on after 10 turns
(values 1, 2, 3, ..., 10 ascending). Students infer p_success from observed
CLIMB outcomes. Given p high, mostly CLIMB; given p low, use PUSH tokens
liberally.

**DESIGNER_B — "Biased River."** Cross a 6-cell river. Each cell, choose
STEP (advance 1 with probability p_step, slip back 1 with probability 1-p_step)
or CAST (spend 1 of 3 rope casts, advance 2 with probability 1, no slip).
Goal: reach cell 6 in minimum turns to maximize a time-based bonus.
Hidden: p_step (fixed, stationary across plays). Learnable after a few
attempts.

**PLAYTESTER.**
- *Slippery Staircase:* Clean structure — hidden transition probability,
  learnable, and the optimal policy (when to use energy tokens) depends on
  the inferred probability. BUT the state involves a stochastic Markov chain
  over positions, which students find hard to reason about without a
  whiteboard simulation. Risk: the "Bellman" part (decide when to PUSH
  based on P(reach-end-in-time | current step, energy, p_success))
  requires explicit probability reasoning that a 5-min classroom game
  doesn't afford.
- *Biased River:* Same problem in miniature. Elegant but the probabilistic
  planning layer adds cognitive load.

**STUDENT_VOICE.** Staircase: "so I'm learning the probability AND planning
when to use tokens? That's a lot." River: "similar."

**MODERATOR synthesis.** Both overloaded. The learnability constraint
creates a natural tension: too little hidden structure = i.i.d. problem
(v1's flaw), too much = overload. The sweet spot is *one* hidden quantity
per play, not two. Colored Row (means per color), Mood Market (transition
probs), Mystery Gardener (watering success per plot) each have one. Keep
that constraint. Next round: one more attempt at a 4th candidate, but with
only-one-hidden-thing.

---

## Round 15

**MODERATOR.** 4th candidate, single hidden quantity, classroom-ready.

**DESIGNER_A — "Lucky Deck."** A 20-card deck composed of unknown mix of
"high" (value 10) and "low" (value 1) cards. Student turns cards over one
at a time. After each card, choose BANK (score += card, lose card) or
RETURN (put card back, reshuffle top 3, skip turn). 10-turn game. 4 banks
available. Hidden quantity: deck composition (fraction of highs). Students
infer from observed draws. Optimal policy: estimate fraction; bank aggressively
if high proportion is high, conservatively if low. But — wait — RETURN plus
reshuffle isn't really a thing in a classroom, too fiddly. Rework: skip
RETURN, just BANK or PASS, and let hidden composition be the only learnable.

**DESIGNER_B — "Urn Walk."** A fixed urn (20 chips, unknown ratio of
white:black). Each turn, student draws one chip at random. White = +3,
black = -1. Student plays up to 10 turns and may STOP at any point. Budget:
must play at least 4 turns. Hidden quantity: white fraction. Across plays
the urn composition is re-drawn from a known prior (e.g., uniform on
{0.3, 0.5, 0.7}), so students learn the *meta* distribution. Optimal policy:
infer urn, then decide when to stop.

**PLAYTESTER.**
- *Lucky Deck (reworked):* 20-card deck, unknown high/low mix, 10-turn
  game, 4 banks. Classroom-friendly — just physical cards. Learnability:
  after each reveal, running proportion is visible. Optimal: bank anything
  if composition looks high-mostly (don't wait); bank only last chances if
  composition low. BUT with only 10 draws and 4 banks, the problem reduces
  to "threshold = value of banked card needed to justify using a bank slot."
  Threshold itself depends on estimate of composition. Works, but is it
  Bellman or is it bandit-stopping? Lean bandit.
- *Urn Walk:* Even more clearly a stopping problem. Urn composition
  inference + optimal stopping. No state transitions. Rejecting.

**STUDENT_VOICE.** Lucky Deck: "this is close to blackjack." Urn Walk:
"this is a stopping puzzle."

**MODERATOR synthesis.** Both are stopping problems with learnable reward
distributions; neither has the multi-state recursion structure we want. The
three candidates (Colored Row v3b, Mood Market v3, Mystery Gardener) stand.
Next round: refine debrief scripts — critical, since the debrief must link
observed learning to Bellman.

---

## Round 16

**MODERATOR.** Debrief scripts. Must connect (a) the hidden regularity you
learned, (b) the improved policy that followed, and (c) the Bellman
equation's inner expectation.

**DESIGNER_A — "Colored Row debrief v2."**
1. Histogram of play-1 scores (wide, many mid-low).
2. "What did you notice about the colors?" Elicit: "black ratings were
   usually high, white usually low."
3. "When you used that knowledge in play 2, what changed?" Elicit: "I
   skipped all whites without looking at the rating."
4. Formalize: you *learned* $\mathbb{E}[r \mid \text{color}]$ from data.
   You then *used* that expectation to pick actions. You were estimating
   $r(s, a)$ from history to feed into the Bellman recursion.
5. Write on board: $V(s) = \max_a [\, \mathbb{E}[r(s,a)] + \gamma V(s')\,]$.
6. The two halves: estimating expected reward (what you just did across
   plays) and maximizing cumulative expected reward given those estimates.
7. "An agent that doesn't learn expected rewards plays like a blind
   reservation-sampler. An agent that doesn't plan plays greedy. Both
   fail. Bellman + learning is the combination."
8. Histogram of play-2 scores. Note sharper, higher distribution.

**DESIGNER_B — "Mood Market debrief v2."**
1. Histogram.
2. "Did the high ratings come in bunches or randomly?" Elicit: "bunches —
   when I saw an 8, the next was often high too."
3. "What does that tell you about the environment?" Elicit: "there's a
   'mood' — a hidden state that persists."
4. "How did that change your strategy?" Elicit: "I waited until I saw a
   high rating, then I bought; if I saw a low rating, I stopped buying."
5. Formalize: you estimated a transition model $p(s' \mid s)$. You then
   used it to plan.
6. $V(s) = \max_a [r(s,a) + \gamma \mathbb{E}_{s' \sim p(\cdot\mid s,a)}[V(s')]]$.
7. Both halves of Bellman: transition model + value iteration.
8. Histogram of play-2 scores sharpens.

**PLAYTESTER.** Colored Row's debrief is cleaner (reward model only, no
transition model). Mood Market's debrief teaches a richer concept (transition
model + policy) but at higher cognitive cost. Depending on audience, either
wins.

**STUDENT_VOICE.** "Both debriefs felt like the equation was a *description*
of what I had already been doing, not a new rule imposed on me." — exactly
the reaction we want.

**MODERATOR synthesis.** Both debriefs land. Mystery Gardener debrief in
Round 17.

---

## Round 17

**MODERATOR.** Mystery Gardener debrief and final ranking discussion.

**DESIGNER_A — "Mystery Gardener debrief."**
1. Histogram.
2. "What did you notice about red vs blue plots?" Elicit: "blue worked
   more reliably."
3. "What did you do differently in play 2?" Elicit: "I focused on blue
   plots and mostly ignored red."
4. Formalize: you estimated a transition model $p(\text{stage advances} \mid
   \text{water}, \text{plot color})$. You then planned plant-water-harvest
   chains on the plot with higher success probability.
5. Bellman recursion: value of planting = 0 + $\gamma$ * expected value of
   seedling-state (which depends on how likely you'll be able to water it
   to ripeness, which depends on p).
6. $V(s) = \max_a [r(s,a) + \gamma \mathbb{E}_{s'}[V(s')]]$ — expectation is
   crucial because watering is stochastic.

**DESIGNER_B — "Ranking."**
1. Colored Row v3b — easiest to explain, learnability obvious (tally column),
   reliable behavior change between plays.
2. Mood Market v3 — richer (hidden Markov regime), teaches transition
   model learning, but needs more setup.
3. Mystery Gardener final — combines delayed reward from v1 Gardener with
   transition probability learning; most "RL textbook" flavor.

**PLAYTESTER.** The three cover the three kinds of learnable structure:
(i) reward function conditioned on observable feature (Colored Row),
(ii) hidden Markov regime (Mood Market), (iii) transition probability
(Mystery Gardener). For a 15-min classroom block, Colored Row is most
robust. For a richer 30-min block or mixed audience, Mood Market wins. For
a RL-specific course, Mystery Gardener wins because it's closest to the
standard MDP formulation.

**STUDENT_VOICE.** "If I had to teach one of these to my parents, Colored
Row. If I had to teach it to a friend who likes stock trading, Mood Market.
If I had to teach it to a CS major, Mystery Gardener."

**MODERATOR synthesis.** Final ranking: Colored Row v3b, Mood Market v3,
Mystery Gardener. Rounds 18-20: materials, time budgets, write-up.

---

## Round 18

**MODERATOR.** Materials and stress-tests for all three.

**DESIGNER_A — "Materials for Colored Row v3b."**
- One slide with rules (60s read).
- Whiteboard to write the color sequence (announced one-ahead).
- Per-student strip with 8 rows, 5 columns:
  [color | rating | EAT/SKIP | slots_left | running_score], plus a
  side-panel with per-color tally: [W: Σ_rating, count, mean |
  G: ... | B: ...].
- Instructor holds the (color, rating) list prepared secretly.
- Sticky notes for histogram.

**DESIGNER_B — "Materials for Mood Market v3 and Mystery Gardener."**
- Mood Market: one-slide rules; per-student strip of 16 rows, columns
  [step | rating | BUY/SKIP | buys_left | running_score | last_rating].
  Instructor's crib: pre-drawn 16-step sequence with mood labels.
- Mystery Gardener: one-slide rules; per-student 2-plot sheet with 6 rows,
  columns [turn | action | water_result (✓/✗) | R_stage | B_stage | budget
  | score]. Instructor flips an internal die (or uses a pre-generated
  result sequence) for watering success.

**PLAYTESTER.** All three pass materials audit. Colored Row is simplest;
Mood Market is medium; Mystery Gardener has a small extra tax (tracking
watering success per plot) but not overwhelming.

**STUDENT_VOICE.** "The per-color tally on Colored Row is the whole lesson —
I can literally see my model forming."

**MODERATOR synthesis.** Materials locked. Next round: timing.

---

## Round 19

**MODERATOR.** 15-minute session arcs for all three.

**DESIGNER_A — "Session arc: Colored Row v3b."**
- 0:00-0:60 — rules.
- 1:00-4:00 — play 1 (8 restaurants at ~22s each, includes color announcement
  and rating reveal).
- 4:00-5:00 — scoreboard histogram. Students also compute their per-color
  means from the tally column.
- 5:00-8:30 — debrief, derive Bellman.
- 8:30-11:30 — play 2 with new sequence (same color distributions).
- 11:30-12:30 — second histogram, compare to first.
- 12:30-15:00 — close (connect to expected-reward estimation and the
  inner-expectation half of Bellman).

**DESIGNER_B — "Session arcs for Mood Market and Mystery Gardener."**
- Mood Market: 1 min rules + 4 min play 1 (16 steps at ~15s each) + 1 min
  histogram + 3 min debrief + 4 min play 2 + 2 min close = 15 min.
- Mystery Gardener: 1 min rules + 4 min play 1 (6 turns × 40s) + 1 min
  histogram + 4 min debrief + 4 min play 2 + 1 min close = 15 min. Tight.

**PLAYTESTER.** All three fit 15 minutes. Colored Row has the most slack for
the debrief, which is where the Bellman math lives. That further supports
it as #1.

**STUDENT_VOICE.** "Two plays with a debrief in between is the whole
learning loop. I wouldn't do it any other way."

**MODERATOR synthesis.** All three session arcs work. Final writeup next.

---

## Round 20

**MODERATOR.** Final rankings and rationale for the top-3 document.

**DESIGNER_A — "Final rankings with one-line hidden regularity for each."**
1. **Colored Row v3b.** Hidden regularity: $\mathbb{E}[r \mid \text{color}]$
   is stationary and learnable from ~8 tagged samples across 2 plays.
2. **Mood Market v3.** Hidden regularity: rewards follow a 2-state Markov
   regime whose transition matrix is stationary; persistence of high
   ratings is discoverable within and across plays.
3. **Mystery Gardener.** Hidden regularity: watering success probability
   varies by plot color (stationary); learnable from 8-12 water attempts
   across 2-3 plays.

**DESIGNER_B — "Why Colored Row wins."**
- Learnability is explicit and namable ("I saw that black usually pays
  high").
- The per-color tally column is a *physical, visible representation of the
  learned model.*
- Dual-fail is visible: greedy eats the first 6 (wastes a slot on a probably-
  gray mediocre meal); blind reservation (wait for 9) wastes most of the
  slots. Color-aware policy dominates both.
- Bellman insight in debrief maps to expected-reward estimation, which is
  the cleaner half of the recursion to teach first.

**PLAYTESTER.** Agreed. Colored Row has the cleanest learnability-to-
behavior-change chain: play 1 builds model, play 2 exploits model, histogram
sharpens, debrief names the Bellman equation with $\mathbb{E}$-over-next-
states baked in.

**STUDENT_VOICE.** "In play 1 I thought it was random; by play 2 I knew
black was the target. That's the whole lesson."

**MODERATOR synthesis.** **Final v2 ranking: Colored Row v3b, Mood Market
v3, Mystery Gardener.** All three fix v1's flaw: they have stationary
hidden regularities that students learn across plays, and the optimal
policy requires BOTH past-informed prediction AND cumulative-future
maximization. The v2 design principle: **one hidden quantity per game, made
discoverable through a visible tagging column or a visible time-series
signal, with 2 plays to build-then-exploit the model.** v1's reservation-
sampling trap is avoided because the optimal threshold is now contingent
on the *learned* model, not a fixed one.

**End of 20 rounds.**
