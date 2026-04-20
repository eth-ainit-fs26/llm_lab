# Top 3 Huffman Teaching Examples

Distilled from the 20-round committee deliberation in
`huffman_committee_log.md`. All three hit the non-trivial, no-background,
≤5-minute target. They are ordered by a combination of: story clarity,
dramatic savings, asymmetry of the tree, and time slack.

---

## #1 — Winter Clothing Shop (from Round 20)

**Story / hook.** "A shop sold 37 items on the first cold day of winter.
Most were coats. Can we encode the sales log in fewer bits than 3 per
item?"

**Symbols + counts.**

| Symbol  | Count |
|---------|-------|
| Coat    | 20    |
| Sweater | 8     |
| Scarf   | 5     |
| Glove   | 3     |
| Hat     | 1     |

Total: 37 items.

**Huffman merge trace.**
- Step 1: Hat(1) + Glove(3) → A(4).
- Step 2: A(4) + Scarf(5) → B(9).
- Step 3: Sweater(8) + B(9) → C(17).
- Step 4: Coat(20) + C(17) → Root(37).

**Tree (ASCII).**

```
                  (37)
                 /    \
              Coat    (17)
              [0]    /    \
                 Sweater  (9)
                  [10]   /   \
                       Scarf (4)
                       [110]/ \
                          Hat  Glove
                        [1110][1111]
```

**Code table.**

| Symbol  | Count | Code  | Length |
|---------|-------|-------|--------|
| Coat    | 20    | 0     | 1      |
| Sweater | 8     | 10    | 2      |
| Scarf   | 5     | 110   | 3      |
| Hat     | 1     | 1110  | 4      |
| Glove   | 3     | 1111  | 4      |

**Total bits.**
20·1 + 8·2 + 5·3 + 1·4 + 3·4 = 20 + 16 + 15 + 4 + 12 = **67 bits**.
Fixed-length encoding (3 bits × 37 items) = **111 bits**.
**Saved: 44 bits (~40%).**

**Teaching script (what the lecturer says and draws).**

1. (30s) "Imagine a shop sold 37 items on the first cold day of winter."
   Write on the board: Coat 20, Sweater 8, Scarf 5, Glove 3, Hat 1.
2. (15s) "If we encoded each with 3 bits (we have 5 products, need at
   least 3 bits), the whole log is 3 × 37 = 111 bits." Circle "111".
3. (15s) "Huffman's idea: repeatedly combine the two smallest piles."
4. (15s) Merge 1: Hat(1) + Glove(3) = 4. Draw a ∧ above Hat and Glove
   with "4" at the apex.
5. (15s) Merge 2: that 4 + Scarf(5) = 9. Draw next layer.
6. (15s) Merge 3: Sweater(8) + 9 = 17.
7. (15s) Merge 4: Coat(20) + 17 = 37. Draw the root.
8. (30s) Read codes off the tree: left = 0, right = 1. Coat = 0,
   Sweater = 10, Scarf = 110, Hat = 1110, Glove = 1111.
9. (30s) Compute bits: 20·1 + 8·2 + 5·3 + 1·4 + 3·4 = 67. Circle "67".
10. (30s) Punchline: "67 vs 111. We cut the log by 40% — and nobody had
    to agree in advance on the code. The frequencies do the work."
11. (10s, optional Q&A buffer) Flag the subtlety: Hat and Glove have
    different counts but the same code length. That's because siblings
    in the tree always have equal-length codes — frequency determines
    depth, not the individual bit pattern.

**Time budget.**

| Segment        | Seconds |
|----------------|---------|
| Setup + story  | 30      |
| Write counts   | 15      |
| State 111 bits | 15      |
| Four merges    | 60      |
| Tree + codes   | 60      |
| Compute 67     | 30      |
| Punchline      | 30      |
| Slack / Q&A    | 60      |
| **Total**      | **5m**  |

**Why rank #1.** Biggest savings (40%), deepest asymmetry among the
five-symbol finalists (depth 1 to 4), cleanest story (everyone has
walked into a shop), most time slack, and exposes the pedagogical
"why do siblings get equal-length codes?" moment cleanly.

---

## #2 — App Review J-Shape (from Round 12)

**Story / hook.** "Look at any app store. Most ratings are 5 stars, a
bunch of haters leave 1 star, and the middle is sparse. Can we encode
22 ratings using fewer bits than naive?"

**Symbols + counts.**

| Symbol | Count |
|--------|-------|
| 5★     | 10    |
| 1★     | 5     |
| 4★     | 4     |
| 3★     | 2     |
| 2★     | 1     |

Total: 22 ratings.

**Huffman merge trace.**
- Step 1: 2★(1) + 3★(2) → A(3).
- Step 2: A(3) + 4★(4) → B(7).
- Step 3: 1★(5) + B(7) → C(12).
- Step 4: 5★(10) + C(12) → Root(22).

**Tree (ASCII).**

```
               (22)
              /    \
            5★     (12)
            [0]   /    \
                1★     (7)
                [10]  /   \
                    4★    (3)
                   [110] /  \
                        2★  3★
                      [1110][1111]
```

**Code table.**

| Symbol | Count | Code  | Length |
|--------|-------|-------|--------|
| 5★     | 10    | 0     | 1      |
| 1★     | 5     | 10    | 2      |
| 4★     | 4     | 110   | 3      |
| 2★     | 1     | 1110  | 4      |
| 3★     | 2     | 1111  | 4      |

**Total bits.**
10·1 + 5·2 + 4·3 + 1·4 + 2·4 = 10 + 10 + 12 + 4 + 8 = **44 bits**.
Fixed-length (3 bits × 22 ratings) = **66 bits**.
**Saved: 22 bits (~33%).**

**Teaching script.**

1. (30s) "Open any app store. Star distributions look like a J — tons
   of 5★, haters at 1★, almost nothing in the middle." Write counts.
2. (15s) "Naive: 3 bits × 22 = 66."
3. (60s) Four merges on the board: 1+2=3, 3+4=7, 5+7=12, 10+12=22.
4. (60s) Draw tree, read codes.
5. (30s) Total: 10+10+12+4+8 = 44. "44 vs 66 — saved a third."
6. (30s) Punchline: "Notice 1★ got a *shorter* code than 4★, even
   though 4★ is a 'higher' rating. The code has nothing to do with how
   many stars the rating shows — only how often it appears."

**Time budget.**

| Segment        | Seconds |
|----------------|---------|
| Setup + story  | 30      |
| Write counts   | 15      |
| State 66 bits  | 15      |
| Four merges    | 60      |
| Tree + codes   | 60      |
| Compute 44     | 30      |
| Punchline      | 30      |
| Slack          | 30      |
| **Total**      | **4m 30s** |

**Why rank #2.** The J-shape distribution is instantly recognizable
(every adult has scrolled Amazon reviews) and the "1★ has a shorter
code than 4★" twist is a priceless pedagogical moment — it forces the
audience to un-couple the *meaning* of a symbol from its *frequency*,
which is exactly the conceptual move the later lecture on
prediction = compression will demand. Lower savings (33% vs 40%) and a
shallower context (only 22 items) are what put it at #2.

---

## #3 — Lunch Survey (from Round 6)

**Story / hook.** "I surveyed 22 students about lunch. Pizza crushed it.
Can we write the survey log with fewer bits than 3 per student?"

**Symbols + counts.**

| Symbol | Count |
|--------|-------|
| Pizza  | 10    |
| Salad  | 5     |
| Burger | 4     |
| Sushi  | 2     |
| Curry  | 1     |

Total: 22 students.

**Huffman merge trace.**
- Step 1: Curry(1) + Sushi(2) → A(3).
- Step 2: A(3) + Burger(4) → B(7).
- Step 3: Salad(5) + B(7) → C(12).
- Step 4: Pizza(10) + C(12) → Root(22).

**Tree (ASCII).**

```
               (22)
              /    \
            Pizza  (12)
            [0]   /    \
                Salad  (7)
                [10]  /   \
                   Burger (3)
                   [110] / \
                       Curry Sushi
                      [1110][1111]
```

**Code table.**

| Symbol | Count | Code  | Length |
|--------|-------|-------|--------|
| Pizza  | 10    | 0     | 1      |
| Salad  | 5     | 10    | 2      |
| Burger | 4     | 110   | 3      |
| Curry  | 1     | 1110  | 4      |
| Sushi  | 2     | 1111  | 4      |

**Total bits.**
10·1 + 5·2 + 4·3 + 1·4 + 2·4 = 10 + 10 + 12 + 4 + 8 = **44 bits**.
Fixed-length (3 bits × 22) = **66 bits**.
**Saved: 22 bits (~33%).**

**Teaching script.**

1. (30s) "Survey: 22 students, 5 lunch options, here are the counts."
2. (15s) "Naive: 3 bits × 22 students = 66."
3. (60s) Merges: 1+2=3, 3+4=7, 5+7=12, 10+12=22.
4. (60s) Tree and codes.
5. (30s) Compute 44 bits. "44 vs 66 — saved a third."
6. (30s) Punchline: "Pizza is half the survey, so Pizza gets one bit.
   Curry is the outlier, so Curry is worth four. Huffman baked that
   into the tree without us touching the algorithm."

**Time budget.**

| Segment        | Seconds |
|----------------|---------|
| Setup + story  | 30      |
| Write counts   | 15      |
| State 66 bits  | 15      |
| Four merges    | 60      |
| Tree + codes   | 60      |
| Compute 44     | 30      |
| Punchline      | 30      |
| Slack          | 30      |
| **Total**      | **4m 30s** |

**Why rank #3.** Identical math and tree to #2, but the story lacks
the "meaning vs frequency" surprise that the review J-shape delivers.
It's the cleanest fallback if the star-rating twist is judged too
slippery for the audience: same tree, same savings, plainer punchline.

---

## Quick picking guide

- If you want **maximum savings and slack**: pick #1 (Winter Clothes).
- If you want a **conceptual aha**: pick #2 (App Reviews) — the
  "rare ≠ less important, just longer code" twist previews the
  prediction-as-compression intuition.
- If the audience is **very arithmetic-averse**: pick #3 (Lunch) — the
  frequencies map to an obvious story without any secondary inference.
