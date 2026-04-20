# Top 3 Huffman Teaching Examples — v2 (Bushy Trees)

Distilled from the 20-round committee deliberation in
`huffman_committee_log_v2.md`. Every candidate here:

- has a **bushy** tree (at least one internal node whose *both*
  children are internal nodes, not a right-spine),
- uses integer counts producing **tie-free** Huffman merges,
- saves **≥ 20%** vs fixed-length encoding,
- fits a **≤ 5-minute** whiteboard activity,
- assumes zero information-theory background.

Ranked by a combination of whiteboard tidiness, dramatic depth range,
and story clarity.

---

## #1 — Lunch Menu (Round 19)

**Tree shape:** `{1, 3, 3, 3, 3}`

**Story / hook.** "Someone surveyed 33 students at lunch. One option
crushed it. Four others were middling. Can we record the whole survey
in fewer bits than 3 per student?"

**Symbols + counts.**

| Symbol | Count |
|--------|-------|
| Pizza  | 15    |
| Salad  | 6     |
| Burger | 5     |
| Taco   | 4     |
| Sushi  | 3     |

Total: 33 students.

**Huffman merge trace (all merge values distinct from each other and
from all starting counts).**

- Step 1: Sushi(3) + Taco(4) → A(7). Queue: {5, 6, 7, 15}.
- Step 2: Burger(5) + Salad(6) → B(11). Queue: {7, 11, 15}.
- Step 3: A(7) + B(11) → C(18). Queue: {15, 18}.
- Step 4: Pizza(15) + C(18) → Root(33).

**ASCII tree (branches on both sides at the level below root — this is
the bushy hallmark).**

```
                     (33)
                    /    \
                 Pizza   (18 = C)
                 [0]     /        \
                      (7 = A)   (11 = B)
                      /   \     /    \
                   Sushi Taco Burger Salad
                   [100] [101] [110] [111]
```

Note: at the second level the right subtree (C=18) branches into *two
internal nodes* (A=7 and B=11), each of which branches into two
leaves. That is the bushy property.

**Code table.**

| Symbol | Count | Code | Length |
|--------|-------|------|--------|
| Pizza  | 15    | 0    | 1      |
| Sushi  | 3     | 100  | 3      |
| Taco   | 4     | 101  | 3      |
| Burger | 5     | 110  | 3      |
| Salad  | 6     | 111  | 3      |

**Total bits.**
15·1 + 3·3 + 4·3 + 5·3 + 6·3 = 15 + 9 + 12 + 15 + 18 = **69 bits**.
Fixed-length encoding (3 bits × 33 students) = **99 bits**.
**Saved: 30 bits (30.3%).**

**Teaching script (5-minute wall-clock plan).**

1. (30s) "Survey of 33 lunch picks. Five options. Here are the counts."
   Write: Pizza 15, Salad 6, Burger 5, Taco 4, Sushi 3.
2. (15s) "Naive cost: 3 bits × 33 students = 99 bits." Circle 99.
3. (15s) "Huffman's rule: repeatedly combine the two smallest piles."
4. (20s) Merge 1: Sushi(3) + Taco(4) = 7. Draw a ∧ over them with 7
   at the apex. (Sushi on the left, Taco on the right.)
5. (20s) Merge 2: Burger(5) + Salad(6) = 11. Draw a *second* ∧ off to
   the side over Burger and Salad — **emphasize this is a separate
   pile, not a continuation of the first one.** This is the key
   moment. The previous committee's trees had no second pile.
6. (20s) Merge 3: the two piles (7 and 11) are now the smallest
   remaining. Combine them into 18. Draw a ∧ over A(7) and B(11).
7. (20s) Merge 4: Pizza(15) + 18 = 33. Draw the root.
8. (45s) Read codes off the tree. "Left is 0, right is 1." Pizza = 0,
   Sushi = 100, Taco = 101, Burger = 110, Salad = 111.
9. (30s) Compute total: 15·1 + 3·3 + 4·3 + 5·3 + 6·3 = 69. Circle 69.
10. (30s) Punchline: "69 vs 99 — saved 30%, almost a third. Pizza got
    one bit because it's half the data. The other four got three bits
    *each the same*, because they were comparable in size." Gesture at
    the two-pile-then-combine structure: "this is what Huffman looks
    like when the tree actually branches — not a spine."
11. (35s slack / Q&A buffer).

**Time budget.**

| Segment                          | Seconds |
|----------------------------------|---------|
| Setup + story                    | 30      |
| Write counts                     | 15      |
| State 99 bits                    | 15      |
| Rule statement                   | 15      |
| Merge 1 (Sushi + Taco)           | 20      |
| Merge 2 (Burger + Salad)         | 20      |
| Merge 3 (7 + 11)                 | 20      |
| Merge 4 (Pizza + 18)             | 20      |
| Read codes                       | 45      |
| Compute 69                       | 30      |
| Punchline                        | 30      |
| Slack / Q&A                      | 40      |
| **Total**                        | **5m**  |

**Why rank #1.** Smallest total (33 items, all numbers ≤ 15), sharpest
depth range for a bushy tree (1 to 3), and the two-parallel-subtrees
structure *physically separates* on the whiteboard in a way that
drives home Huffman's merge-the-smallest rule. The bottom of the tree
being two mini-trees sitting side by side is the one bit of geometry
the v1 spines could not show — and it's exactly the visual the
lecturer asked for.

---

## #2 — Weather Log (Round 18)

**Tree shape:** `{1, 2, 4, 4, 4, 4}`

**Story / hook.** "A meteorologist logged the weather hour-by-hour for
62 hours. Sunny dominates. Cloudy is second. Four different wet
conditions round out the rest. Can we record the log in fewer bits
than 3 per hour?"

**Symbols + counts.**

| Symbol   | Count |
|----------|-------|
| Sunny    | 32    |
| Cloudy   | 12    |
| Rainy    | 6     |
| Drizzle  | 5     |
| Snow     | 4     |
| Hail     | 3     |

Total: 62 hours.

**Huffman merge trace.**

- Step 1: Hail(3) + Snow(4) → A(7). Queue: {5, 6, 7, 12, 32}.
- Step 2: Drizzle(5) + Rainy(6) → B(11). Queue: {7, 11, 12, 32}.
- Step 3: A(7) + B(11) → C(18). Queue: {12, 18, 32}.
- Step 4: Cloudy(12) + C(18) → D(30). Queue: {30, 32}.
- Step 5: Sunny(32) + D(30) → Root(62).

All merge values (7, 11, 18, 30, 62) distinct from each other and from
all starting frequencies {3, 4, 5, 6, 12, 32}.

**ASCII tree (three-level nested bushiness).**

```
                          (62)
                         /    \
                      Sunny   (30 = D)
                      [0]    /        \
                          Cloudy    (18 = C)
                          [10]      /        \
                                 (7 = A)   (11 = B)
                                 /   \     /    \
                              Hail  Snow Drizzle Rainy
                             [1100][1101][1110][1111]
```

Root branches into a leaf and an internal; that internal branches into
a leaf and an internal; *that* internal branches into two internals,
each of which branches into two leaves. The tree visibly branches on
three distinct levels.

**Code table.**

| Symbol   | Count | Code  | Length |
|----------|-------|-------|--------|
| Sunny    | 32    | 0     | 1      |
| Cloudy   | 12    | 10    | 2      |
| Hail     | 3     | 1100  | 4      |
| Snow     | 4     | 1101  | 4      |
| Drizzle  | 5     | 1110  | 4      |
| Rainy    | 6     | 1111  | 4      |

**Total bits.**
32·1 + 12·2 + 3·4 + 4·4 + 5·4 + 6·4 = 32 + 24 + 12 + 16 + 20 + 24 =
**128 bits**.
Fixed-length (3 bits × 62 hours) = **186 bits**.
**Saved: 58 bits (31.2%).**

**Teaching script.**

1. (30s) "Meteorologist's log. 62 hours. Six weather states." Write
   counts: Sunny 32, Cloudy 12, Rainy 6, Drizzle 5, Snow 4, Hail 3.
2. (15s) "3 bits × 62 = 186 bits naively." Circle 186.
3. (60s) Five merges on the board:
   - Hail + Snow = 7.
   - Drizzle + Rainy = 11. (Emphasize: separate pile.)
   - 7 + 11 = 18.
   - Cloudy + 18 = 30.
   - Sunny + 30 = 62.
4. (45s) Draw full tree; read codes.
5. (45s) Compute 32+24+12+16+20+24 = 128. Circle.
6. (30s) Punchline: "186 → 128, about a third saved. Sunny is half the
   log, Sunny is one bit. Cloudy is an eighth, Cloudy is two bits. The
   four wet conditions are each rare *and roughly equal*, so they all
   get the same code length — four bits. Huffman doesn't care *which*
   wet condition, only that each is individually rare."
7. (35s) Slack.

**Time budget.**

| Segment        | Seconds |
|----------------|---------|
| Setup + story  | 30      |
| Write counts   | 15      |
| State 186 bits | 15      |
| Five merges    | 60      |
| Tree + codes   | 45      |
| Compute 128    | 45      |
| Punchline      | 30      |
| Slack          | 40      |
| **Total**      | **4m 40s** |

**Why rank #2.** Highest savings (31.2%), richest tree (three distinct
code lengths: 1, 2, 4; dramatic depth gap 1-to-4), most nested bushy
shape in the finals. Drops to #2 only because 62 items is heavier on
the board than 33, and Sunny = 32 is an ugly-looking number to recite.
Pick this when the audience is comfortable with arithmetic and you
have the full five minutes — the three-tier code length table is the
best single artifact for the "prediction = compression" payoff.

---

## #3 — Dessert Menu (Round 9)

**Tree shape:** `{2, 2, 2, 3, 3}`

**Story / hook.** "The café tracked dessert sales over one afternoon.
Five kinds, 22 orders. No one kind dominated. Can we still beat 3 bits
per order?"

**Symbols + counts.**

| Symbol   | Count |
|----------|-------|
| Cake     | 7     |
| Brownie  | 6     |
| Cookie   | 5     |
| Pie      | 3     |
| Tart     | 1     |

Total: 22 orders.

**Huffman merge trace.**

- Step 1: Tart(1) + Pie(3) → A(4). Queue: {4, 5, 6, 7}.
- Step 2: A(4) + Cookie(5) → B(9). Queue: {6, 7, 9}.
- Step 3: Brownie(6) + Cake(7) → C(13). Queue: {9, 13}.
- Step 4: B(9) + C(13) → Root(22).

All values distinct (4, 5, 6, 7, 9, 13, 22; frequencies 1, 3, 5, 6, 7
all distinct; 4 from merge equal to no starting count).

**ASCII tree (near-symmetric bushy).**

```
                      (22)
                     /    \
                  (9 = B) (13 = C)
                  /   \    /    \
              Cookie (4=A) Brownie Cake
              [00]  / \   [10]   [11]
                  Tart Pie
                  [010][011]
```

Root branches into *two* internal nodes (B = 9 and C = 13) — the
cleanest bushy split. Both subtrees have depth ≥ 2, so the tree is
bushy rather than spinal.

**Code table.**

| Symbol  | Count | Code | Length |
|---------|-------|------|--------|
| Cookie  | 5     | 00   | 2      |
| Brownie | 6     | 10   | 2      |
| Cake    | 7     | 11   | 2      |
| Tart    | 1     | 010  | 3      |
| Pie     | 3     | 011  | 3      |

**Total bits.**
7·2 + 6·2 + 5·2 + 3·3 + 1·3 = 14 + 12 + 10 + 9 + 3 = **48 bits**.
Fixed-length (3 bits × 22) = **66 bits**.
**Saved: 18 bits (27.3%).**

**Teaching script.**

1. (30s) "22 desserts sold. Five kinds. Counts are pretty close to
   each other — no runaway favorite." Write counts.
2. (15s) "Naive: 3 × 22 = 66 bits."
3. (60s) Four merges:
   - Tart + Pie = 4.
   - 4 + Cookie = 9.
   - Brownie + Cake = 13 (**separate pile forming on the right**).
   - 9 + 13 = 22.
4. (45s) Draw tree, read codes.
5. (30s) Compute 14 + 12 + 10 + 9 + 3 = 48.
6. (30s) Punchline: "48 vs 66 — saved a quarter, even without any one
   dessert dominating. The tree still found structure: Tart and Pie
   were the rarest, so they got three bits. Everyone else got two.
   When counts are close, Huffman quietly gives almost-uniform codes —
   this is the limit case where compression approaches zero."

**Time budget.**

| Segment        | Seconds |
|----------------|---------|
| Setup + story  | 30      |
| Write counts   | 15      |
| State 66 bits  | 15      |
| Four merges    | 60      |
| Tree + codes   | 45      |
| Compute 48     | 30      |
| Punchline      | 30      |
| Slack          | 55      |
| **Total**      | **4m 40s** |

**Why rank #3.** Smallest and least intimidating data (total 22,
largest count 7). Best for an arithmetic-averse audience. The tree is
the most *symmetric* of the three bushy finalists — both children of
the root are internal nodes, depth multiset `{2,2,2,3,3}`. Savings
(27.3%) are real but not flashy. Pick this when you want to demonstrate
that Huffman produces bushy trees *even without* a dominant symbol.

The reason it's not #1: the depth range is only 2–3, which is a
smaller "wow gap" than the 1-to-3 gap in the Lunch Menu, and the
punchline is about the *absence* of a dominant symbol rather than its
presence — a subtler pedagogical moment.

---

## Quick picking guide

- **Default / safest:** #1 (Lunch Menu, `{1,3,3,3,3}`). Cleanest board,
  sharpest story, clearest two-pile geometry.
- **Most dramatic, more arithmetic:** #2 (Weather Log, `{1,2,4,4,4,4}`).
  Best savings, widest depth range, three-tier code table.
- **Balanced counts / arithmetic-shy audience:** #3 (Dessert Menu,
  `{2,2,2,3,3}`). Smallest numbers, most symmetric tree; demonstrates
  that bushiness does not require a dominant symbol.

All three are bushy, tie-free, and fit within 5 minutes with slack.
