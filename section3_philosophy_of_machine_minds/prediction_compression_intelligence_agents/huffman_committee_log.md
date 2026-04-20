# Huffman Committee Log — 20 Rounds

Goal: design a 5-minute classroom toy example for teaching Huffman coding to
an audience with no information-theory background (basic arithmetic only).
The tree must be non-trivial (asymmetric depth, not 2–3 symbols).

Three roles per round: **Creator**, **Verifier** (runs Huffman by hand),
**Critic** (confused listener, 1–3 sharp complaints).

---

## Round 1

**Creator.** Candidate: the word **BANANA** (6 letters, 3 symbols).
Symbols + frequencies: A=3, N=2, B=1. Hook: "Bananas are mostly A's — so the
letter A should get the shortest code."

**Verifier.**
Merges:
- Start: A=3, N=2, B=1.
- Pick smallest two: N(2)+B(1) = NB(3). Pool: A=3, NB=3.
- Pick both remaining: A+NB = 6. Done.

Tree:
```
       (6)
      /   \
     A     (3)
          /  \
         N    B
```
Code table: A=0, N=10, B=11.
Encoded bits: 3·1 + 2·2 + 1·2 = 3 + 4 + 2 = 9 bits.
Fixed-length (2 bits/symbol × 6 symbols) = 12 bits. Saving: 3 bits.
Time estimate: setup 30s, merges 30s, tree 45s, code table 30s, savings 30s =
2m 45s. Fits easily.

**Critic.** Complaints:
1. Only three symbols — the tree is so shallow it looks like a trivial
   "binary decision"; the audience doesn't see the thing the lecture
   is selling (deep asymmetric codes).
2. 9 vs 12 is a weak payoff — 25% saving feels like rounding noise, not a
   lightbulb.
3. "Bananas are mostly A's" is cute but the point gets lost because there
   are too few symbols for frequency to even matter.

---

## Round 2

**Creator.** Incorporating the critic: more symbols. Candidate: the phrase
**MISSISSIPPI** (11 letters, 4 symbols). Symbols + counts: I=4, S=4, P=2,
M=1. Hook: "Which letter hurts the most if you lose it? Spend fewer bits on
the ones you see again and again."

**Verifier.**
Merges:
- Start: I=4, S=4, P=2, M=1.
- Smallest two: M(1)+P(2) = MP(3). Pool: I=4, S=4, MP=3.
- Smallest two: MP(3)+I(4) = MPI(7). Pool: S=4, MPI=7.
- Last: S(4)+MPI(7) = 11. Done.

Tree:
```
          (11)
         /    \
        S     (7)
             /   \
            I    (3)
                /  \
               M    P
```
Code table: S=0, I=10, M=110, P=111.
Encoded bits: 4·1 (S) + 4·2 (I) + 1·3 (M) + 2·3 (P) = 4+8+3+6 = 21 bits.
Fixed-length: 2 bits × 11 symbols = 22 bits. Saving: 1 bit.
Time: setup 30s, merges 45s, tree 60s, table 30s, savings 30s = 3m 15s.

**Critic.** Complaints:
1. Saving 1 bit out of 22 is *comic*. I expected compression to matter and
   it looks like it does nothing.
2. Two symbols tied at 4 — which do I merge first? Teacher glosses over it
   and I'm already confused.
3. The tree is prettier than Round 1 but the punchline is a dud.

---

## Round 3

**Creator.** The critic is right: I need a distribution where the savings are
visible, not 1 bit out of 22. Rule of thumb I'll adopt — one very frequent
symbol that dominates. Candidate: morse-ish distribution on letters of
**"TO BE OR NOT TO BE"** (spaces removed = 13 letters). Counts: O=4, T=4,
B=2, E=2, R=1, N=1. 6 symbols.
Hook: "Shakespeare already knew some letters cost more than others."

**Verifier.**
Merges (break ties by arbitrary but stated rule: smaller alphabetical first):
- Pool: O=4, T=4, B=2, E=2, R=1, N=1.
- R(1)+N(1) = RN(2). Pool: O=4, T=4, B=2, E=2, RN=2.
- B(2)+E(2) = BE(4). Pool: O=4, T=4, RN=2, BE=4.
  Wait — RN(2) is smaller than BE(4). Redo: smallest two are RN(2)+E(2) or
  RN(2)+B(2). Pick RN(2)+B(2) = RNB(4). Pool: O=4, T=4, E=2, RNB=4.
- Now smallest is E=2. Next smallest: O=4 (tie with T and RNB). E(2)+O(4) =
  EO(6). Pool: T=4, RNB=4, EO=6.
- T(4)+RNB(4) = TRNB(8). Pool: EO=6, TRNB=8.
- EO(6)+TRNB(8) = 14. Done.

Tree:
```
              (14)
             /    \
           (6)    (8)
          /  \   /   \
         E   O  T   (4)
                   /   \
                 (2)    B
                /  \
               R    N
```
Code table: E=00, O=01, T=10, B=111, R=1100, N=1101.
Encoded bits: 2·2 (E) + 4·2 (O) + 4·2 (T) + 2·3 (B) + 1·4 (R) + 1·4 (N)
= 4+8+8+6+4+4 = 34.
Fixed-length: ceil(log2 6)=3 bits × 13 symbols = 39 bits. Saving: 5 bits (≈13%).
Time: setup 45s, merges 90s, tree 75s, table 45s, savings 30s = 4m 45s.

**Critic.** Complaints:
1. The merges got confusing — three ties at value 4 and the teacher had to
   stop and say "pick arbitrarily, but consistently." That's exactly the
   kind of footnote that breaks a 5-minute flow.
2. I had to count letters in "TO BE OR NOT TO BE" myself and I got
   different numbers. Confusing setup.
3. Savings 34 vs 39 is better than Round 2 but still feels small. I want
   to SEE compression happen, not hear "we saved 5 bits."

---

## Round 4

**Creator.** Fix the tie problem: choose counts that are *all distinct*.
Fix the payoff problem: make one symbol dominant. Fix the setup problem:
use a stated scenario, not a quoted phrase.

Candidate: "What did the class have for lunch?" Tally from a survey of 20
students. Items: Pizza=10, Salad=4, Burger=3, Sushi=2, Curry=1. 5 symbols,
all distinct counts, one dominant. Hook: "Half the class had pizza — pizza
should get the shortest signal."

**Verifier.**
Merges:
- Pool: P=10, Sa=4, B=3, Su=2, C=1.
- Smallest two: C(1)+Su(2) = CSu(3). Pool: P=10, Sa=4, B=3, CSu=3.
- Smallest two: B(3)+CSu(3) = BCSu(6). Pool: P=10, Sa=4, BCSu=6.
- Smallest two: Sa(4)+BCSu(6) = SaBCSu(10). Pool: P=10, SaBCSu=10.
- Last: P(10)+SaBCSu(10) = 20. Done.

Tree:
```
                (20)
               /    \
              P     (10)
                   /    \
                  Sa    (6)
                       /   \
                      B    (3)
                          /  \
                         C   Su
```
Code table: P=0, Sa=10, B=110, C=1110, Su=1111.
Encoded bits: 10·1 + 4·2 + 3·3 + 1·4 + 2·4 = 10+8+9+4+8 = 39.
Fixed-length: ceil(log2 5)=3 bits × 20 = 60 bits. Saving: 21 bits (35%).
Time: setup 45s (story + tally), merges 60s, tree 75s, table 30s, savings 30s
= 4m 00s.

**Critic.** Complaints:
1. Finally a dramatic saving (39 vs 60). I get it.
2. Five merges with distinct counts read cleanly. No ties.
3. BUT — four symbols end up with ugly long codes (110, 1110, 1111) and
   the "Curry vs Sushi" split at the bottom is doing nothing for the
   pedagogy; they both have 4-bit codes. A truly asymmetric tree would
   have one symbol at depth 4 and the rest ramping up gradually, which
   this tree actually does — so this might be fine. Tiny complaint: 20
   bars in the survey is borderline tedious to draw on the board.

---

## Round 5

**Creator.** Round 4 is the strongest so far. Critic's only real objection
is draw-tedium: 20 tally marks eats time. Can I cut the total count while
keeping the asymmetry?

Candidate: same story, smaller tally. Pizza=8, Salad=3, Burger=2, Sushi=1,
Curry=1. Total 15. Hook unchanged.

**Verifier.**
Merges:
- Pool: P=8, Sa=3, B=2, Su=1, C=1.
- C(1)+Su(1) = CSu(2). Pool: P=8, Sa=3, B=2, CSu=2.
- B(2)+CSu(2) = BCSu(4). Pool: P=8, Sa=3, BCSu=4.
- Sa(3)+BCSu(4) = SaBCSu(7). Pool: P=8, SaBCSu=7.
- Last: P(8)+SaBCSu(7) = 15. Done.

Tree:
```
              (15)
             /    \
            P     (7)
                 /   \
                Sa   (4)
                    /  \
                   B  (2)
                      / \
                     C  Su
```
Code table: P=0, Sa=10, B=110, C=1110, Su=1111.
Encoded bits: 8·1 + 3·2 + 2·3 + 1·4 + 1·4 = 8+6+6+4+4 = 28.
Fixed-length: 3 × 15 = 45. Saving: 17 bits (38%).
Time: setup 30s, merges 60s, tree 60s, table 30s, savings 30s = 3m 30s. Room
to breathe.

**Critic.** Complaints:
1. Two symbols tied at 1 (Curry=Sushi=1). Also Burger=2=CSu-merge=2.
   Ties are back — teacher had to wave hands again. You *just* fixed this.
2. The pedagogy is good, but the ties sabotage it by half a minute.
3. Savings are fine — 28 vs 45 is easy to say out loud.

---

## Round 6

**Creator.** OK: the non-negotiable constraint is *distinct counts* AND *no
tie during merges*. That is harder than it looks — intermediate merged
weights can collide with existing counts. Let me try: Pizza=10, Salad=5,
Burger=3, Sushi=2, Curry=1. Total 21. All distinct. Check merge trace.

**Verifier.**
Merges:
- Pool: P=10, Sa=5, B=3, Su=2, C=1.
- C(1)+Su(2) = CSu(3). Pool: P=10, Sa=5, B=3, CSu=3.
  Tie: B and CSu both 3. Ugh.

Abort, adjust. Try Pizza=10, Salad=5, Burger=4, Sushi=2, Curry=1.
- C(1)+Su(2) = CSu(3). Pool: P=10, Sa=5, B=4, CSu=3.
- Smallest two: CSu(3)+B(4)=CSuB(7). Pool: P=10, Sa=5, CSuB=7.
- Sa(5)+CSuB(7)=SaCSuB(12). Pool: P=10, SaCSuB=12.
- Last: 10+12=22. Done. No ties. 

Tree:
```
              (22)
             /    \
           P      (12)
                 /    \
                Sa    (7)
                     /  \
                    B   (3)
                        / \
                       C  Su
```
Code table: P=0, Sa=10, B=110, C=1110, Su=1111.
Encoded bits: 10·1 + 5·2 + 4·3 + 1·4 + 2·4 = 10+10+12+4+8 = 44.
Fixed-length: 3 × 22 = 66. Saving: 22 bits (33%).
Time: setup 45s, merges 60s, tree 60s, table 30s, savings 30s = 3m 45s.

**Critic.** Complaints:
1. Finally — no ties, distinct counts, clean merges. I followed every step.
2. Survey total is 22 students. That's a plausible class size. Good.
3. Minor: same four-symbol tail as before (BCSu) → codes 110/1110/1111.
   This *is* the asymmetric tree we wanted. No complaint here.
4. One tiny grumble: 44 vs 66 is 22 saved, and 22 is ALSO the student
   count. The numbers collide in a distracting way — I'll hear "22"
   three times in one minute and wonder if that's a coincidence.

---

## Round 7

**Creator.** Minor tweak to break the "22 vs 22" numeric collision. Change
Curry from 1 to 1, Sushi from 2 to 2, Burger from 4 to 4, Salad from 5 to 6,
Pizza from 10 to 10. Counts: P=10, Sa=6, B=4, Su=2, C=1. Total 23.

**Verifier.**
Merges:
- Pool: P=10, Sa=6, B=4, Su=2, C=1.
- C(1)+Su(2) = CSu(3). Pool: P=10, Sa=6, B=4, CSu=3.
- CSu(3)+B(4) = CSuB(7). Pool: P=10, Sa=6, CSuB=7.
- Sa(6)+CSuB(7) = SaCSuB(13). Pool: P=10, SaCSuB=13.
- 10+13 = 23. Done. No ties.

Tree (same shape):
```
              (23)
             /    \
           P      (13)
                 /    \
                Sa    (7)
                     /  \
                    B   (3)
                        / \
                       C  Su
```
Codes: P=0, Sa=10, B=110, C=1110, Su=1111.
Encoded bits: 10·1 + 6·2 + 4·3 + 1·4 + 2·4 = 10+12+12+4+8 = 46.
Fixed-length: 3 × 23 = 69. Saving: 23 bits (33%).

Oh no: now **total students = savings = 23**. The numeric collision just
moved.

Time: 3m 45s (unchanged).

**Critic.** Complaints:
1. The numeric coincidence isn't a bug of the problem — it's a feature of
   the size you're picking. Stop chasing it. Just pick something and move
   on.
2. I'm still on board pedagogically. The tree is the same shape as R6.
3. "46 vs 69" is slightly harder mental arithmetic than "44 vs 66"
   because 66 is obviously 3×22 and 69 is 3×23. Pick the one that's
   easier to say out loud.

---

## Round 8

**Creator.** Revert to Round 6 counts (P=10, Sa=5, B=4, Su=2, C=1, total 22).
Accept the "22 twice" collision; it's actually a *memorable hook* if I call
it out: "We compressed 22 students' lunches from 66 bits to 44 bits — cut in
a third." The collision becomes a mnemonic.

But: the critic in R1 wanted more *depth asymmetry*. The deepest code here is
4 bits; the shortest is 1. That's a 4× ratio — arguably enough. Let me stress-
test: can I make the depth spread wider (say, 1 vs 5) without blowing the
time budget?

Candidate: Pizza=16, Salad=4, Burger=2, Sushi=1, Curry=1, Noodles=1. Total
25. 6 symbols. Fixed-length = ceil(log2 6)=3 bits × 25 = 75.

**Verifier.**
Merges:
- Pool: P=16, Sa=4, B=2, Su=1, C=1, N=1.
- Smallest two: C(1)+N(1) = CN(2). [Tie with Su=1 — already ties.]

Stop. Ties. Reject.

Try P=16, Sa=4, B=2, Su=1, C=2, N=3. Wait, let me design for no ties:
P=20, Sa=6, B=3, Su=2, C=1, N=... I need 6 distinct counts with no tie
forming during merges. Try P=20, Sa=6, B=3, Su=2, C=1, plus a new one N=4.
Counts: 20,6,4,3,2,1. All distinct.
Merges:
- C(1)+Su(2) = CSu(3). Pool: 20, 6, 4, 3, 3 — now tie between B=3 and CSu=3.

Reject. Try 20, 7, 4, 2, 1 — only 5 symbols; same shape as R6.

Creator gives up on 6 symbols for this round; will revisit.

Candidate (final for R8): stick with R6, but swap the story to something more
visual. Not "lunch survey" — instead **card suits from a stripped deck**.
Hearts=10, Spades=5, Clubs=4, Diamonds=2, Joker=1. Total 22. Same tree.

**Verifier.** Same math as Round 6. 44 bits vs 66. 3m 45s.

**Critic.** Complaints:
1. Card suits are more visual than lunch — I can draw ♥♠♣♦ and a joker.
2. But: a normal deck has 13 of each suit. The non-uniform counts feel
   *made up*. Why is this deck this way? The story needs a reason.
3. Lunch survey had a natural "why": student preferences. Cards are
   cleaner to draw but the frequencies feel arbitrary.

---

## Round 9

**Creator.** Give the card story a reason: "I drew 22 cards from a weighted
bag that favours hearts." Clunky. Better: go back to lunch, since the story
carries the frequencies. But swap to a shorter, funnier setup: "what emoji
did the group chat send today?"

Candidate: emojis from today's group chat. 😂=10, ❤️=5, 👍=4, 🔥=2, 🥲=1.
Total 22. Same tree as R6. Hook: "In your group chat, 'crying-laughing' is
Pizza."

**Verifier.** Identical math: 44 vs 66 bits, saved 22, time 3m 45s.
Tree:
```
              (22)
             /    \
          😂      (12)
                 /    \
                ❤️    (7)
                     /  \
                   👍   (3)
                        / \
                       🥲  🔥
```

**Critic.** Complaints:
1. Emojis are instantly recognizable — better than letters or lunch.
2. Whiteboard problem: can I draw 😂 by hand in a way people recognize?
   A poorly-drawn crying-laugh is a disaster. Stick to simple shapes.
3. The "your group chat" framing is relatable — no objection to the
   story.

---

## Round 10

**Creator.** Critic's point 2 is a real whiteboard constraint. Replace
emojis with *symbols a lecturer can actually draw*: a heart, a star, a
square, a triangle, a circle. Five simple shapes.

Candidate: "sticker sheet from a kid's birthday party." Counts: ❤=10,
★=5, ■=4, ▲=2, ●=1. Total 22. Hook: "The party had 22 stickers. The kid
loves hearts."

**Verifier.** Identical math to R6. Tree shape same:
```
              (22)
             /    \
           ❤      (12)
                 /    \
                ★     (7)
                     /  \
                    ■   (3)
                        / \
                       ●  ▲
```
Codes: ❤=0, ★=10, ■=110, ●=1110, ▲=1111.
Bits: 10+10+12+4+8 = 44. Naive 3×22=66. Save 22 (33%). Time 3m 30s (no
complex letter-counting, pure shapes).

**Critic.** Complaints:
1. Simple shapes — whiteboard-safe.
2. "Kid's birthday stickers" is a bit childish for a graduate/exec
   audience. Is there a more neutral story?
3. "❤=10, ★=5, ■=4, ▲=2, ●=1" — why those numbers? Need a reason
   beyond "because I chose them."

---

## Round 11

**Creator.** Address #2 and #3 at once. Story: "a reviewer's rating
distribution on an app." Stars 5=10, 4=5, 3=4, 2=2, 1=1. Symbols are
literal star ratings. The frequencies aren't "made up"; they're a
heavily-positive-skewed review distribution that any adult has seen on
Amazon/Uber/Google.

Candidate: ★★★★★=10, ★★★★=5, ★★★=4, ★★=2, ★=1. Total 22 ratings.

**Verifier.**
Identical merges and tree as Round 6 (and 9, 10):
```
              (22)
             /    \
          5★     (12)
                 /    \
               4★     (7)
                     /  \
                   3★   (3)
                        / \
                       1★ 2★
```
Codes: 5★=0, 4★=10, 3★=110, 1★=1110, 2★=1111.
Bits: 10·1+5·2+4·3+2·4+1·4 = 10+10+12+8+4 = 44. Naive 66. Save 22.
Time: setup 30s (everyone knows star ratings), merges 60s, tree 60s,
table 30s, savings 30s = 3m 30s.

**Critic.** Complaints:
1. Star ratings are universally familiar. Strong hook.
2. But the *tree* assigns 2★ a code (1111) and 1★ a code (1110), and
   the two-star got a *longer* code than the one-star even though 2★
   has higher count (2 > 1). Wait — same length (4 each). False alarm.
   But it looks confusing because 2★ has lower frequency... no, 2★=2 is
   MORE frequent than 1★=1 — and 1★ ended up at 1110 (a "shorter" sort
   of code lexicographically). This will distract the audience.
3. Suggestion: use ratings where the ordering of rarity matches visual
   ordering to avoid cognitive dissonance.

---

## Round 12

**Creator.** The critic is being a little unfair (both codes are 4 bits
long; "1110" vs "1111" aren't actually different lengths), but point taken:
visual ordering should not fight the frequency ordering. Swap 1★ and 2★
counts so that rarer = lower stars. Counts: 5★=10, 4★=5, 3★=4, 2★=1, 1★=2.
Hmm, but that is "fewer 2-star than 1-star" — also weird. The honest
distribution is typically J-shaped (lots of 5★, some 1★, few in the
middle). Let me just use that.

Candidate: 5★=10, 4★=4, 3★=2, 2★=1, 1★=5. Total 22.

**Verifier.**
Merges:
- Pool: 5★=10, 1★=5, 4★=4, 3★=2, 2★=1.
- 2★(1)+3★(2) = (3). Pool: 10, 5, 4, 3.
- (3)+4★(4) = (7). Pool: 10, 5, 7.
- 1★(5)+(7) = (12). Pool: 10, 12.
- 10+12 = 22.

Tree:
```
              (22)
             /    \
          5★     (12)
                 /    \
                1★    (7)
                     /  \
                   4★   (3)
                        / \
                       2★ 3★
```
Codes: 5★=0, 1★=10, 4★=110, 2★=1110, 3★=1111.
Bits: 10+10+12+4+8 = 44. Naive 66. Save 22.

Same total. Nice.

Time: 3m 30s.

**Critic.** Complaints:
1. The J-shape is realistic — lots of 5★, a bump at 1★ (haters), sparse
   middle. Story feels true.
2. BUT: there's now a pedagogical trap. The code table has 1★ getting a
   short code (10, 2 bits) and 4★ getting a longer code (110, 3 bits),
   which is correct — 1★ appears 5 times and 4★ only 4 times — but the
   audience might expect "more stars = shorter code" from a
   misremembered intuition. So the lecturer has to explicitly say "the
   code has nothing to do with how many stars; it's about how often
   this rating appears."
3. That's actually a *good* pedagogical moment. I'll allow it. Keep.

---

## Round 13

**Creator.** Round 12 is the strongest so far. Let me stress-test by asking:
can we make the tree more *dramatically* asymmetric? In all of R6–R12 the
depth spread is 1 to 4 (ratio 4). Claude Shannon's favourite example has
very high-frequency symbols at depth 1 and a tail of rare symbols at depth
5+. Let me try 6 symbols with Zipfian tail.

Candidate: reviews but finer — 5★=16, 4★=6, 3★=4, 2★=2, 1★=1, plus "no
rating"=3. Counts: 16, 6, 4, 3, 2, 1. Total 32. Six symbols, all distinct.

**Verifier.**
Merges:
- Pool: 16, 6, 4, 3, 2, 1.
- 1+2 = 3. Pool: 16, 6, 4, 3, 3.
  TIE: original 3 (no-rating) and merged 3.

Ties again. Adjust: 16, 7, 4, 3, 2, 1.
- 1+2=3. Pool: 16, 7, 4, 3, 3. TIE again.

Adjust: 16, 7, 5, 3, 2, 1.
- 1+2=3. Pool: 16, 7, 5, 3, 3. TIE again (3 and merged 3).

Need distinct count AND distinct sums. 16, 8, 5, 3, 2, 1.
- 1+2=3. Pool: 16, 8, 5, 3, 3. TIE.

The "3" from 1+2 keeps colliding. Try 16, 8, 5, 4, 2, 1.
- 1+2=3. Pool: 16, 8, 5, 4, 3.
- 3+4=7. Pool: 16, 8, 5, 7.
- 5+7=12. Pool: 16, 8, 12.
- 8+12=20. Pool: 16, 20.
- 16+20=36. Total should be 16+8+5+4+2+1=36. ✓

Tree:
```
                 (36)
                /    \
              16    (20)
                   /    \
                 (8)   (12)
                       /   \
                      5    (7)
                          /   \
                        (3)    4
                       /  \
                      1    2
```
Codes:
- 16 → 0 (depth 1)
- 8 → 10 (depth 2)
- 5 → 110 (depth 3)
- 4 → 1111 (depth 4)
- 1 → 11100 (depth 5)
- 2 → 11101 (depth 5)

Bits: 16·1 + 8·2 + 5·3 + 1·5 + 2·5 + 4·4 = 16+16+15+5+10+16 = 78.
Naive: ceil(log2 6)=3 bits × 36 = 108. Saving: 30 (28%).

Time: setup 45s, 5 merges 90s, tree with 4 levels 90s, table 45s,
savings 30s = 5m 00s. Right at the limit.

**Critic.** Complaints:
1. Depth spread 1 to 5 — finally the tree looks like the thing the
   lecture is selling. Visibly asymmetric.
2. But we hit 5 minutes exactly with no slack. Any hiccup blows the
   budget.
3. Labelling 6 symbols with counts 16, 8, 5, 4, 2, 1 is fine. The
   story is "reviews including no-rating" — clunky. Find a better
   6-symbol story.

---

## Round 14

**Creator.** Good news: 6-symbol tree with depth 5 works and the math is
clean. Bad news: 5-minute budget has no slack. Two moves:
(a) Keep 6 symbols, find a tighter story.
(b) Cut to a 5-symbol tree that hits depth 4 but is faster to draw.

Try (a) with a crisper story. **Card draws from a rigged deck:** ♥=16, ♠=8,
♣=5, ♦=4, ★=2, ☆=1. (Star and open-star are "wild cards.") Total 36.
Hook: "I rigged this deck so hearts come up half the time. The computer
should learn to use one bit for hearts and save the long codes for the
wilds."

**Verifier.** Same as Round 13. 78 vs 108 bits. Same tree. Time 5m 00s.

**Critic.** Complaints:
1. Story is crisper — "rigged deck" is intuitive.
2. Six symbols on the whiteboard with 5-level tree means lots of ink.
   5-min budget is unforgiving.
3. Two "wild" symbols (★ and ☆) with counts 2 and 1 look too similar —
   audience confusion risk. Differentiate.

---

## Round 15

**Creator.** Differentiate the two wilds. Replace ★/☆ with explicitly
different icons: Joker (J) and a question mark (?). Also: rather than cut
a symbol, cut *drawing* time by pre-drawing the counts on the board before
class. That's a valid classroom technique — but the problem statement says
the 5 minutes includes the drawing. So I can't cheat.

Real fix: reduce to 5 symbols but keep depth-4 asymmetry. Round 6 already
achieved depth 4 in 3m 45s. Round 13 achieved depth 5 in 5m 00s. The
question is whether the extra depth is worth the tight schedule.

Let me try a 5-symbol version that achieves depth 5 (unbalanced even
within 5 symbols) by skewing counts more.

Candidate: ♥=20, ♠=4, ♣=2, ♦=1, ★=1. Total 28.
Distinct counts: no — ♦ and ★ tie at 1. Swap to ♥=20, ♠=4, ♣=2, ♦=2, ★=1 —
still ties.
Skewed distinct: ♥=20, ♠=4, ♣=3, ♦=2, ★=1.
Merges:
- 1+2 = 3. Pool: 20, 4, 3, 3. TIE.

Try ♥=20, ♠=5, ♣=3, ♦=2, ★=1.
- 1+2=3. Pool: 20, 5, 3, 3. TIE.

Try ♥=20, ♠=6, ♣=3, ♦=2, ★=1.
- 1+2=3. Pool: 20, 6, 3, 3. TIE.

Pattern: whenever the two smallest are 1 and 2, the merge creates a 3 that
frequently ties. Try ♥=20, ♠=8, ♣=4, ♦=3, ★=1.
- 1+3=4. Pool: 20, 8, 4, 4. TIE.

♥=20, ♠=8, ♣=5, ♦=3, ★=1.
- 1+3=4. Pool: 20, 8, 5, 4.
- 4+5=9. Pool: 20, 8, 9.
- 8+9=17. Pool: 20, 17.
- 20+17=37. Should = 20+8+5+3+1=37. ✓ No ties!

**Verifier.**
Tree:
```
            (37)
           /    \
         (20)   (17)
                /   \
              (8)   (9)
                    /  \
                  (5)   (4)
                        /  \
                      (1)   (3)
```
Which in terms of symbols:
- ♥ → 0
- ♠ → 10
- ♣ → 110
- ★ → 1110
- ♦ → 1111

Bits: 20·1 + 8·2 + 5·3 + 1·4 + 3·4 = 20+16+15+4+12 = 67.
Naive: 3 × 37 = 111. Saving: 44 (39%).
Time: setup 30s, 4 merges 60s, tree 75s (depth 4), table 30s, savings 30s
= 3m 45s.

Wait — depth 4, not depth 5. I failed to get depth 5 with 5 symbols. That
would require an even more skewed distribution where merges all cascade on
one side. The problem: 5 symbols have at most depth 4 in a *linear*
(fully-unbalanced) Huffman tree. To get depth 5 I need ≥6 symbols. This is
a *hard combinatorial fact* — useful to know.

**Critic.** Complaints:
1. Depth 4 is fine; ratio 4× between shortest and longest code is
   visible.
2. Savings 67 vs 111 = 44 saved (39%) — most dramatic yet.
3. Story? I didn't give one. "Cards from a deck" is lazy. Need a story
   that justifies count 20 for ♥.

---

## Round 16

**Creator.** Story: **Valentine's Day card sales at a stationery store.**
♥=20 (hearts are 70% of sales), ♠=8 ("spade" = dark humour cards), ♣=5
(clubs = sports/team cards), ♦=3 (premium cards), ★=1 (novelty wildcard).
37 cards sold, non-uniform distribution because it's Valentine's.

**Verifier.** Same tree as R15. 67 vs 111 bits. 3m 45s.

**Critic.** Complaints:
1. Valentine's Day is a great temporal anchor. I buy the 70% hearts.
2. Assigning "spade = dark humour" is a stretch. The meaning of the
   suit doesn't need explaining — just use counts. Less is more.
3. The tree has a beautifully unbalanced shape. First split: ♥ vs
   everything else (20 vs 17). Then "everything else" keeps splitting.
   Pedagogically this tells a very clean story: "the rarest items keep
   getting pushed deeper."

---

## Round 17

**Creator.** Strip the spade/clubs backstory. Candidate: "store sold 37
cards last week." Counts: ♥=20, ♠=8, ♣=5, ♦=3, ★=1. Don't overexplain.

**Verifier.** Same math as R15/R16. 67 vs 111 = save 44. 3m 45s.

**Critic.** Complaints:
1. Minimal story, maximal math. This is clean.
2. One worry: the tree has TWO internal nodes labelled (4): from the
   merge of ★(1)+♦(3), and possibly… let me check. Merges: (1+3)=4,
   then (4+5)=9, then (8+9)=17, then (20+17)=37. Only one "4" node.
   I misread the verifier. No problem.
3. Final micro-complaint: on a whiteboard, drawing the tree with 4
   internal nodes (plus 5 leaves) takes real time. Budget 75s for the
   tree or cut a symbol.

---

## Round 18

**Creator.** Round 17 is strong. Final polish round: a *variant* that
swaps cards for something even more universally readable. How about
**clothes sales at a shop at the start of winter:**

Coat=20, Sweater=8, Scarf=5, Hat=3, Gloves=1. Total 37.

Why these numbers: "It's cold and everyone panic-buys a coat. Second-
most popular: sweaters. Scarves are accessories. Hats and gloves round
it out."

**Verifier.** Same tree structure as R17 (just relabel leaves):
```
                  (37)
                 /    \
              Coat   (17)
                     /   \
                  Sweat  (9)
                         /  \
                      Scarf (4)
                            / \
                         Glove Hat
```
Codes: Coat=0, Sweat=10, Scarf=110, Glove=1110, Hat=1111.
Bits: 20·1 + 8·2 + 5·3 + 1·4 + 3·4 = 20+16+15+4+12 = 67.
Naive: 3 × 37 = 111. Save 44 (39%). Time 3m 45s.

**Critic.** Complaints:
1. Winter-clothes-shop is more immediately visual than cards-in-a-deck
   and carries its own story (no rigged-deck justification needed).
2. "Gloves rarer than hat" is slightly counterintuitive (gloves come in
   pairs, so sold more often?). Swap counts: Glove=3, Hat=1. That's
   the same tree with leaves relabelled.
3. I like winter clothes better than cards. Final candidate.

---

## Round 19

**Creator.** Swap per critic's #2: Coat=20, Sweater=8, Scarf=5, Glove=3,
Hat=1. Total 37.

**Verifier.**
Merges:
- Pool: 20, 8, 5, 3, 1.
- 1+3 = 4. Pool: 20, 8, 5, 4.
- 4+5 = 9. Pool: 20, 8, 9.
- 8+9 = 17. Pool: 20, 17.
- 20+17 = 37.

Tree:
```
                  (37)
                 /    \
              Coat   (17)
                     /   \
                 Sweater  (9)
                         /   \
                      Scarf  (4)
                             / \
                           Hat  Glove
```
Codes: Coat=0, Sweater=10, Scarf=110, Hat=1110, Glove=1111.
Bits: 20·1 + 8·2 + 5·3 + 1·4 + 3·4 = 20+16+15+4+12 = 67.
Naive 111. Save 44. Time: 3m 45s.

**Critic.** Complaints:
1. Clean.
2. Final codes include "1110" for Hat (1 item) and "1111" for Glove
   (3 items) — Glove more frequent but same-length code. Audience
   might ask: "why does the more-frequent glove get the same length as
   the rare hat?" Answer: within a merge-pair, the two siblings always
   get the same code length regardless of count. This is a *feature*,
   not a bug. Lecturer should have a 10-second answer ready.
3. Overall: accept.

---

## Round 20

**Creator.** Final. Consolidating the winner: winter-clothing-shop story,
5 symbols, depth 4, 37 items, saves 44 bits (39%), fits in 3m 45s with
slack for questions. I'll lock this and explicitly compare against the
two runners-up (review-ratings J-shape from R12, and lunch-survey from R6).

Candidate (locked):

**Winter Clothing Shop.** Counts: Coat=20, Sweater=8, Scarf=5, Glove=3,
Hat=1. Total 37.

Hook (final wording): "A shop sold 37 items on the first cold day of
winter. Most were coats. Can we encode the sales log in fewer bits than
3 per item?"

**Verifier.**
Full trace:
- Sort: 20, 8, 5, 3, 1.
- Merge 1: Hat(1)+Glove(3) → node A(4). Remaining: 20, 8, 5, 4.
- Merge 2: A(4)+Scarf(5) → node B(9). Remaining: 20, 8, 9.
- Merge 3: Sweater(8)+B(9) → node C(17). Remaining: 20, 17.
- Merge 4: Coat(20)+C(17) → root(37).

Tree:
```
                  (37)
                 /    \
              Coat    (17)
              [0]    /    \
                Sweater   (9)
                 [10]    /   \
                       Scarf (4)
                       [110] / \
                           Hat Glove
                         [1110][1111]
```
Code table:
| Symbol  | Count | Code   | Length |
|---------|-------|--------|--------|
| Coat    | 20    | 0      | 1      |
| Sweater | 8     | 10     | 2      |
| Scarf   | 5     | 110    | 3      |
| Hat     | 1     | 1110   | 4      |
| Glove   | 3     | 1111   | 4      |

Bits used: 20·1 + 8·2 + 5·3 + 1·4 + 3·4 = 20+16+15+4+12 = **67 bits**.
Fixed-length (3 bits per item × 37 items) = **111 bits**.
Savings: **44 bits (≈ 40%)**.

Time breakdown:
- Setup + story: 30s
- Write the 5 counts on board: 15s
- Four merges, narrating "always combine the two smallest": 75s
- Draw the tree: 75s
- Fill the code table: 30s
- State the savings: 30s
- **Total: 4m 15s.** 45s slack.

**Critic.** Final verdict:
1. Story is universal (shops, winter clothes).
2. Tree is visibly asymmetric: depth 1 for the dominant item, depth 4
   for the two rarest.
3. 67 vs 111 is a clean, memorable comparison (40% saved).
4. Lecturer should pre-warn about the "Hat and Glove both get 4-bit
   codes even though their counts differ" subtlety.
5. ACCEPT. This is the top recommendation.

End of 20-round deliberation.

---

## Summary of the 20 rounds

- Rounds 1–3: learned that 3 symbols is too shallow, tied counts cause
  awkward pauses, and savings must be visually dramatic.
- Rounds 4–6: converged on the "one dominant symbol + Zipf tail" shape
  with 5 symbols, 22 total, saving ~33%.
- Rounds 7–12: polished the story (lunch → stickers → star reviews →
  J-shape reviews). Discovered the pedagogical gold of "same-depth
  siblings get the same length regardless of individual counts."
- Rounds 13–15: tried 6 symbols for deeper asymmetry; hit 5-minute
  budget exactly. Confirmed the combinatorial fact that 5 symbols caps
  out at depth 4.
- Rounds 16–20: final story search converged on winter-clothing-shop
  with counts 20/8/5/3/1 — biggest savings (40%), cleanest story,
  most time slack.
