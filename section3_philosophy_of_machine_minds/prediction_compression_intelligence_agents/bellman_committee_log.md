# Bellman Committee Log — 20 Rounds

**Pedagogical target.** Students must discover, by playing, that (1) the value of an action depends on the stream of *future* rewards it enables, (2) they must look at *past state/action history* to infer the best action *now*, and (3) optimal play maximizes *cumulative* future reward, not greedy immediate reward. Only after play does the instructor reveal $V(s) = \max_a [r(s,a) + \gamma V(s')]$.

---

## Round 1

**MODERATOR.** Goal in one line: a game where taking the shiny coin now quietly ruins your score ten moves later, and where remembering what was shown earlier tells you which path is shiny-but-cursed.

**DESIGNER_A — "Coin Corridor."** A 1x10 track drawn on the whiteboard. Student starts on cell 0, must reach cell 9 within 12 moves. Each cell has a face-up reward chip: values like +3, +1, -5, +10, 0, +2, +1, -20, +4, +15. On each turn, the student moves forward 1 *or* 2 cells, collecting the chip they land on. Greedy says "jump to the +10 on cell 3." But jumping +2 from cell 3 lands on the -20 on cell 5 (the parity is forced by the step pattern thereafter), while the slower path stair-steps into the +15 finish. State = (cell, moves_remaining). Action = {+1, +2}. Reward = chip value. Victory = highest total at cell 9.

**DESIGNER_B — "Memory Market."** Three face-down card stacks labeled A, B, C on the table. Each round (of 8), the instructor flips the top card of each stack face-up, showing a reward (-3 to +5). The student picks ONE stack to collect from. Here's the twist: each stack has a *hidden rule* — e.g., A's next reward is always the negative of the previous A reward; B's next is +2 if you skipped B last round else -2; C is IID random. Students must watch the full history to infer the rule for each stack, then predict which stack's *next* card will be best. Greedy picks whichever stack currently shows the biggest face-up number. State = history of flips and choices. Action = which stack. Reward = the hidden card under the face-up one, revealed after choice.

**PLAYTESTER.**
- *Coin Corridor:* With chips visible the game is a deterministic shortest-path problem. A sharp student will solve it on paper in 30 seconds by backward induction — which is *exactly* the Bellman insight, but it arrives via pen-and-paper planning rather than via felt failure. "Greedy fails" is visible but not viscerally *experienced*. Past doesn't matter because the state is fully observable.
- *Memory Market:* Past matters heavily — you literally cannot play without history. But "greedy fails because of future reward" is muddy; greedy fails here because of *partial observability*, which is a different lesson (POMDP, not vanilla Bellman).

**STUDENT_VOICE.** Coin Corridor: "this is just a math puzzle, why is it a game?" Memory Market: "how am I supposed to guess the rule? This feels like a psychology experiment."

**MODERATOR synthesis.** Both games miss in opposite ways. A has no hidden state, so looking back is trivial. B has hidden *rules* not hidden *value*, which teaches inference, not Bellman. Next round: find a game where the state is fully visible *but* the consequences of an action ripple forward in a way that isn't obvious from the current cell alone — so greedy is tempting, and looking at the path so far teaches you that you're in a particular *kind* of future.

---

## Round 2

**MODERATOR.** Restate: cumulative-future-reward must beat immediate-reward, and history must be informative for the *value* decision, not just for deducing hidden rules.

**DESIGNER_A — "Coin Corridor v2, with Fuel."** Same 1x10 track but now every step costs 1 fuel, and the student starts with 6 fuel. Some cells are gas stations (+3 fuel). Running out of fuel mid-track ends the game at current score. The +10 cell is reachable greedily but leaves you stranded before the +15 finish; the "boring" path hits two gas stations. Now greedy fails *because future reachability depends on resource state*. State = (cell, fuel). History matters because your remaining fuel is a function of everything you did.

**DESIGNER_B — "Restaurant Row."** Student walks past 7 restaurants in sequence (left to right on a whiteboard strip). At each restaurant they choose EAT or SKIP. Each restaurant shows a rating (1-10). Catch: you can EAT at most 3 times total, AND after you EAT you must SKIP the next two (digestion). The student wants to maximize summed rating of eaten meals. The last restaurant has the highest visible rating (a 10). Greedy students eat the first 8+ they see and arrive at the 10 unable to eat. Optimal students must *count eats used* and *remember how recently they ate*, then backward-induce. State = (position, eats_left, cooldown). Action = EAT/SKIP. Reward = rating if EAT legal.

**PLAYTESTER.**
- *Corridor v2:* Better. Fuel is a visible state variable, but tracking it across actions requires arithmetic the student does naturally — it feels like a game, not a proof. Greedy fails viscerally: "I grabbed the +10, now I can't reach the +15." Past matters because fuel = starting fuel minus moves.
- *Restaurant Row:* Excellent. The cooldown forces a "was the last one good enough to burn an eat-slot here?" judgment. With a known distribution of ratings (instructor reads them left-to-right with suspense), students feel the pull of greedy. The 10 at the end makes the trap visible in *retrospect*, after the instructor reveals the full sequence.

**STUDENT_VOICE.** Corridor v2: "I can see the board, can't I just plan ahead?" — YES, and that planning IS the Bellman computation. Good. Row: "can I peek at the whole row?" If yes, it's a planning puzzle; if no, it's a secretary problem. Need to decide.

**MODERATOR synthesis.** Restaurant Row is the stronger candidate but must commit to *hidden future*: ratings revealed one at a time. Then history is all you have. Next round, lean into Row, add a past-dependence that isn't just a counter.

---

## Round 3

**MODERATOR.** Row is promising if ratings are hidden until you arrive. Designers: push on hidden-future variants and also bring a dice-based alternative to check the design space.

**DESIGNER_A — "Restaurant Row v2 (sequential reveal)."** Same rules, but each rating is revealed only when you reach that restaurant. At that moment you must commit EAT/SKIP. 3 eat-slots, 2-step cooldown after EAT. Students don't know the future ratings but know the *distribution* (instructor says: ratings are drawn uniformly from 1-10, 7 restaurants). Now students must compute: "is this 8 good enough, or might a 9 come later?" The Bellman logic — value of EAT = current rating; value of SKIP = expected best I can still get with my remaining slots — becomes a felt necessity. Past matters: eats_left and cooldown are determined by history.

**DESIGNER_B — "Dice Climb."** Roll a d6 each turn for up to 10 turns. On each roll, choose BANK (add the roll to score, end turn, lose 1 of your 3 lives) or PUSH (continue rolling, score accumulates, but if you ever roll a 1, you lose all accumulated AND lose a life). Out of lives = game over, final score stands. State = (turn, lives, current_bank, accumulated_this_push). Action = BANK/PUSH. The greedy-fail: always banking low rolls squanders lives; always pushing guarantees ruin. The past (how many 1s have shown, how many lives left) shapes the optimal threshold.

**PLAYTESTER.**
- *Row v2:* Clean and cheap to run. Reveal one rating, students raise EAT or SKIP paddles (or stand up/sit down), instructor records, move on. A 7-restaurant game runs in 3 minutes. Greedy eaters burn slots on 6s and 7s, then watch a 9 and a 10 go past uneaten — the pain is the lesson. History matters through the (eats_left, cooldown) state. I think this lands.
- *Dice Climb:* Fun but it's a variance game. Half the class will attribute their loss to "bad rolls" and miss the Bellman insight. Also too close to Pig/Farkle, which students may already know.

**STUDENT_VOICE.** Row v2: "okay but WHY is expected-future-value the right object to compare against?" — that's exactly the question we want them asking. Dice Climb: "I lost because I rolled a 1 three times in a row, this is rigged."

**MODERATOR synthesis.** Row v2 is our current front-runner. Dice Climb loses because luck drowns the signal. Next round: stress-test Row v2 against a very different archetype — something spatial or adversarial — to see if we've truly found the best shape.

---

## Round 4

**MODERATOR.** Row v2 is the baseline. Designers, propose spatial/adversarial alternatives; we want to map the design space, not converge prematurely.

**DESIGNER_A — "Gridworld Treasure Hunt (paper version)."** 4x4 grid on graph paper. Treasure chests with values in some cells; one cell has a monster (-20). Student starts top-left, must reach bottom-right in exactly 8 moves (down or right only). Collects rewards along path. Some paths pass near monster (risk of -20 if a coin-flip goes against you when adjacent). State = (row, col, flips_used). Action = D or R. The "greedy" student takes the path with the single biggest visible chest; the optimal path is the one with the highest *expected* sum.

**DESIGNER_B — "The Negotiator's Ladder."** Student plays a 5-round negotiation. Each round the opponent (instructor) offers a split of $10. Accepting ends the game with that payoff. Rejecting means next round the pie shrinks by $2 AND the opponent's offer is drawn from a distribution that depends on what the student rejected last time (e.g., reject a fair offer => next offer is more generous; reject a stingy offer => next offer is stingier). The student must reason about cumulative value across rounds and how their own actions shift the future distribution. State = (round, last_rejected_offer). Action = ACCEPT/REJECT.

**PLAYTESTER.**
- *Gridworld:* With 8 moves down-right on a 4x4 grid there are only 70 paths, easily enumerated on paper. Greedy's failure is visible but "just don't go near the monster" is the student's takeaway, not "cumulative future reward beats immediate." Also: the randomness near the monster introduces variance complaints.
- *Negotiator's Ladder:* Interesting because actions *alter the future distribution*, which is pure Bellman. But the rule "your rejection changes the next offer" is a lot to absorb in the 60-second briefing. Students will freeze.

**STUDENT_VOICE.** Gridworld: "this is just path-finding." Negotiator: "wait, my rejection affects their future offers HOW? Explain again." — over budget.

**MODERATOR synthesis.** Neither beats Row v2 yet. Gridworld's spatial metaphor is nice but under-constrains the insight; Negotiator is too rule-heavy. Next round: keep searching, but also try a variant of Row where the *environment responds to you* (like Negotiator) but with simpler rules.

---

## Round 5

**MODERATOR.** Keep Row v2 in reserve. Explore variants with *environment response* but rule-minimal.

**DESIGNER_A — "Restaurant Row v3 (reactive chef)."** Row v2 with one added rule: each time you EAT, the next restaurant's rating is decreased by 2 (chef gets nervous). Each time you SKIP, the next restaurant's rating increases by 1 (chef tries harder). This introduces action-dependent transitions (classic MDP structure), but adds a 6-word rule to the brief: "eating lowers next; skipping raises next."

**DESIGNER_B — "Tollbooth Trek."** Whiteboard path with 8 segments. Each segment has a reward and a toll that must be paid from a budget. Budget starts at 10. Each turn, the student chooses FAST (collect reward, pay toll, advance 1) or SLOW (skip reward, pay no toll, advance 1). Some segments have huge rewards but huger tolls; budget dying means you forfeit all future rewards.

**PLAYTESTER.**
- *Row v3:* The reactive-chef rule is genuinely illuminating — students see that their action changes the *state they arrive in*, which is the heart of the Bellman equation. But the 2-for-1 asymmetry and running arithmetic taxes beginners. Could simplify to: EAT => next rating -2, SKIP => next rating unchanged.
- *Tollbooth:* Clean variant of Corridor v2 (fuel). Same lesson. Doesn't add much. Rejecting.

**STUDENT_VOICE.** Row v3 (asymmetric): "I'm doing arithmetic in my head AND remembering cooldown AND eats_left — too much."

**MODERATOR synthesis.** Row v3 simplified: EAT lowers next rating by 2, SKIP leaves it alone. Cooldown dropped (redundant with the reactive rule). Eats-left cap stays. Cleaner. Let's playtest this in Round 6 and start considering a second front-runner.

---

## Round 6

**MODERATOR.** Refine Row v3 simplified. Propose one new game that uses a totally different mechanic (cards, public scoreboard, team play) so we don't over-fit to the Row metaphor.

**DESIGNER_A — "Restaurant Row v3s."** 8 restaurants. Start by announcing rating distribution (1-10 uniform). Walk down the row. At each, rating revealed. EAT or SKIP. EAT => score += rating, next rating -= 2 (min 1). SKIP => next rating unchanged. 4 eat-slots. Score = sum of ratings eaten. Greedy eats early on 6s and 7s AND suppresses the next rating, compounding the trap.

**DESIGNER_B — "Relay of Secrets."** Team game for the class. Class split into 6-person teams. Each team has a 6-card deck (values 1,2,3,4,5,10). Cards are played one per round in sequence, face-up on the scoreboard. After all teams play, the team's score for that round is: value_played times (number_of_rounds_remaining + 1) if the card is strictly higher than the previous card played by that team; else value_played times 1. So saving the 10 for last is *bad* (no multiplier), but playing the 10 early and then being forced to play 1-5 also collapses the multiplier. Optimal play sequences cards so that values are monotonically increasing — but this means *not* playing the 10 when tempted.

**PLAYTESTER.**
- *Row v3s:* Crisp. Three state variables (position, rating_just_shown, eats_left). Greedy's failure is double-barreled: you burned a slot AND poisoned your next view. Running time ~3 min. I like it.
- *Relay:* Very clever. The monotone-increasing rule rewards "sacrifice now for multiplier later" — the Bellman principle incarnate. But the multiplier formula "value times (rounds_remaining + 1) if strictly higher else value times 1" is a mouthful. Students need a visible reference card.

**STUDENT_VOICE.** Row v3s: "okay, I get it, don't eat too early." Relay: "wait, when does the multiplier apply again?" Relay needs a worked example.

**MODERATOR synthesis.** Row v3s and Relay are both strong. They teach slightly different aspects: Row teaches "future reward depends on future opportunities I still have," Relay teaches "current action shapes the value of future actions." Keep both alive. Next round: add a third mechanic — something public-information / auction-based — to stress the field.

---

## Round 7

**MODERATOR.** Keep Row v3s and Relay. Explore auction/public-info games.

**DESIGNER_A — "Public Auction Path."** 5 items auctioned off in sequence. Each student has $10 to bid. Items have visible values 3, 7, 2, 8, 6 (revealed one at a time). Highest bidder wins the item (value added to score). Over-bidding wastes budget. The twist: unspent budget at the end is worthless. Greedy students blow budget early on the 7; optimal students save for the 8. History matters because everyone sees everyone else's bids, so you update on opponents' remaining budgets.

**DESIGNER_B — "Time-Bomb Tokens."** Each student starts with 5 tokens. Each round (of 6), the instructor announces a reward value for spending a token this round (revealed at round start). The student decides spend-1-token or hold. Catch: if you finish the game with ≥ 2 unspent tokens, all unspent tokens explode for -3 each. So you must spend roughly on time, but spending on low-reward rounds wastes the opportunity cost. Reward distribution known in advance. State = (round, tokens_left).

**PLAYTESTER.**
- *Auction:* Multi-agent, so there's noise from opponent strategy. Teaches game theory more than Bellman. Variance from classmates' decisions dilutes the signal. Rejecting — not our target lesson.
- *Time-Bomb:* Similar to Row v2 in spirit (slot allocation over sequential reveal) but without the reactive-environment feature of Row v3s. Cleaner than Row v3s but teaches less. Marginal.

**STUDENT_VOICE.** Auction: "everyone bid different things, I can't tell if my strategy was wrong." Time-Bomb: "nice, this is simple."

**MODERATOR synthesis.** Auction is killed — too multi-agent. Time-Bomb is viable but redundant with Row family. Front-runners remain Row v3s and Relay. Next round: torture-test Row v3s with bigger class sizes and see how it scales; also give Relay one more simplification pass.

---

## Round 8

**MODERATOR.** Scale-test Row v3s for a class of 40; simplify Relay.

**DESIGNER_A — "Row v3s, class version."** Every student plays in parallel with a shared rating sequence revealed by the instructor. Each student marks EAT/SKIP on a paper strip at each reveal. At end, students compute their own score using the rule (which is printed at the top of the strip). Instructor then shows the score distribution on the board — bimodal if theory holds (greedy vs far-sighted). Plays in 4 minutes even with 40 students because it's synchronous.

**DESIGNER_B — "Relay Lite."** 5-card deck per team (values 1, 3, 5, 7, 10). Rule simplified: "if the card you play is higher than any card you've played so far, it scores its face value times the number of cards you've played (including this one). Otherwise it scores 0." So playing 1, 3, 5, 7, 10 in order yields 1 + 6 + 15 + 28 + 50 = 100. Playing 10 first yields 10 and everything after is 0 = 10. The tension: every round you're tempted to play your best card now, but that zeros out the next four. State = (cards_in_hand, cards_played_history). The classroom version runs as teams; within a team students must agree on which card to play next.

**PLAYTESTER.**
- *Row v3s class:* Scales beautifully. The bimodal score histogram on the board is a *visible argument* for the Bellman principle — the instructor doesn't need to assert it, the distribution shows it. This is very strong.
- *Relay Lite:* Now trivially optimal (sort ascending). Over-simplified. Need to add randomness or hidden info.

**STUDENT_VOICE.** Row v3s class: "seeing the distribution was the clincher — I was at the low peak and the high peak kids figured something out." Relay Lite: "just play smallest first, right?" Yes — no insight.

**MODERATOR synthesis.** Relay Lite was over-simplified. Revise to restore tension. Row v3s class-version is our strongest candidate. Next round: relay revision plus a fresh contender.

---

## Round 9

**MODERATOR.** Revive Relay with tension. New contender welcome.

**DESIGNER_A — "Relay Lite v2."** Same as Lite but now each team's hand has one WILD card whose value is drawn randomly (1-10) only when played. Further, after each card played, one card is stolen from your hand by the "market" (instructor) — the stolen card is the one with the highest remaining value. So if you save your 10, it gets stolen. You must play high cards before they're stolen, but also earlier plays score less. State = (hand, history, round). The tension: "play the 10 now or risk losing it" versus "save it for the multiplier."

**DESIGNER_B — "Shopping Spree."** $20 budget, a list of 8 items revealed in sequence with prices and "joy" values. Buy or skip. Budget can go negative by ≤5 but triggers -10 penalty. Some items are necessities (if not bought, -5 at end). Greedy buys the first shiny thing; optimal students track budget and weigh against future reveals.

**PLAYTESTER.**
- *Relay Lite v2:* The stealing rule is clever but adds cognitive load. Students spend mental cycles computing "which card will be stolen next?" rather than feeling the Bellman tradeoff. Also the WILD card randomness dilutes the signal.
- *Shopping Spree:* A reskin of Row v3s. Same lesson, different paint. Doesn't teach anything new.

**STUDENT_VOICE.** Relay v2: "too many rules." Shopping: "this is just Row with prices."

**MODERATOR synthesis.** Relay is drifting; its last clean form was Lite, which was trivial. Relay may be structurally unable to match Row on simplicity. Keep Row v3s as front-runner. Next round: hunt for a truly different second candidate — perhaps a *movement* game where the agent's position determines its future options asymmetrically.

---

## Round 10 (midpoint check)

**MODERATOR.** Halfway. Current leader: Row v3s. Gaps: we haven't nailed a *movement* game that survives playtesting. Try again.

**DESIGNER_A — "Two-Door Dungeon."** Student moves through a 6-room dungeon. Each room has two doors, each labeled with the reward you get *upon entering the next room*. But each door also sets a flag (red or blue) on the current room. The final room's payout = +20 if you entered through a door that matches the PARITY of red flags in the rooms you passed through; otherwise 0. Greedy students pick the biggest reward at each door ignoring flags; optimal students plan the parity. State = (room, red_flag_count_so_far). History is literally the red_flag_count.

**DESIGNER_B — "The Hiker's Dilemma."** Student hikes a linear trail of 10 checkpoints. At each checkpoint they choose REST or MARCH. REST gives +2 energy. MARCH spends 1 energy and collects the checkpoint's reward (revealed on arrival, drawn 1-10). If energy hits 0, the student is stuck and earns 0 thereafter. Start energy = 3. Must reach checkpoint 10 (forced end). Greedy marches on every reveal; optimal rests at low-reward checkpoints to bank energy for future high rewards.

**PLAYTESTER.**
- *Two-Door Dungeon:* The parity rule is cute but teaches a specific-planning skill, not Bellman. Greedy fails for a reason other than cumulative future reward (it fails because of a boundary condition). Rejecting.
- *Hiker:* Very clean. Energy is visible state. Future rewards are hidden but distribution known. The rest-to-march tradeoff is pure Bellman: value of REST = expected future gain from +2 energy. History matters: (position, energy) is all you need, but energy IS the path integral of your actions.

**STUDENT_VOICE.** Dungeon: "red flag parity? what?" Hiker: "this feels like a real decision, not a puzzle."

**MODERATOR synthesis.** Hiker is promising — it's Row-like but with a resource that accumulates/depletes rather than a slot counter. Keep Row v3s as leader, Hiker as second candidate. Next round: comparative playtest.

---

## Round 11

**MODERATOR.** Head-to-head: Row v3s vs Hiker. Designers, each present a playtest focused on whether the Bellman aha-moment lands.

**DESIGNER_A — "Row v3s playtest focus."** Scripted rating sequence: [5, 7, 6, 4, 9, 3, 8, 10], 4 eats allowed, EAT lowers next by 2 min 1. Greedy eats at 5, 7, 6, 4 => score 22, arrives at 9 with 0 slots. Optimal skips 5, eats at 7 (next becomes 4), skips 4, eats at 9 (next becomes 1), skips 1, eats at 8 (next becomes 6), arrives at 10 eating it => 7+9+8+10 = 34. Wait — 4 eats used: 7, 9, 8, 10 = 34. Greedy: 22. Visible 12-point gap.

Actually let me recheck: greedy eats 5 (now next=5), eats 5 (now next=4), eats 4 (now next=2), eats 2 => 16. Even worse. Optimal 34. 18-point gap. Wonderful.

**DESIGNER_B — "Hiker playtest focus."** Rating sequence [3, 8, 2, 9, 1, 10, 4, 7, 6, 5]. Start energy 3. Greedy marches all => gets 3, 8, 2 then stuck => score 13. Optimal rests at 3, marches 8 (energy 2), rests at 2 (energy 4), marches 9 (3), rests at 1 (5), marches 10 (4), rests at 4 (6), marches 7 (5), marches 6 (4), marches 5 (3) — counts 5 marches = rewards 8+9+10+7+6+5 = 45? Let me recount. Actually energy = 3, 10 checkpoints, each MARCH costs 1 and collects, each REST gives +2 but skips collection. You want to collect the biggest 5-8 rewards your energy budget allows given resting opportunities. Bellman-optimal is a dynamic programming problem. Huge gap between greedy and optimal.

**PLAYTESTER.**
- *Row v3s:* 18-point gap. The gap is caused by a combination of slot-rationing AND the reactive-chef effect. Students feel both.
- *Hiker:* Roughly 30-point gap. BUT Hiker has a subtle bug: energy-budget planning requires integer knapsack reasoning, which is hard to feel viscerally in 5 minutes. Students report "I ran out of energy" rather than "I was greedy." The failure mode is attributed to *resource mismanagement*, not short-sighted value estimation.

**STUDENT_VOICE.** Row: "I ate too early — the chef effect killed me." Hiker: "I didn't pace myself — felt like a survival game."

**MODERATOR synthesis.** Both work, but Row gets students to say *exactly* the right thing: "I ate too early." That framing is the Bellman framing — value of eating-now was lower than value of eating-later. Hiker's framing is "I ran out of energy," which is resource management (still MDP, but the insight is muddier). Row v3s remains #1. Hiker is solid #2. Next round: seek a third contender that's distinct from both.

---

## Round 12

**MODERATOR.** Find a third contender with a different feel.

**DESIGNER_A — "Ghost Writer."** Student is told: "I (the instructor) have written a hidden sequence of 6 numbers. Each number is either +5 or -3. You can peek at up to 2 numbers before committing to a stopping rule: after peeking (optionally), you declare 'stop at position K' for some K in 1-6. Your score = sum of the first K numbers." The trick: the sequence has a *pattern* — e.g., after two -3s in a row, the next is +5 with high probability. Peeks at position 1 and 4 give different info value. Students must decide which peeks to use (exploration) and when to stop (exploitation).

**DESIGNER_B — "The Patient Gardener."** Student has a 4x1 row of "plots." Each turn (8 turns), they choose PLANT (cost 2, plot becomes seedling), WATER (cost 1, seedling becomes flower OR flower becomes ripe — one step up), or HARVEST (gain value based on stage: seedling=0, flower=3, ripe=8, overripe=-5; plot resets). Budget of 15. Greedy plants and harvests immediately for tiny gains; optimal plants early, waters twice, harvests ripe, repeats. The ripening transition is deterministic once the rules are shown. State = (turn, budget, per-plot stage). History matters because each plot's stage is the integral of your past actions on it.

**PLAYTESTER.**
- *Ghost Writer:* Teaches exploration/exploitation (bandits, information value), which is RL-adjacent but not Bellman's recursive value. Also the peek mechanic complicates the brief. Rejecting for our specific target.
- *Gardener:* Multi-plot parallelism adds rich state but also complexity. Running it in 5 minutes with 4 plots and 8 turns is tight. BUT the delayed-reward structure (plant => water => water => harvest) is a crystal-clear Bellman arc. You literally feel that "planting now" has value only via the harvest four turns later.

**STUDENT_VOICE.** Ghost Writer: "peek? stop rule? is this a game show?" Gardener: "oh, I get it — planting is an investment."

**MODERATOR synthesis.** Gardener is a strong third. It teaches Bellman via the investment metaphor, which is intuitive for any student (especially managers, but also engineering undergrads). Simplify to 2 plots and 6 turns for the classroom version. Next round: refine Gardener and compare all three.

---

## Round 13

**MODERATOR.** Refine Gardener; then all three compete.

**DESIGNER_A — "Patient Gardener v2."** 2 plots, 6 turns, budget 8. Plant cost 2, Water cost 1 (advances stage), Harvest free. Stages: empty -> seedling -> flower -> ripe -> overripe -> (auto-resets to empty for -2 penalty). Harvest yields 0/3/8/-3 for seedling/flower/ripe/overripe. Goal: max score minus budget spent. Rules on a 3-line reference card.

**DESIGNER_B — "Row v3s final form."** 8 restaurants, 4 eats, EAT lowers next by 2 (min 1). Already locked in. Present again for comparison.

**PLAYTESTER.**
Side-by-side with a simulated class of 20:
- *Row v3s:* 4-minute run. 15 of 20 play greedy the first time and score ~20. Debrief reveals the reactive-chef dynamic. On second play with the same rule but a new rating sequence, 17 of 20 adopt a forward-looking strategy — average score jumps to 32. The *behavior change between play 1 and play 2 is the pedagogical gold.*
- *Gardener v2:* 5-minute run. First play: students mostly harvest at flower stage (3 points each) to be safe, score ~15. Second play: some attempt ripe-harvest (8 points each), but overripe risk trips up the timid. Roughly half the class internalizes delayed-gratification; the other half retreats to flower-harvesting. Mixed outcome.
- *Hiker:* 4-minute run. First play, 12 of 20 run out of energy early. Second play, most correctly ration energy but complain the game felt "about managing health, not about rewards."

**STUDENT_VOICE.** Row: "I can't believe how differently I played the second time." Gardener: "I wanted to wait but I was scared of overripe." Hiker: "this was a survival game."

**MODERATOR synthesis.** Row's second-play behavior change is the cleanest signal we've seen. Gardener is pedagogically sound but the risk-aversion tail dilutes the signal. Hiker frames the lesson wrong. Current ranking: Row v3s #1, Gardener v2 #2, Hiker #3. Let's push to strengthen Gardener in Round 14 or displace Hiker.

---

## Round 14

**MODERATOR.** Strengthen Gardener or replace Hiker.

**DESIGNER_A — "Patient Gardener v3."** Remove overripe penalty; auto-harvest at ripe with full value if not harvested. Now the only risk is: did you water enough times to reach ripe? Budget tighter (6). This removes the risk-aversion drag: students no longer fear waiting too long. State space shrinks. The delayed-investment lesson survives without the fear tax.

**DESIGNER_B — "Quest Board."** 5 quests pinned to a board, each with a cost (time in turns), a reward (gold), and a precondition (e.g., "must have completed Quest 2"). Student has 8 turns. Choose one quest per turn to start; once started it occupies you for the cost. The student must plan dependency order + time budget. Greedy picks the highest gold/time ratio first; optimal respects preconditions and plans backward from the biggest final quest.

**PLAYTESTER.**
- *Gardener v3:* Crisp. Removing overripe saved the design. Students now play with confidence; the gap between water-and-harvest-at-flower-each-turn and plant-water-water-harvest-ripe is visible. Second-play behavior change matches Row's.
- *Quest Board:* Teaches planning-under-constraints, not Bellman's recursive value. Precondition logic swamps value reasoning. Rejecting.

**STUDENT_VOICE.** Gardener v3: "okay, simple now, and I see why I should wait." Quest: "there are arrows pointing everywhere, I'm lost."

**MODERATOR synthesis.** Gardener v3 is tight. New ranking: Row v3s, Gardener v3, then Hiker (still viable but weakest). Let's see if there's a fourth archetype we haven't explored: maybe a *sequential move* game on a 1D track with a *hidden* future that the student must *predict from history*.

---

## Round 15

**MODERATOR.** One more archetype: predictive 1D track.

**DESIGNER_A — "Weather Walker."** Student walks a 10-day trip. Each day the weather is one of {sun, rain} and the student collects a reward: sun+5 if outside, rain-3 if outside, or +1 if stays inside. Weather has a hidden Markov rule: sun => sun with prob 0.7 tomorrow, rain => rain with prob 0.8 tomorrow. The first 2 days' weather is announced. After that, student must guess each day's weather (based on yesterday's) and choose OUTSIDE/INSIDE before seeing today's weather. State = (day, yesterday's weather, wealth). The "optimal strategy" is: after sun-day, go outside (0.7 chance of sun); after rain-day, stay inside (0.8 chance of rain). But the student must *infer the transition probabilities from observed history*.

**DESIGNER_B — "Color Coder."** Sequence of colored tokens revealed one at a time (6 tokens total). Each round, student predicts the next token's color, then the real token is revealed. Correct prediction = +2, wrong = 0. Tokens follow a hidden rule (e.g., "the next color is always different from the last two"). Student must induce the rule from history.

**PLAYTESTER.**
- *Weather Walker:* Mixes prediction (learning transition probs) with Bellman. The Bellman part (value of going outside given belief about tomorrow's weather) is real but obscured by the probability-estimation part. Two lessons in one game — too much.
- *Color Coder:* Pure prediction/induction. Not Bellman at all. Rejecting.

**STUDENT_VOICE.** Weather: "I'm doing statistics AND planning, overwhelming." Color: "is this a pattern-recognition IQ test?"

**MODERATOR synthesis.** Predictive track archetype doesn't match our target. Bellman needs transitions known (or near-known) so the decision is about value, not about belief. Current top three stable: Row v3s, Gardener v3, Hiker. Next round: final refinements and debrief-script drafting for each.

---

## Round 16

**MODERATOR.** Debrief scripts. How does the instructor walk from "you just played this" to $V(s) = \max_a [r(s,a) + \gamma V(s')]$?

**DESIGNER_A — "Row v3s debrief script."**
1. Show score distribution on board. Note bimodality (greedy cluster vs far-sighted cluster).
2. Ask: "Why did some of you score 34 and others 16?"
3. Elicit: "eating early burned slots and lowered the next rating."
4. Write on board: "value of eating at position $t$ = rating_now + effect_on_future."
5. Formalize: let $V(s)$ = best score I can still get from state $s = (position, eats\_left, next\_rating)$. Then $V(s) = \max\{ \text{EAT: } r_t + V(s') , \text{SKIP: } 0 + V(s'') \}$.
6. Note: $s'$ and $s''$ differ because action changes state — that's the transition.
7. Generalize: $V(s) = \max_a [ r(s,a) + \gamma V(s') ]$.
8. Name it: the Bellman equation.

**DESIGNER_B — "Gardener v3 debrief script."**
1. Score distribution.
2. "Why did harvest-at-flower players score lower than plant-water-water-ripe players?"
3. Elicit: "planting has no immediate reward; its value only shows up at harvest."
4. Write: "value of planting = 0 + (value of next state with a seedling)."
5. Recurse: "value of watering a seedling = 0 + (value of next state with a flower)."
6. Chain: "value of eventual harvest flows backward through the watering-and-planting chain."
7. Formalize: $V(s) = \max_a [r(s,a) + \gamma V(s')]$.
8. Name the equation; name the principle (optimality).

**PLAYTESTER.**
Both debriefs are strong. Row's debrief hits the "history matters" point harder because `eats_left` and `next_rating` are explicit state variables. Gardener's debrief hits the "delayed reward" point harder because the harvest is far from the plant action. Row's lesson is more about *opportunity cost*; Gardener's is more about *investment*. Both are Bellman-legal.

**STUDENT_VOICE.** Row debrief: "the equation matches exactly what I was computing — nice." Gardener debrief: "I wasn't computing; I was acting on intuition. The equation formalizes my gut."

**MODERATOR synthesis.** Both debriefs work. Row's is more mechanistic (students computed values), Gardener's is more narrative (students acted and see the math after). Depends on class. For CS/ML students, Row is crisper. For mixed audiences, Gardener is warmer. Keep both. Hiker debrief draft in Round 17.

---

## Round 17

**MODERATOR.** Hiker debrief; then consider if Hiker remains in top 3 or is displaced.

**DESIGNER_A — "Hiker debrief script."**
1. Score distribution — typically wider than Row/Gardener.
2. "Why did some of you stall at checkpoint 3?"
3. Elicit: "I marched on every reveal and ran out."
4. Write: "value of resting = 0 now + (future reward I can still grab because I have +2 energy)."
5. Formalize $V(s)$ over state $(position, energy)$.
6. Bellman equation.

**DESIGNER_B — "Alternative: revive Relay?"** Propose a clean Relay: 5 cards per team (1, 3, 5, 7, 10). Play one per round. The card's score is face_value × (rounds_remaining + 1) but only if it's higher than every previously played card; else face_value × 0.5. This keeps the monotone-increasing reward and the investment-now-for-multiplier-later tension. Simpler than earlier Relay versions.

**PLAYTESTER.**
- *Hiker debrief:* Works, but students consistently frame the lesson as "ration resources" rather than "compare cumulative values." Debrief has to re-frame their experience. That's a mild pedagogical cost.
- *Relay v3:* Cleaner than past Relay iterations. But the 0.5 multiplier for non-monotone plays is still a rule. With only 5 rounds, the game is over fast, and optimal play is sort ascending — same over-determination problem.

**STUDENT_VOICE.** Hiker debrief: "so I should think of resting as an investment in future energy that enables future rewards? Got it." Relay v3: "okay, I just play low to high." Over-determined.

**MODERATOR synthesis.** Hiker stays in top 3 — it teaches a genuine Bellman lesson, even if the framing is slightly off. Relay does not recover; it's either too complex or too trivial. Final top 3: **Row v3s, Gardener v3, Hiker.** Rounds 18-20: stress-test, finalize materials, check time budgets.

---

## Round 18

**MODERATOR.** Materials check. Each game must be playable with whiteboard/paper/one-slide.

**DESIGNER_A — "Materials audit."**
- *Row v3s:* One slide with the rules. A whiteboard to write the rating sequence (revealed one at a time). Each student has a paper strip with 8 boxes marked "rating / EAT-SKIP / score." That's it. 4-minute play, 3-minute debrief.
- *Gardener v3:* One slide with the rules. Each student has a 2-plot sheet with 6 rows (turns). Each row has columns: action, plot1_stage, plot2_stage, budget, score. Pencil. 5-minute play, 4-minute debrief.
- *Hiker:* One slide. Each student has a strip with 10 boxes. Columns: reward_revealed, REST/MARCH, energy, score. 4-minute play, 3-minute debrief.

All pass.

**DESIGNER_B — "Scoreboard design."** For all three: after play, each student writes their final score on a sticky note and puts it on the board in a histogram. Bimodality (or wide spread) = pedagogical payload. Instructor uses the histogram to open the debrief.

**PLAYTESTER.** Tested all three materials in a dry run. Row and Hiker strips are simplest (single-row). Gardener's 2-plot sheet is one more column but students handle it fine. Sticky-note histogram is a reliable engagement tool.

**STUDENT_VOICE.** "The histogram made me want to know what the high-scorers did differently — that's when I learned the most."

**MODERATOR synthesis.** Materials are ready. Next round: timing stress-test with a full imagined class session.

---

## Round 19

**MODERATOR.** Full 15-minute session run-through.

**DESIGNER_A — "Full session for Row v3s."**
- 0:00-0:60 — rules (instructor reads, shows slide).
- 1:00-5:00 — play 1 (8 reveals, one every ~25s for student to decide).
- 5:00-6:00 — scoreboard.
- 6:00-9:00 — debrief of play 1, derive Bellman recursion.
- 9:00-13:00 — play 2 with new sequence. Most students now play far-sighted.
- 13:00-14:00 — second scoreboard.
- 14:00-15:00 — "look how the distribution shifted — this is what learning $V(s)$ looks like."

Flawless 15-minute arc.

**DESIGNER_B — "Full session for Gardener v3."**
- 0:00-1:00 — rules.
- 1:00-6:00 — play 1.
- 6:00-7:00 — scoreboard.
- 7:00-10:30 — debrief (slightly longer; investment metaphor needs unpacking).
- 10:30-14:30 — play 2.
- 14:30-15:00 — closing.

14-minute arc. Tight but works.

**PLAYTESTER.** Both session plans are realistic. Row has 1 minute of slack; Gardener is tight. Hiker similar to Row, 15 minutes clean.

**STUDENT_VOICE.** "Playing twice — that's the key. The second play is where I proved to myself I had the lesson."

**MODERATOR synthesis.** All three fit a 15-minute block with two plays. Final round: write it up.

---

## Round 20

**MODERATOR.** Final ranking and rationale.

**DESIGNER_A — "Final ranking."**
1. **Row v3s (Restaurant Row, reactive chef).** Cleanest Bellman lesson. Explicit state variables (position, eats_left, next_rating). Greedy fails in a way students *name correctly* ("I ate too early"). Bimodal scoreboard. Perfect for CS/ML beginners.
2. **Gardener v3.** Best for mixed audiences including non-CS. Investment metaphor is universally intuitive. Delayed-reward chain is a direct Bellman backup. Slightly more complex state per plot.
3. **Hiker.** Solid backup. Resource-integration teaches a real MDP lesson but with "ration resources" framing that the instructor must re-frame to "cumulative future reward."

**DESIGNER_B — "Agreement with some nuances."** I'd swap Gardener and Hiker for a CS-heavy audience (Hiker is closer to the textbook frozen-lake-style gridworld), but keep the ranking for mixed audiences. Agreed on Row as #1 across all audiences.

**PLAYTESTER.** Row v3s had the best second-play behavior change, which I consider the gold standard for "they learned it." Gardener's investment frame was memorable. Hiker teaches the lesson but with an off-angle framing.

**STUDENT_VOICE.** "Row felt like a game; Gardener felt like a parable; Hiker felt like a survival scenario. Game-feel helps retention."

**MODERATOR synthesis.** **Final ranking: Row v3s, Gardener v3, Hiker.** All three are being written up in `bellman_top3.md`. Key design principle we learned: the failure mode must be *namable in the student's own words* ("I ate too early" / "I didn't invest" / "I was too greedy"), and that phrase must map cleanly onto the Bellman equation at debrief. Games where students blamed luck, complexity, or resources failed. Games where they blamed their own greed succeeded.

**End of 20 rounds.**
