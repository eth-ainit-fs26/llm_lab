# Huffman Toy Example Committee — Run v2 (Bushy Tree Constraint)

Prior committee (`huffman_committee_log.md`) converged on right-spine
trees with depth multiset `{1,2,3,4,4}`. The lecturer judged those
visually monotonous. This run re-opens the search under a new
constraint:

> **Bushy shape required.** At least one internal node must itself
> split into two internal subtrees, so the tree branches on more than
> one level.

Unchanged constraints:
- ≤5 minute activity, no information-theory background.
- Concrete symbols (shop, menu, cards, apps, etc.).
- Integer counts, tie-free merges.
- ≥20% savings vs ⌈log₂ n⌉-bit fixed-length (target 25–35%).

Three roles each round: **CREATOR**, **VERIFIER**, **CRITIC**.
Creator incorporates the critic's feedback at round N+1.

---

## Round 1

**CREATOR.** Start from the v1 winner (`Coat 20, Sweater 8, Scarf 5,
Glove 3, Hat 1`) and try to bend it bushy. Story unchanged: winter
shop. Why bushy? If I can introduce a mid-weight pair that merges early
and a small pair that merges early, the algorithm will form two
sub-piles rather than a single spine. Proposal: `Coat 15, Sweater 8,
Scarf 6, Glove 4, Hat 3, Boot 2`. (Total 38, 6 symbols, fixed = 3 bits.)

**VERIFIER.**
- Merge 1: Boot(2) + Hat(3) → A(5). Queue: {4,5,5A,6,8,15}. **Tie: 5 vs
  A(5).** Arithmetically defensible but violates tie-free rule.

Rejected.

**CRITIC.** Good direction (6 symbols, 3-bit fixed-length still clean),
but the 2+3 = 5 collision is the classic beginner trap. Pick starting
numbers so the first pairwise sum never hits an existing count.

---

## Round 2

**CREATOR.** Following critic: start numbers that do not sum to another
starter. Proposal: `Coat 15, Sweater 8, Scarf 6, Glove 4, Hat 3, Boot 1`
(replace Boot 2 → 1). Total 37. Small pair 1+3 = 4, which collides with
Glove(4). Same trap.

**VERIFIER.** Merge 1: 1+3=4A. Queue {4, 4A, 6, 8, 15}. **Tie.** Reject.

**CRITIC.** Same problem. You need the two smallest to sum to something
strictly outside the starting multiset. 1+3 collides with 4; 2+3
collides with 5. Try 1+4 = 5 (not in set) or 3+4 = 7 (not in set).

---

## Round 3

**CREATOR.** Proposal: `Coat 12, Sweater 8, Scarf 6, Glove 4, Hat 3, Boot 1`.
Two smallest are Boot(1) + Hat(3) = 4. **Tie with Glove(4).** Still
broken.

**VERIFIER.** Reject: tie at step 1.

**CRITIC.** You keep hitting the small-number collision. Drop either
the 3 or the 4. Specifically — if you keep {1, 3} as smallest, remove
the 4 from the set. Or switch to smallest {3, 4} (sum 7) and remove 7.

---

## Round 4

**CREATOR.** Drop the 4. Proposal: `Coat 12, Sweater 8, Scarf 6, Hat 3,
Boot 1` (5 symbols, 30 total). Smallest pair: 1+3=4, not in set.

**VERIFIER.**
- Merge 1: 1+3 = 4A. Queue {4A, 6, 8, 12}. Distinct.
- Merge 2: 4A+6 = 10B. Queue {8, 10B, 12}. Distinct.
- Merge 3: 8+10B = 18C. Queue {12, 18C}. Distinct.
- Merge 4: 12+18C = 30.

Tree: Coat(12) | 18C → {Sweater(8) | 10B} → {Scarf(6) | 4A} → {Boot(1)
| Hat(3)}.

Depths: Coat 1, Sweater 2, Scarf 3, Boot 4, Hat 4 = **{1,2,3,4,4}**.
**This is a spine.** Exactly what we were told to avoid.

**CRITIC.** Back to square one. To force bushiness you need two
*separate* early pairs to each form an internal node, and then those
internal nodes must merge together before being absorbed by a big
singleton. That means at least four mid-sized symbols of roughly equal
count so they pair up on the first two merges.

---

## Round 5

**CREATOR.** Lean into critic's insight. Use one dominant symbol plus
four roughly equal mid-sized symbols, no near-zero tail. Proposal:
`Pizza 20, Salad 6, Burger 5, Taco 4, Sushi 3` (5 symbols, total 38).

**VERIFIER.**
- Merge 1: Sushi(3) + Taco(4) = 7A. Queue {5, 6, 7A, 20}. Distinct.
- Merge 2: Burger(5) + Salad(6) = 11B. Queue {7A, 11B, 20}. Distinct.
- Merge 3: 7A + 11B = 18C. Queue {18C, 20}. Distinct.
- Merge 4: 18C + 20 = 38.

Tree:
```
         (38)
        /    \
     Pizza  (18C)
     [0]   /     \
        (7A)    (11B)
       /  \     /   \
    Sushi Taco Burger Salad
    [100] [101] [110] [111]
```
Depths: Pizza 1, Sushi 3, Taco 3, Burger 3, Salad 3 = **{1,3,3,3,3}**.
**Bushy!** Root branches into one leaf and one subtree; that subtree
branches into two subtrees; each of those branches into two leaves.

Bits: 20·1 + 3·3 + 4·3 + 5·3 + 6·3 = 20 + 9 + 12 + 15 + 18 = 74.
Fixed: 3·38 = 114. Savings: 40/114 = **35.1%**. In the sweet spot.

All merge values 7, 11, 18, 38 — distinct from each other and from all
frequencies. Tie-free.

**CRITIC.** This is the first actually good candidate. Story is
zero-friction (everyone has ordered lunch). Tree looks visibly
different from the v1 spines. The only nit: Pizza dominates by a lot
(20 of 38), so the "one pile is special" narrative is the whole show.
That's fine but the tree does not reward drawing *the bottom two
merges* with suspense — both pairs merge at the same step. Could a
6-symbol version sustain more suspense?

---

## Round 6

**CREATOR.** Extend round 5 to 6 symbols for more merge theater.
`Pizza 20, Salad 8, Burger 6, Taco 5, Sushi 4, Curry 3`. Total 46.

**VERIFIER.**
- Merge 1: Curry(3) + Sushi(4) = 7A. Queue {5, 6, 7A, 8, 20}. Distinct.
- Merge 2: Taco(5) + Burger(6) = 11B. Queue {7A, 8, 11B, 20}. Distinct.
- Merge 3: 7A + Salad(8) = 15C. Queue {11B, 15C, 20}. Distinct.
- Merge 4: 11B + 15C = 26D. Queue {20, 26D}. Distinct.
- Merge 5: 20 + 26D = 46.

Tree:
```
              (46)
             /    \
          Pizza  (26D)
          [0]   /     \
             (11B)   (15C)
            /   \    /    \
         Taco Burger Salad (7A)
         [100][101] [110] /  \
                        Curry Sushi
                       [1110][1111]
```
Depths: Pizza 1, Taco 3, Burger 3, Salad 3, Curry 4, Sushi 4 =
**{1,3,3,3,4,4}**. Bushy.

Bits: 20·1 + 8·3 + 6·3 + 5·3 + 3·4 + 4·4 = 20+24+18+15+12+16 = 105.
Fixed: 3·46 = 138. Savings: 33/138 = **23.9%**.

Tie-free verified.

**CRITIC.** Savings slip to just under the sweet spot (24%). The 6-
symbol version has more merge drama, but the 5-symbol round-5 version
has bigger numeric punchline. If we go 6 symbols, skew Pizza further
up to recover savings.

---

## Round 7

**CREATOR.** Skew harder: `Pizza 25, Salad 9, Burger 6, Taco 5, Sushi 4,
Curry 3`. Total 52.

**VERIFIER.**
- Merge 1: 3+4 = 7A. Queue {5, 6, 7A, 9, 25}. Distinct.
- Merge 2: 5+6 = 11B. Queue {7A, 9, 11B, 25}. Distinct.
- Merge 3: 7A+9 = 16C. Queue {11B, 16C, 25}. Distinct.
- Merge 4: 11B+16C = 27D. Queue {25, 27D}. Distinct.
- Merge 5: 25+27D = 52.

Tree same shape as round 6.
Depths: Pizza 1, Taco 3, Burger 3, Salad 3, Curry 4, Sushi 4 =
**{1,3,3,3,4,4}**.

Bits: 25·1 + 9·3 + 6·3 + 5·3 + 3·4 + 4·4 = 25+27+18+15+12+16 = 113.
Fixed: 3·52 = 156. Savings: 43/156 = **27.6%**. Sweet spot.

**CRITIC.** Good. But now total = 52 items — more numbers for the
audience to track on the board. Round-5 has 38 items, more mentally
manageable. Run both in parallel and let the lecturer pick on
classroom feel.

---

## Round 8

**CREATOR.** Try a different shape: `{2,2,2,3,3}` depth multiset. This
needs 5 symbols where the root branches into two internal nodes, one
a leaf-pair and the other a three-deep triplet — actually impossible
for 5 symbols with Huffman since the root has two subtrees of sizes
that sum to 5, so shapes possible are (1,4) or (2,3). (1,4) gives our
round-5 {1,3,3,3,3}. (2,3) gives depths {2,2,3,3,3} — let me aim for
that.

For (2,3): root subtrees have 2 and 3 leaves. The 2-leaf subtree sits
at depth 2 (both leaves). The 3-leaf subtree must itself split (1,2):
one leaf at depth 2, two leaves at depth 3. So multiset
**{2,2,2,3,3}**. Numerical recipe: the two leaves under the 2-side
must pair up in the very last merge, so they must be *big* at the top
of the priority queue at the end.

Proposal: `A 7, B 6, C 5, D 3, E 1`. Total 22.
- Merge 1: 1+3 = 4a. Queue {4a, 5, 6, 7}. Distinct.
- Merge 2: 4a+5 = 9b. Queue {6, 7, 9b}. Distinct.
- Merge 3: 6+7 = 13c. Queue {9b, 13c}. Distinct.
- Merge 4: 9b+13c = 22.

**VERIFIER.**
Tree:
```
            (22)
           /    \
         (13c)  (9b)
         /  \   /  \
        B=6 A=7 5C (4a)
       [00][01][10]/  \
                  D=3 E=1
                 [110][111]
```
Depths: B 2, A 2, C 2, D 3, E 3 = **{2,2,2,3,3}**. Bushy and balanced-
ish.

Bits: 7·2 + 6·2 + 5·2 + 3·3 + 1·3 = 14+12+10+9+3 = 48.
Fixed: 3·22 = 66. Savings: 18/66 = **27.3%**. 

Tie-free verified (4, 5, 6, 7, 9, 13, 22 all distinct).

**CRITIC.** This shape is the most visually balanced bushy tree we have.
Story? These are just letters — boring. Give it a concrete skin. Card
suits? Menu items? Dice? Also check: the depth gap is only 3−2 = 1,
which de-dramatizes the "more frequent → shorter code" lesson. Round 5
had depth gap 3−1 = 2, a sharper punchline.

---

## Round 9

**CREATOR.** Skin round 8 as dessert menu:
`Cake 7, Brownie 6, Cookie 5, Pie 3, Tart 1`. Total 22.

Hook: "The café tracks dessert sales over one afternoon. Five kinds,
22 total orders."

Same merges as round 8, same tree, same savings (27.3%).

**VERIFIER.** All steps check. Depths still {2,2,2,3,3}. Bushy.

**CRITIC.** Cleaner than round 8. But I maintain that the {1,3,3,3,3}
shape (round 5) has the sharper pedagogical moment because one symbol
really pops out with code length 1. In round 9, every "popular" item
(Cake, Brownie, Cookie) gets length 2. The *shape* is bushier, but the
*surprise* is flatter. We should keep both in the finals.

---

## Round 10

**CREATOR.** Try shape `{2,2,3,3,3,3}` for 6 symbols. Root: (2,4).
The 2-subtree is two leaves at depth 2. The 4-subtree is two internal
nodes each with two leaves, giving depth 3 for all four. Recipe: two
big roughly-equal symbols, four smaller roughly-equal symbols.

Proposal (shop context): `Latte 11, Cappuccino 10, Mocha 5, Espresso 4,
Tea 3, Juice 2`. Total 35.
- Merge 1: 2+3 = 5a. **Tie with Mocha(5).** Reject.

**VERIFIER.** Reject.

**CRITIC.** Same old collision. Either bump Mocha to 6 or bump the
smallest pair past 5.

---

## Round 11

**CREATOR.** `Latte 11, Cappuccino 10, Mocha 6, Espresso 5, Tea 3,
Juice 2`. Total 37.
- Merge 1: 2+3 = 5a. **Tie with Espresso(5).** Reject.

**VERIFIER.** Reject.

**CRITIC.** You need to bump the 5 too.

---

## Round 12

**CREATOR.** `Latte 11, Cappuccino 10, Mocha 6, Espresso 4, Tea 3,
Juice 2`. Total 36.
- Merge 1: 2+3 = 5a. Queue {4, 5a, 6, 10, 11}. Distinct.
- Merge 2: 4+5a = 9b. Queue {6, 9b, 10, 11}. Distinct.
- Merge 3: 6+9b = 15c. Queue {10, 11, 15c}. Distinct.
- Merge 4: 10+11 = 21d. Queue {15c, 21d}. Distinct.
- Merge 5: 15c + 21d = 36.

**VERIFIER.**
Tree:
```
                 (36)
                /    \
            (15c)    (21d)
            /   \    /    \
         Mocha (9b) Cap Latte
         [00] /  \ [10][11]
            Esp (5a)
            [010]/  \
               Juice Tea
               [0110][0111]
```
Wait — Esp is at depth 3 and the pair (Juice, Tea) is at depth 4.
Re-check: 15c splits into Mocha(6) and 9b. 9b splits into Esp(4) and
5a. 5a splits into Juice(2) and Tea(3).

Depths: Cap 2, Latte 2, Mocha 2, Esp 3, Juice 4, Tea 4 =
**{2,2,2,3,4,4}**. Bushy (root branches into two internals).

Bits: 11·2 + 10·2 + 6·2 + 4·3 + 3·4 + 2·4 = 22+20+12+12+12+8 = 86.
Fixed: 3·36 = 108. Savings: 22/108 = **20.4%**. Just barely.

**CRITIC.** 20.4% is threshold. And the tree isn't *quite* the
symmetric {2,2,3,3,3,3} we were targeting — the left side got a 2-deep
triple and the right got a deeper spine. Partial bushiness. It works
but we can do better.

---

## Round 13

**CREATOR.** Target a true {2,2,3,3,3,3} by picking counts so *both*
subtrees end up balanced. Need: a pair (A,B) that the algorithm merges
late (so they stay at depth 2 together), and four smaller (C,D,E,F)
that pair as (C+D) and (E+F) early and then those merge.

Proposal: `Hearts 15, Spades 14, Diamonds 6, Clubs 5, Jokers 4, Blanks 3`.
Total 47.
- Merge 1: 3+4 = 7a. Queue {5, 6, 7a, 14, 15}. Distinct.
- Merge 2: 5+6 = 11b. Queue {7a, 11b, 14, 15}. Distinct.
- Merge 3: 7a + 11b = 18c. Queue {14, 15, 18c}. Distinct.
- Merge 4: 14 + 15 = 29d. Queue {18c, 29d}. Distinct.
- Merge 5: 18c + 29d = 47.

**VERIFIER.**
Tree:
```
                  (47)
                 /    \
             (18c)    (29d)
             /   \    /    \
          (7a)  (11b) Spades Hearts
          /  \  /   \  [10]   [11]
        Bl  Jo Cl  Di
       [000][001][010][011]
```
Depths: Hearts 2, Spades 2, Diamonds 3, Clubs 3, Jokers 3, Blanks 3 =
**{2,2,3,3,3,3}**. Perfectly bushy.

Bits: 15·2 + 14·2 + 6·3 + 5·3 + 4·3 + 3·3 = 30+28+18+15+12+9 = 112.
Fixed: 3·47 = 141. Savings: 29/141 = **20.6%**. Threshold again.

Tie-free: 7, 11, 14, 15, 18, 29, 47 distinct; freqs 3,4,5,6,14,15
distinct; no merge hits any freq.

**CRITIC.** Story is weaker ("Hearts/Spades/Diamonds/Clubs/Jokers/
Blanks" — why would blanks appear?). Savings barely scrape 20%. The
tree is the most beautifully bushy we have, but the savings payoff is
small and the hook is contrived. Maybe shift to a more natural
2-heavy-plus-4-small-but-similar story.

---

## Round 14

**CREATOR.** Try bus stops on a commuter line. `Central 15, North 14,
East 6, West 5, Airport 4, Harbor 3`. Total 47. Same numbers, better
story: "47 passengers boarded. Two stops dominate; four smaller stops
share the rest."

**VERIFIER.** Identical to round 13. {2,2,3,3,3,3}, savings 20.6%.

**CRITIC.** Story is improved. The symmetry is pretty. But the savings
are still at threshold. Problem: in the {2,2,3,3,3,3} shape *every*
code is either 2 or 3 bits, which gives a very flat histogram of code
lengths. The audience looks at the table and thinks "why did we
bother?" Huffman's dramatic win comes from code length 1 next to code
length 4.

---

## Round 15

**CREATOR.** Return to the {1,3,3,3,3} and {1,3,3,3,4,4} family from
rounds 5 and 7 — they have the visually dramatic depth range. Take
round 7 (6 symbols, 27.6% savings) and re-skin. Story: *daily coffee
orders at a campus café*.

`Espresso 25, Latte 9, Cappuccino 6, Macchiato 5, Mocha 4, Cortado 3`.
Total 52.

**VERIFIER.** Same merges as round 7:
- 3+4 = 7a; 5+6 = 11b; 7a+9 = 16c; 11b+16c = 27d; 25+27d = 52.
- Depths: Espresso 1, Macchiato 3, Cappuccino 3, Latte 3, Cortado 4,
  Mocha 4 = **{1,3,3,3,4,4}**. Bushy.
- Bits: 25·1 + 9·3 + 6·3 + 5·3 + 3·4 + 4·4 = 25+27+18+15+12+16 = 113.
- Fixed: 3·52 = 156. Savings: 43/156 = **27.6%**.

Tie-free verified.

**CRITIC.** Good. The `25` is a bit big to write six times on a
whiteboard, and six distinct coffee names plus counts is a lot of ink.
But it works. Could we find a {1,2,3,3,3,3}-shape to get even more
savings?

---

## Round 16

**CREATOR.** Targeting **{1,2,3,3,3,3}**. Root splits (1,5). Left leaf
at depth 1 (huge count). Right subtree has 5 leaves. The 5-leaf sub-
tree needs to be {1,3,3,3,3}-shaped (per round 5). So two symbols
*among the smaller five* are a big one and the rest are a pair of
pairs.

Proposal: `Dominant 30, Subdominant 12, S1 3, S2 4, S3 5, S4 6`.
Total 60.

**VERIFIER.**
- Merge 1: 3+4 = 7a. Queue {5, 6, 7a, 12, 30}. Distinct.
- Merge 2: 5+6 = 11b. Queue {7a, 11b, 12, 30}. Distinct.
- Merge 3: 7a+11b = 18c. Queue {12, 18c, 30}. Distinct.
- Merge 4: 12+18c = 30d. **Tie with Dominant(30).** Reject.

**CRITIC.** So close. Adjust Dominant or Subdominant to dodge the
collision.

---

## Round 17

**CREATOR.** `Dominant 32, Subdominant 12, S1 3, S2 4, S3 5, S4 6`.
Total 62.

**VERIFIER.**
- Merge 1: 3+4 = 7a.
- Merge 2: 5+6 = 11b.
- Merge 3: 7a+11b = 18c.
- Merge 4: 12+18c = 30d. Queue {30d, 32}. Distinct.
- Merge 5: 30d+32 = 62.

Tree:
```
                    (62)
                   /    \
                 Dom    (30d)
                 [0]   /    \
                     Sub   (18c)
                     [10] /    \
                        (7a)  (11b)
                        / \   /  \
                       S1 S2 S3 S4
                      [1100][1101][1110][1111]
```
Depths: Dom 1, Sub 2, S1 4, S2 4, S3 4, S4 4.

Wait — depth multiset is **{1,2,4,4,4,4}**, not {1,2,3,3,3,3}. The
problem: 18c is merged with 12 *before* it has a chance to sit at
depth 2. The four smallest all end up at the bottom.

Actually this *is* still bushy (root → leaf + internal; that internal
→ leaf + internal; that internal → two internals; each of those → two
leaves). So shape is {1,2,4,4,4,4}. Even bushier than I thought — a
3-level nested structure.

Bits: 32·1 + 12·2 + 3·4 + 4·4 + 5·4 + 6·4 = 32+24+12+16+20+24 = 128.
Fixed: 3·62 = 186. Savings: 58/186 = **31.2%**. Sweet spot!

All merge values 7, 11, 18, 30, 62 distinct. Tie-free.

**CRITIC.** 31% savings, shape {1,2,4,4,4,4} — visibly bushy, three
distinct code lengths (1, 2, 4), and big dramatic range. But 62 items
is a lot to talk through, and Dominant-32 writes as an ugly number on
the board. Story skin needed.

---

## Round 18

**CREATOR.** Skin round 17 as a weather log:
`Sunny 32, Cloudy 12, Rainy 6, Drizzle 5, Snow 4, Hail 3`.
Hook: "A city meteorologist logged the weather hour-by-hour for a
stretch of 62 hours. Sun dominates. Clouds second. Four wet conditions
round it out."

**VERIFIER.** Merges identical to round 17. Depths {1,2,4,4,4,4}.
Savings 31.2%. Tie-free.

**CRITIC.** Great story skin. Everyone has looked at a weather app.
The "1 bit for Sunny, 4 bits for Hail" gap dramatizes frequency vs
meaning. This is a contender for #1.

---

## Round 19

**CREATOR.** Two more probes before locking finalists. First, can we
improve round 5 ({1,3,3,3,3}, 38 items, 35% savings) with smaller
total so the whiteboard stays tidier?

`Pizza 15, Salad 6, Burger 5, Taco 4, Sushi 3`. Total 33.
- Merge 1: 3+4 = 7a. Queue {5, 6, 7a, 15}. Distinct.
- Merge 2: 5+6 = 11b. Queue {7a, 11b, 15}. Distinct.
- Merge 3: 7a+11b = 18c. Queue {15, 18c}. Distinct.
- Merge 4: 15+18c = 33.

**VERIFIER.**
Depths: Pizza 1, Sushi 3, Taco 3, Burger 3, Salad 3 = **{1,3,3,3,3}**.
Bushy.

Bits: 15·1 + 3·3 + 4·3 + 5·3 + 6·3 = 15+9+12+15+18 = 69.
Fixed: 3·33 = 99. Savings: 30/99 = **30.3%**. Sweet spot, and the
numbers are all smaller — easier to add on the board.

**CRITIC.** This is the cleanest candidate overall. 5 symbols, 33
items, no number above 18, shape {1,3,3,3,3} is the most visually
readable bushy tree, savings 30%. I'd rank this #1.

---

## Round 20

**CREATOR.** Final consolidation pass. Compare the three leading
candidates on the full criteria matrix:

| # | Story | Shape | #sym | Total items | Savings | Biggest count | Verdict |
|---|-------|-------|------|-------------|---------|---------------|---------|
| R5/R19 | Lunch menu | {1,3,3,3,3} | 5 | 33 | 30.3% | 15 | cleanest |
| R18 | Weather log | {1,2,4,4,4,4} | 6 | 62 | 31.2% | 32 | richest |
| R9 | Dessert menu | {2,2,2,3,3} | 5 | 22 | 27.3% | 7 | balanced |

**VERIFIER.** All three re-verified:
- Lunch (R19): merges 7, 11, 18, 33. Freqs {3,4,5,6,15}. No collisions.
- Weather (R18): merges 7, 11, 18, 30, 62. Freqs {3,4,5,6,12,32}. No
  collisions.
- Dessert (R9): merges 4, 9, 13, 22. Freqs {1,3,5,6,7}. No collisions.

All three bushy, all ≥ 27% savings, all tie-free, all ≤ 5 min.

**CRITIC.** Final call:

- **#1 Lunch menu (R19)**. Smallest numbers, sharpest "one bit for the
  winner" moment, shape {1,3,3,3,3} reads clearly on a whiteboard. The
  bottom of the tree is two parallel two-leaf subtrees, which is the
  cleanest way to show that Huffman's merges really are *local* —
  nothing in the big-pizza side interacts with the four small-guys
  side until the very last merge.
- **#2 Weather (R18)**. Best savings and richest tree (three distinct
  code lengths: 1, 2, 4). Use when the lecturer has 5 full minutes and
  wants to stretch the drama. 62 items is heavier on the board.
- **#3 Dessert (R9)**. Use when the class is especially arithmetic-shy
  (smallest total, 22 items), or when the lecturer wants to emphasize
  that bushy trees *can* be near-symmetric — depths {2,2,2,3,3} shows
  that Huffman does not always produce sharp spines, even without the
  one-dominant-symbol skew. Savings are smaller but honest.

Committee closes here. Finals written to `huffman_top3_v2.md`.

---

## Summary findings

- **The bushy constraint is harder than the spine constraint.** Spines
  arise naturally whenever small counts chain (1+3 → 4, 4+5 → 9, etc.).
  To *force* bushiness, you need either (a) one dominant symbol plus
  multiple mid-sized symbols of comparable count so they pair among
  themselves, or (b) two large-and-roughly-equal symbols plus four
  small-and-roughly-equal symbols.
- **Tie collisions are the main dead end.** Six of twenty rounds died
  to ties, all from the same family: 1+2=3, 2+3=5, 1+3=4, 3+4=7. The
  practical rule is to pick starting counts so *no pairwise sum of two
  smallest counts equals any starting count*.
- **Bushy shapes cost some savings.** Spines pack frequency into
  monotonic depth, maximizing bit compression. Bushy trees split
  frequency across depth levels, which costs a few percent. Our best
  bushy candidate saves 31%; the v1 spine winner saved 40%. The
  pedagogical win — a tree that actually looks like branching — is
  worth the trade.
- **Counts that collapsed into spines even though they looked bushy.**
  Round 4 (`12, 8, 6, 3, 1`) *looked* like it had a bushy potential
  because two small counts (1, 3) sit alongside a 6 and an 8, but the
  4a = 1+3 gets absorbed into the 6 before any second pair forms, and
  the whole thing re-linearizes into depths {1,2,3,4,4}. The lesson:
  you need *at least four* roughly-equal small-or-mid counts, not two.
