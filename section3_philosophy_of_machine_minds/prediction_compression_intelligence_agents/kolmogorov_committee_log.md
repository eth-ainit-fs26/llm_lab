# Kolmogorov Committee — 20-Round Design Log

Five agents iterate on a set of 10 classroom sequences for a lecture motivating
Kolmogorov complexity (prediction = compression = intelligence). Each round
shows: GENERATOR (proposal), EXECUTOR (delivery), STUDENT_A (math-leaning),
STUDENT_B (verbal-leaning), FEEDBACK SYNTHESIZER (keep/drop/modify).

---

## Round 1

**GENERATOR**
1. `2 4 6 8 10 12` — "even numbers from 2". Tier 1.
2. `1 1 2 3 5 8 13` — "Fibonacci". Tier 2.
3. `A B A B A B A B` — "alternate A, B". Tier 1.
4. `2 3 5 7 11 13 17` — "primes". Tier 2.
5. `1 4 9 16 25 36` — "n squared". Tier 2.
6. `O T T F F S S E N` — "one, two, three, … initials". Tier 4.
7. `3 1 4 1 5 9 2 6` — "digits of pi". Tier 3.
8. `ZYXWVUTSRQ` — "alphabet reversed". Tier 1.
9. `11 21 1211 111221` — "look-and-say". Tier 5.
10. `8 5 4 9 1 7 6 10 3 2` — "numbers 1–10 sorted alphabetically (English)". Tier 5.

**EXECUTOR**
Open with "I'm going to show you ten short sequences. For each one, try to
write down the shortest sentence or formula that produces it." Reveal on the
slide one at a time; 45 seconds per sequence on a visible timer; after each,
collect 2–3 student guesses orally. After all ten, flip the slide to the
word "COMPLEXITY" and say: "Each description you wrote has a length. The
Kolmogorov complexity of a sequence is essentially the shortest such
description — measured in bits, for a fixed universal computer."

**STUDENT_A (math)**
Got #1–#5, #7 instantly. #8 obvious. #9 took 40 s (spotted the recursion).
#10 — no idea, flagged `unfindable`. #6 — flagged `unfindable` (tried
modular arithmetic, got nowhere).

**STUDENT_B (verbal)**
Got #1, #3, #8 instantly. #6 in 20 s ("One Two Three…"). #10 cracked in 50 s
once I said the numbers aloud. #2, #4 recognized by name. #5 saw "squares".
#7 — "looks random, maybe pi digits?" got it. #9 — `unfindable`, looked like
gibberish.

**FEEDBACK SYNTHESIZER**
- Keep #1, #2, #3, #4, #5, #7, #8 — solid tier spread, both students cracked.
- #6 is a great verbal vs. math split — keep it.
- #9 split the same way: A got it, B didn't — keep, but maybe shorten.
- #10 is borderline unfindable for math students. Keep, since verbal gets
  it, but consider: is the gap (very short description, moderate sequence)
  actually huge? Yes: "1–10 sorted alphabetically" is ~30 chars; sequence
  is ~25 chars. Gap is negative — flagged `trivial` in gap terms, though
  the pedagogical twist is fun. Mark for discussion.
- Difficulty distribution: 3 × T1, 3 × T2, 1 × T3, 1 × T4, 2 × T5 — need
  more T3 middle.

---

## Round 2

**GENERATOR**
Keep 1–8, tweak 9, replace 10 with a T3.
1. `2 4 6 8 10 12` — "even numbers". Tier 1.
2. `1 1 2 3 5 8 13 21` — "Fibonacci". Tier 2.
3. `A B A B A B A B` — "alternate A, B". Tier 1.
4. `2 3 5 7 11 13 17` — "primes". Tier 2.
5. `1 4 9 16 25 36` — "n squared". Tier 2.
6. `O T T F F S S E N T` — "initials of one, two, …, ten". Tier 4.
7. `3 1 4 1 5 9 2 6` — "digits of pi". Tier 3.
8. `Z Y X W V U T` — "alphabet reversed". Tier 1.
9. `1 11 21 1211 111221` — "look-and-say, start 1". Tier 5.
10. `M T W T F S S` — "days of the week initials". Tier 3.

**EXECUTOR**
Tighten pacing: 30 s per sequence, not 45. After each reveal, show the
"shortest description" in a smaller font below the sequence, so students
see the gap visually. End with a two-column table on the final slide:
left column the sequence, right column the description, sorted by
description length ascending.

**STUDENT_A**
All cracked except #6 (still not seeing the verbal trick — 90 s, gave up)
and #9 (cracked in 35 s this time since the starting 1 helps).

**STUDENT_B**
Cracked #6 (15 s), #10 (instant). Still stuck on #9. Interesting: got #7
only because "pi" is culturally famous — didn't actually verify digits.

**FEEDBACK SYNTHESIZER**
- #6 is now clearly a verbal-vs-math splitter. Keep it — the lecture can
  make this the moment to say "your prior model of the world is part of
  the description length." `best`.
- #9 is the hardest. Student A got it with the seed; student B cannot.
  Consider reducing to 4 terms so the recursion is visible.
- #10 is strong and fits T3. Keep.
- Still need one more T3. Consider a simple arithmetic-plus-offset or a
  letter-position encoding.
- Overall gap distribution is good; #3 and #8 may be too trivial (raw
  length ≈ description length). Check.

---

## Round 3

**GENERATOR**
Adjust #9 length, add an extra T3 by refining #8.
1. `2 4 6 8 10 12` — "even numbers". T1.
2. `1 1 2 3 5 8 13 21` — "Fibonacci". T2.
3. `ABABABAB` — "AB repeated". T1.
4. `2 3 5 7 11 13 17` — "primes". T2.
5. `1 4 9 16 25 36` — "n²". T2.
6. `O T T F F S S E N T` — "one…ten initials". T4.
7. `3 1 4 1 5 9 2 6` — "π digits". T3.
8. `C E G B D F A` — "letters at positions 3,5,7,…,13 mod 7" (= every
   other letter wrapping). T3. **new**
9. `1 11 21 1211` — "look-and-say". T5.
10. `M T W T F S S` — "weekday initials". T3.

**EXECUTOR**
Use the two-column reveal. Add a running "description-length-so-far"
counter on the side — cumulative chars of the lecturer's descriptions —
to emphasize that short patterns buy a lot of sequence for few words.

**STUDENT_A**
#8 — tried "letter positions are primes" (C=3, E=5, G=7, …) — yes, 3 5 7
11 13 17 — wait, that's the first 7 primes' positions in the alphabet!
Got it in 60 s but with a different description than the intended "every
other odd". The primes reading is shorter. Flag `ambiguous`.
Everything else same as round 2.

**STUDENT_B**
Got #8 only as "music: C major scale" (C-E-G is a triad). Completely
different frame. Flag `ambiguous`.

**FEEDBACK SYNTHESIZER**
- #8 is ambiguous — music, primes, "every other odd" all work. Drop and
  replace.
- Keep the rest. The deck is close to final. Need a clean T3 to replace.

---

## Round 4

**GENERATOR**
Replace #8 with a cleaner T3.
1. `2 4 6 8 10 12` — "evens". T1.
2. `1 1 2 3 5 8 13 21` — "Fibonacci". T2.
3. `ABABABAB` — "AB × 4". T1.
4. `2 3 5 7 11 13 17` — "primes". T2.
5. `1 4 9 16 25 36` — "n²". T2.
6. `O T T F F S S E N T` — "digits in English, first letter". T4.
7. `3 1 4 1 5 9 2 6` — "π digits". T3.
8. `1 2 4 8 16 32 64 128` — "powers of 2". T3. **new**
9. `1 11 21 1211` — "look-and-say". T5.
10. `M T W T F S S` — "weekday initials". T3.

**EXECUTOR**
Consider showing the timer only for the first 3 sequences, then remove
it — students get the rhythm and removing time pressure for the harder
ones (6, 9) gives them space to notice the trick. Keep the descriptions
in small monospace under each sequence at reveal.

**STUDENT_A**
#8 — "powers of 2" — instant. But: it's T2, not T3; it's too easy. Flag
`trivial` in the tier sense (not the description sense).

**STUDENT_B**
Same as A on #8. Rest unchanged. On #9 finally got the pattern: "each
term describes the previous". 70 s.

**FEEDBACK SYNTHESIZER**
- #8 is too easy. Need a genuine middle-difficulty, without ambiguity.
- Consider a sequence whose description is non-obvious but once seen is
  very short.
- Candidate: `1 2 6 24 120 720` (factorials) — still T2-T3.
- Or: `1 2 4 7 11 16 22` (differences are 1, 2, 3, 4, 5, 6) — T3.

---

## Round 5

**GENERATOR**
Swap #8 to a differences-based sequence.
1. `2 4 6 8 10 12`. T1. "evens"
2. `1 1 2 3 5 8 13 21`. T2. "Fibonacci"
3. `ABABABAB`. T1. "AB × 4"
4. `2 3 5 7 11 13 17`. T2. "primes"
5. `1 4 9 16 25 36`. T2. "n²"
6. `O T T F F S S E N T`. T4. "English digit initials"
7. `3 1 4 1 5 9 2 6`. T3. "π digits"
8. `1 2 4 7 11 16 22`. T3. "add 1, 2, 3, …". **new**
9. `1 11 21 1211`. T5. "look-and-say"
10. `M T W T F S S`. T3. "weekday initials"

**EXECUTOR**
For #8, prompt students to write down the *differences* between adjacent
terms. That hint-scaffold is built into the lecture when we get to
"finding a good description often means changing representation". Good
tie-in.

**STUDENT_A**
#8 — saw differences immediately, 15 s. Rest unchanged.

**STUDENT_B**
#8 — 45 s; didn't think of differences, eventually brute-force pattern
match. Still found it. Rest unchanged.

**FEEDBACK SYNTHESIZER**
- Good — #8 now works, and its description is short ("a_n = a_{n-1} +
  n") vs. raw sequence. Keep.
- Still have 3 × T2 — might be heavy. But the three T2s feel different
  (Fibonacci is a recursion, primes is a selector, squares is a
  polynomial) — they hit different *kinds* of descriptions, which is
  pedagogically good. Keep.
- Overall tier spread: T1 × 2, T2 × 3, T3 × 3, T4 × 1, T5 × 1. Need one
  more T5 or a harder T4 for balance.

---

## Round 6

**GENERATOR**
Replace one T2 with a T5 devious sequence.
1. `2 4 6 8 10 12`. T1. evens
2. `1 1 2 3 5 8 13 21`. T2. Fibonacci
3. `ABABABAB`. T1. AB × 4
4. `2 3 5 7 11 13 17`. T2. primes
5. `1 4 9 16 25 36`. T2. n²  ← candidate to drop
6. `O T T F F S S E N T`. T4. digit initials
7. `3 1 4 1 5 9 2 6`. T3. π digits
8. `1 2 4 7 11 16 22`. T3. +1,+2,+3,…
9. `1 11 21 1211`. T5. look-and-say
10. `M T W T F S S`. T3. weekdays

Added candidate to replace #5: `14 23 34 47 62 79` — differences are
9, 11, 13, 15, 17 → arithmetic progression of odds from 9. Description:
"a_n = a_{n-1} + (2n+7)" or equivalently "a_n = n² + 6n + 7". T5.

**EXECUTOR**
Hesitation here: dropping squares would lose a beloved warm-up. Maybe
keep squares and replace one of the T3s instead? Or allow two T5s (6 is
actually T4 — the devious one is currently only #9).

**STUDENT_A**
Proposed replacement `14 23 34 47 62 79`: took 2 min, found it via
second differences. Noted description "n²+6n+7" is elegant.

**STUDENT_B**
Proposed replacement: completely `unfindable`. No handle at all. If it's
in the set, the verbal student walks away with no compression moment for
this slot.

**FEEDBACK SYNTHESIZER**
- Too cruel. A good T5 still needs a punchline that both students can
  appreciate on reveal — even if only one cracks it.
- Keep squares. Consider a different T5 candidate: a sequence that feels
  random but has a cute *meta* description.
- Candidate: `3 3 5 4 4 3 5 5 4` — English word lengths of one, two,
  three, … Similar vibe to #6 but numeric. Probably too close to #6.
- Candidate: `C D E C D E C D E` — musical notes; too trivial.
- Candidate: `61 52 63 94 46 18` — digits of e shuffled? Too obscure.
- Better: keep current set and promote #6 to the devious slot, since
  it's truly tier 4.5. Confirm #9 remains the clear T5.

---

## Round 7

**GENERATOR**
Stabilize: restore #5 (squares), keep #6 and #9 as the hard ones, and
rework one of the trivial T1s into a T2-ish to rebalance.
1. `2 4 6 8 10 12`. T1. evens
2. `1 1 2 3 5 8 13 21`. T2. Fibonacci
3. `AB AB AB AB`. T1. "AB repeated 4×"
4. `2 3 5 7 11 13 17`. T2. primes
5. `1 4 9 16 25 36`. T2. n²
6. `O T T F F S S E N T`. T4. digit initials
7. `3 1 4 1 5 9 2 6`. T3. π digits
8. `1 2 4 7 11 16 22`. T3. +n
9. `1 11 21 1211`. T5. look-and-say
10. `M T W T F S S`. T3. weekdays

**EXECUTOR**
Delivery is clean with this set. Discussion: after the 10-sequence
reveal, open with "raise your hand if you found the pattern for at
least 7 of 10". Expect most hands. Then: "how many chars of English is
your description for each?" Prompt students to compare their
description lengths — introducing the idea that complexity is about the
*shortest* anyone could find, not the first one that works.

**STUDENT_A**
All cracked. Note: #3 description "AB × 4" is 5 chars, raw is 11 chars —
gap is real. Fine.

**STUDENT_B**
All cracked except #9 (still 120+ s). Note: #3 felt dismissive — "of
course AB repeats"; wondered if the set is *too* easy overall.

**FEEDBACK SYNTHESIZER**
- The set is close to final. #3 is genuinely T1, and that's fine — we
  want instant wins at the start.
- Only real concern: is #9 too hard for half the class? We'll keep it,
  but the lecturer should be prepared to walk through it. That's
  pedagogically fine — revealing a surprising short description *is*
  the point.
- Action for round 8: look at description *lengths* and compute the
  complexity gap for each, to make sure the table tells a clean story.

---

## Round 8

**GENERATOR**
Annotate each with raw-length and description-length (chars, spaces
included), and a complexity gap (raw − description).

| # | Sequence | Raw (chars) | Description | Desc (chars) | Gap |
|---|---|---|---|---|---|
| 1 | `2 4 6 8 10 12` | 13 | "evens from 2" | 12 | +1 |
| 2 | `1 1 2 3 5 8 13 21` | 18 | "Fibonacci" | 9 | +9 |
| 3 | `ABABABAB` | 8 | "AB × 4" | 6 | +2 |
| 4 | `2 3 5 7 11 13 17` | 16 | "first 7 primes" | 14 | +2 |
| 5 | `1 4 9 16 25 36` | 14 | "n² for n=1..6" | 14 | 0 |
| 6 | `OTTFFSSENT` | 10 | "English digit initials 1–10" | 27 | -17 |
| 7 | `3 1 4 1 5 9 2 6` | 16 | "first 8 digits of π" | 19 | -3 |
| 8 | `1 2 4 7 11 16 22` | 16 | "a_n = a_{n-1} + n" | 16 | 0 |
| 9 | `1 11 21 1211` | 12 | "look-and-say" | 12 | 0 |
| 10 | `MTWTFSSMT` | 9 | "weekday initials" | 16 | -7 |

**EXECUTOR**
Uh. Several "gaps" are ≤0 in pure chars. This is because *natural
language descriptions are verbose and the sequences are short*. The
lecturer needs to carefully frame: Kolmogorov complexity is measured
relative to a universal computer/formal language, and in a formal
language ("Fibonacci", "primes", "π") each of these descriptions is a
constant-size program that generates arbitrarily many terms. **The
gap grows when we extend the sequence to length N → ∞.** That's the
real punch line.

**STUDENT_A**
Agrees. The table as-shown is misleading for finite short sequences,
but if we add a column "description length for generating N=100 terms",
it's extremely dramatic. Proposes adding such a column.

**STUDENT_B**
Confused by the negative gaps at first. Once the "extend to 100 terms"
framing is added, gets it.

**FEEDBACK SYNTHESIZER**
- Insight: the **teaching frame** is what makes this work, not the
  visible char count of these short sequences.
- Action: for the final deliverable, show two gap columns: "finite"
  and "asymptotic (per term)". Or better, frame as: "the sequence can
  be extended indefinitely; the description does not grow."
- No change needed to the 10 sequences, but the companion script must
  emphasize the asymptotic frame.

---

## Round 9

**GENERATOR**
Minor wording improvements to descriptions to make them crisper.
1. `2 4 6 8 10 12` — "2n". T1.
2. `1 1 2 3 5 8 13 21` — "Fibonacci". T2.
3. `ABABABAB` — "(AB)×4". T1.
4. `2 3 5 7 11 13 17` — "primes". T2.
5. `1 4 9 16 25 36` — "n²". T2.
6. `OTTFFSSENT` — "1st letter of 'one', 'two', …, 'ten'". T4.
7. `3 1 4 1 5 9 2 6` — "digits of π". T3.
8. `1 2 4 7 11 16 22` — "aₙ = aₙ₋₁ + n, a₁=1". T3.
9. `1 11 21 1211` — "look-and-say from '1'". T5.
10. `MTWTFSSMT` — "weekday initials". T3.

**EXECUTOR**
The tighter descriptions are more elegant on the slide. The math-style
formulas look like what we'll introduce formally two slides later, so
students see the continuity.

**STUDENT_A**
#1 description "2n" is 2 chars vs. 13-char raw — now the gap looks
right. Approved.

**STUDENT_B**
Finds "2n" slightly cryptic compared to "even numbers", but after the
lecturer's first example, gets it. Fine.

**FEEDBACK SYNTHESIZER**
- Keep #1 as "2n". The formal notation is on-topic.
- #3 is now "(AB)×4" which is 6 chars vs 8 raw — tiny gap, intentional:
  this is the example where the gap is *small* because the sequence is
  already short. Use it to make the point that complexity is relative
  to description language.

---

## Round 10

**GENERATOR**
Add metadata for pedagogical use — "what does each sequence teach?":

1. `2 4 6 8 10 12` — closed form, simplest possible. T1.
2. `1 1 2 3 5 8 13 21` — recursion / named-pattern recognition. T2.
3. `ABABABAB` — symbolic (non-numeric) repetition; complexity ≠ just math. T1.
4. `2 3 5 7 11 13 17` — definitional pattern ("select primes" is short
   but *computing* primes is work — intro to the idea that short
   description ≠ cheap computation). T2.
5. `1 4 9 16 25 36` — polynomial. T2.
6. `OTTFFSSENT` — **prior knowledge matters**: your model of the world
   is part of the description language. T4.
7. `3 1 4 1 5 9 2 6` — **constants**: π is a short name for an infinite
   string — strong compression. T3.
8. `1 2 4 7 11 16 22` — **representation change**: the trick is to look
   at differences. T3.
9. `1 11 21 1211` — **meta-description**: the sequence describes
   itself. Startling when revealed. T5.
10. `MTWTFSSMT` — **cultural encoding**: weekday names as a finite
    shared vocabulary. T3.

**EXECUTOR**
Excellent — the ten sequences now cover a *curriculum* of compression
ideas: closed form, recursion, symbolic, definitional, polynomial, prior
knowledge, constants, representation change, self-reference, cultural
encoding. The lecturer can use this as a spine.

**STUDENT_A**
Notes the curriculum aspect helps answer "why these ten?". Also
suggests that after the reveal, the lecturer list the 10 ideas on one
slide. Students can match which sequence embodied which idea.

**STUDENT_B**
Agrees. Likes that the exercise covers "your prior model counts" (#6
and #10) explicitly.

**FEEDBACK SYNTHESIZER**
- Set is now conceptually complete. The next ten rounds will be about
  polish: length of sequences, choice of exact terms, ordering for the
  reveal, and testing robustness against alternative descriptions
  (ambiguity stress-test).

---

## Round 11

**GENERATOR**
Test for ambiguity: for each sequence, ask "is there a shorter or
equally-short *different* description that fits?" If yes, we have an
ambiguity bug. Proposed audit:

- #1 `2 4 6 8 10 12`: "2n" vs "a_n=a_{n-1}+2, a_1=2" — the closed form
  is shorter. OK.
- #2 Fibonacci: named pattern is shortest. OK.
- #3 `ABABABAB`: "(AB)×4" vs "A followed by B, repeated". First shorter.
  OK.
- #4 primes: alternatives? "numbers with exactly 2 divisors" — longer. OK.
- #5 squares: "n²" vs "differences are consecutive odds". First shorter. OK.
- #6: ambiguity risk — could someone read it as "random letters"? Only
  before getting the trick. After, the description is unique.
- #7 π: alternative "digits of 3.14159…" — same thing; no conflict.
- #8 `1 2 4 7 11 16 22`: alternative "a_n = (n²-n+2)/2"? Let me check:
  n=1: 1, n=2: 2, n=3: 4, n=4: 7, n=5: 11, n=6: 16, n=7: 22 — yes!
  This is *shorter* ("a_n = (n²-n+2)/2") or longer? Counting: `aₙ =
  aₙ₋₁+n, a₁=1` (19 chars) vs `aₙ = (n²-n+2)/2` (15 chars). Closed
  form is shorter! Flag `ambiguous` — we should switch the intended
  description to the closed form.
- #9 look-and-say: uniquely described by its rule. OK.
- #10 weekdays: unique once prior knowledge is granted. OK.

**EXECUTOR**
Good catch on #8. Let the student "find" either form. The closed form
is the shorter description — so if a math student writes the closed
form, they've won. The pedagogy: "a better description exists". Use
this as a live moment: ask the class which of the two forms they wrote.

**STUDENT_A**
Wrote the closed form initially. Good.

**STUDENT_B**
Wrote the recursive form. Both are valid — this is a natural comparison
moment in class.

**FEEDBACK SYNTHESIZER**
- Update #8's intended description to the closed form `aₙ = (n²-n+2)/2`,
  but teach the moment: "the recursion works; the closed form is
  shorter; the shortest possible description is what Kolmogorov cares
  about."
- Flag #8 as `best` for mid-lecture debate.

---

## Round 12

**GENERATOR**
With #8 description updated, re-check the complexity-gap table.

| # | Sequence | Raw | Description | Desc | Gap |
|---|---|---|---|---|---|
| 1 | `2 4 6 8 10 12` | 13 | "2n" | 2 | +11 |
| 2 | `1 1 2 3 5 8 13 21` | 18 | "Fibonacci" | 9 | +9 |
| 3 | `ABABABAB` | 8 | "(AB)×4" | 6 | +2 |
| 4 | `2 3 5 7 11 13 17` | 16 | "primes" | 6 | +10 |
| 5 | `1 4 9 16 25 36` | 14 | "n²" | 2 | +12 |
| 6 | `OTTFFSSENT` | 10 | "initials of 1..10" | 18 | -8 |
| 7 | `3 1 4 1 5 9 2 6` | 16 | "digits of π" | 11 | +5 |
| 8 | `1 2 4 7 11 16 22` | 16 | "(n²-n+2)/2" | 10 | +6 |
| 9 | `1 11 21 1211` | 12 | "look-and-say" | 12 | 0 |
| 10 | `MTWTFSSMT` | 9 | "weekday initials" | 16 | -7 |

**EXECUTOR**
Now the gaps tell a proper story. The negative-gap sequences (#6, #10)
are *deliberate*: they embody "prior knowledge shrinks description
length only if the description is in a language that knows about
prior". This motivates the "universal computer + input" framing of
Kolmogorov complexity. Brilliant teachable moment.

**STUDENT_A**
Suggests the lecturer make the negative gaps explicit: "descriptions in
plain English can be *longer* than the sequence, because English is
verbose. If we imagine writing these descriptions in a programming
language where 'weekday' is one token, the gap is positive."

**STUDENT_B**
Agrees. Adds: the *asymptotic* gap — extending all sequences to 100
terms — makes every gap positive and dramatic.

**FEEDBACK SYNTHESIZER**
- Add two optional derived columns to the final table: "gap at n=100"
  and "description length as fraction of raw".
- For brevity, the deliverable table will show just the finite gap,
  and the teaching script will explain the asymptotic view.

---

## Round 13

**GENERATOR**
Test ordering. Propose reveal order for maximum pedagogical arc:
1. (T1) `ABABABAB` — gentle opener, symbolic.
2. (T1) `2 4 6 8 10 12` — quick win.
3. (T2) `1 4 9 16 25 36` — squares — "a formula!"
4. (T2) `2 3 5 7 11 13 17` — primes — "a *selector*, not a formula".
5. (T2) `1 1 2 3 5 8 13 21` — Fibonacci — "recursion".
6. (T3) `3 1 4 1 5 9 2 6` — π — "a *constant* hidden in digits".
7. (T3) `1 2 4 7 11 16 22` — differences — "change representation".
8. (T3) `MTWTFSSMT` — weekdays — "cultural prior".
9. (T4) `OTTFFSSENT` — digit initials — "linguistic prior".
10. (T5) `1 11 21 1211` — look-and-say — "self-reference".

**EXECUTOR**
Arc is clean: symbolic → formula → selector → recursion → constant →
representation → prior → prior → self-reference. Each one introduces a
*new kind* of description. This is the lesson spine.

**STUDENT_A**
Approves. Suggests the lecturer explicitly narrate the progression
after reveal: "notice we went from 'pattern = formula' to 'pattern =
selector' to 'pattern = recursion' to …". Compression isn't one thing —
it's a zoo of description-types.

**STUDENT_B**
Approves. Suggests a short pause after #6 (π) to acknowledge "oh!" — the
π reveal is the most viscerally delightful for humanities students.

**FEEDBACK SYNTHESIZER**
- Lock this ordering.
- Also: because it's a classroom exercise, the lecturer should *not*
  reveal the shortest description immediately on slide — let students
  guess first, collect 2-3 proposals, then show.

---

## Round 14

**GENERATOR**
Stress-test with a skeptic: what if a student proposes a *different*
valid description for a sequence?

- #1 (`ABABABAB`): student says "alphabet's first two letters, doubled
  four times". That's 45 chars vs. 6 for "(AB)×4". Their description
  is valid but longer. Teaching moment: *shorter is better.*
- #2 (evens): student says "doubles of 1..6". 16 chars vs. "2n" = 2.
  Same moment.
- #3 (squares): student says "1, then add 3, 5, 7, 9, 11". Works, 24
  chars. Longer than "n²" = 2. Same moment.
- #4 (primes): student says "odd numbers except 1 and 9 and 15 and …".
  Longer + wrong because it includes 2. Wrong answers teach too.
- #5 (Fibonacci): student says "each is the sum of the two before". 30
  chars. Longer than "Fibonacci" = 9 — *if* the student and audience
  share the name. Introduce: complexity depends on shared vocabulary.
- #6 (π): student says "3.14159..." — same thing, just written without
  dots. Fine.
- #7 (differences): student writes the recursion; gets taught the
  closed form.
- #8 (weekdays): student writes "Monday, Tuesday, …". 45 chars vs.
  "weekday initials" = 16. Shorter wins.
- #9 (digit initials): student says "some repeating pattern" — no. Or
  "count up to 10" — still needs the "initials" step. Embraces the
  prior-knowledge lesson.
- #10 (look-and-say): student tries but no prior description — *must*
  be pattern-derived. Celebrate whoever gets it.

**EXECUTOR**
The skeptic test confirms that the intended descriptions are indeed
the shortest. The one risk is #5 — for a student who doesn't know
"Fibonacci", the name is cryptic. But: those students *will* write the
recursive description (30 chars) rather than the name (9 chars) —
this demonstrates "descriptions depend on the vocabulary of your
description language".

**STUDENT_A**
Approves.

**STUDENT_B**
Knows "Fibonacci" from culture. Approves. Notes: this is a gorgeous
illustration that *Kolmogorov complexity is relative to a universal
machine's instruction set*.

**FEEDBACK SYNTHESIZER**
- Set is robust. No changes.

---

## Round 15

**GENERATOR**
Consider accessibility: can we state each sequence in a way that works
in a dark lecture hall, font size 24pt minimum, on a 16:9 slide?

- All 10 sequences ≤ 20 visible tokens. ✓
- Longest: `1 1 2 3 5 8 13 21` = 8 numbers. Fine.
- `OTTFFSSENT` is 10 letters in one block — is that too cryptic? Maybe
  render as `O T T F F S S E N T` (with spaces) for legibility.
- Ditto `MTWTFSSMT` → `M T W T F S S M T`.
- Ditto `ABABABAB` → `A B A B A B A B`.

**EXECUTOR**
Yes — always show letter sequences with spaces so students can track
them. Update notation.

**STUDENT_A**
Fine. Doesn't affect difficulty.

**STUDENT_B**
Prefers spaced letters — slightly easier to read, doesn't reduce
challenge of *finding* the pattern.

**FEEDBACK SYNTHESIZER**
- Final notation update: spaces between letter tokens.
- Raw-length recompute after this is slightly larger, but that's fine.

---

## Round 16

**GENERATOR**
Final-draft table with spaced-letter notation and updated raw lengths.

| # | Sequence | Description | Tier | Raw | Desc | Gap |
|---|---|---|---|---|---|---|
| 1 | `A B A B A B A B` | "(AB)×4" | 1 | 15 | 6 | +9 |
| 2 | `2 4 6 8 10 12` | "2n for n=1..6" | 1 | 13 | 14 | -1 |
| 3 | `1 4 9 16 25 36` | "n² for n=1..6" | 2 | 14 | 14 | 0 |
| 4 | `2 3 5 7 11 13 17` | "first 7 primes" | 2 | 16 | 14 | +2 |
| 5 | `1 1 2 3 5 8 13 21` | "Fibonacci (first 8)" | 2 | 18 | 19 | -1 |
| 6 | `3 1 4 1 5 9 2 6` | "digits of π (first 8)" | 3 | 16 | 21 | -5 |
| 7 | `1 2 4 7 11 16 22` | "(n²−n+2)/2" | 3 | 16 | 10 | +6 |
| 8 | `M T W T F S S M T` | "weekday initials, 9 days" | 3 | 17 | 25 | -8 |
| 9 | `O T T F F S S E N T` | "initials of 1..10 in English" | 4 | 19 | 29 | -10 |
| 10 | `1 11 21 12 11` | "look-and-say from 1" | 5 | 13 | 20 | -7 |

Wait — #2 ("2n") was 2 chars before, now "2n for n=1..6" is 14. The
earlier table had "2n" = 2. Which is honest? In a lecture, the
lecturer would say "just 2n" and the audience fills in the range. So
the *honest* description length is "2n" = 2 chars, because the range
is implicit from the displayed sequence. But to be academically
defensible, the range belongs in the description.

**EXECUTOR**
This is a real pedagogical choice. Recommend: **show the short form**
on slide ("2n", "n²", "Fibonacci", "primes"), and in the companion
script explain that formally the description is the *program* that
produces the sequence — and a program doesn't need an explicit range
if we agree the output is "as many terms as requested". For the
tabulated gap, use the short form.

**STUDENT_A**
Agrees — use the short form; it's closer to formal Kolmogorov
complexity (a self-contained program, of which ranges and lengths are
parameters).

**STUDENT_B**
Agrees.

**FEEDBACK SYNTHESIZER**
- Lock the short-form descriptions for the slide and the final table.

---

## Round 17

**GENERATOR**
Final table with short descriptions and revised gaps.

| # | Sequence | Description | Tier | Raw | Desc | Gap |
|---|---|---|---|---|---|---|
| 1 | `A B A B A B A B` | "(AB)*" | 1 | 15 | 5 | +10 |
| 2 | `2 4 6 8 10 12` | "2n" | 1 | 13 | 2 | +11 |
| 3 | `1 4 9 16 25 36` | "n²" | 2 | 14 | 2 | +12 |
| 4 | `2 3 5 7 11 13 17` | "primes" | 2 | 16 | 6 | +10 |
| 5 | `1 1 2 3 5 8 13 21` | "Fibonacci" | 2 | 18 | 9 | +9 |
| 6 | `3 1 4 1 5 9 2 6` | "digits of π" | 3 | 16 | 11 | +5 |
| 7 | `1 2 4 7 11 16 22` | "(n²−n+2)/2" | 3 | 16 | 10 | +6 |
| 8 | `M T W T F S S M T` | "weekday initials" | 3 | 17 | 16 | +1 |
| 9 | `O T T F F S S E N T` | "English digit initials 1–10" | 4 | 19 | 27 | -8 |
| 10 | `1 11 21 12 11` | "look-and-say" | 5 | 13 | 12 | +1 |

**EXECUTOR**
Now 9 of 10 gaps are positive. #9 is still negative — but that's the
point of #9: prior-knowledge descriptions are *long in English* but
*short in a person's head*. Teaching moment stays.

Also: #10 notation — `1 11 21 12 11` is wrong. Should be
`1 11 21 1211 111221`. Let me fix. The sequence is: 1; one 1 = 11; two
1s = 21; one 2, one 1 = 1211; one 1, one 2, two 1s = 111221. Raw with
spaces: `1 1 1 2 1 1 1 1 2 2 1` — that's 21 chars; too long. Better:
show the four terms as `1, 11, 21, 1211`, with commas, raw = 14 chars.

**STUDENT_A**
Recommends the 4-term version `1, 11, 21, 1211`. The 5th term (111221)
is too visually heavy and gives away the pattern.

**STUDENT_B**
Agrees — 4 terms is gentler. The pattern is still discoverable.

**FEEDBACK SYNTHESIZER**
- Update #10 to `1, 11, 21, 1211`. Raw ≈ 14.

---

## Round 18

**GENERATOR**
Penultimate table.

| # | Sequence | Description | Tier | Raw | Desc | Gap |
|---|---|---|---|---|---|---|
| 1 | `A B A B A B A B` | "(AB)*" | 1 | 15 | 5 | +10 |
| 2 | `2 4 6 8 10 12` | "2n" | 1 | 13 | 2 | +11 |
| 3 | `1 4 9 16 25 36` | "n²" | 2 | 14 | 2 | +12 |
| 4 | `2 3 5 7 11 13 17` | "primes" | 2 | 16 | 6 | +10 |
| 5 | `1 1 2 3 5 8 13 21` | "Fibonacci" | 2 | 18 | 9 | +9 |
| 6 | `3 1 4 1 5 9 2 6` | "digits of π" | 3 | 16 | 11 | +5 |
| 7 | `1 2 4 7 11 16 22` | "(n²−n+2)/2" | 3 | 16 | 10 | +6 |
| 8 | `M T W T F S S M T` | "weekday initials" | 3 | 17 | 16 | +1 |
| 9 | `O T T F F S S E N T` | "English digit initials" | 4 | 19 | 22 | -3 |
| 10 | `1, 11, 21, 1211` | "look-and-say" | 5 | 15 | 12 | +3 |

**EXECUTOR**
Every gap is within a reasonable range now. The distribution of gaps
is itself instructive: two gaps of +11/+12 (tiny formulas for moderate
sequences), mid gaps around +5 to +10, and a single *negative* gap at
#9 that teaches a crucial nuance about priors. This is the ideal
pedagogical distribution.

Script draft, line by line:
> "Look at these ten sequences. Take 30 seconds per sequence. Write
> down the *shortest phrase or formula* that, if I gave it to someone,
> would let them reproduce the sequence."
> [Reveal 1-10, 30s each.]
> "Show of hands — for how many did you find a pattern shorter than the
> sequence itself? How short was your shortest description?"
> [Collect answers.]
> "For #9 — if I said 'weekday initials' in a culture that doesn't use
> the English names — the description is useless. So complexity depends
> on a language. Formally:"
>
> K(x) = length of shortest program, on a fixed universal computer,
> that outputs x.
>
> "When we say prediction = compression = intelligence, we mean: an
> agent that can predict x well has found a short program for x."

**STUDENT_A**
Approves. The final "K(x)" definition lands naturally.

**STUDENT_B**
Approves. Suggests adding a sentence for humanities students: "you've
been doing Kolmogorov complexity your whole life — every time you
summarize a novel, you're compressing."

**FEEDBACK SYNTHESIZER**
- Final set is locked.
- Final teaching script needs the two-paragraph formal transition.

---

## Round 19

**GENERATOR**
No changes to sequences. Final audit:

- Tier distribution: T1 × 2, T2 × 3, T3 × 3, T4 × 1, T5 × 1. Close to
  "2 per tier"; T2 and T3 are slightly heavy at 3 each, but the three
  per tier hit different description-types, which is good.
- Complexity curriculum coverage: closed-form ✓ (1,2,3), selector ✓ (4),
  recursion ✓ (5), constant ✓ (6), representation change ✓ (7),
  cultural prior ✓ (8), linguistic prior ✓ (9), self-reference ✓ (10).
- Gap distribution: 9 positive, 1 negative (#9 intentionally).
- Ambiguity: all cleared in round 11.
- Timing: 30s × 10 = 5 min of guessing + 5 min of discussion + 2 min
  formal definition = 12-min classroom module. Fits a lecture slot.

**EXECUTOR**
All constraints satisfied. Ready for final write-up.

**STUDENT_A**
No complaints. Recommends the class sees the closed form for #7 as a
*surprise* — "you thought recursion, and the polynomial is shorter" —
as a teaser for the Kolmogorov punchline.

**STUDENT_B**
Recommends adding one sentence after the exercise: "the best
compressor is the best predictor — and that's what our big neural
nets are trying to do."

**FEEDBACK SYNTHESIZER**
- Close. Round 20 is for final sign-off and confirmation of the
  "tier to sequence" binding.

---

## Round 20

**GENERATOR — FINAL**

| # | Sequence | Shortest Description | Tier |
|---|---|---|---|
| 1 | `A B A B A B A B` | "(AB)*" | 1 |
| 2 | `2 4 6 8 10 12` | "2n" | 1 |
| 3 | `1 4 9 16 25 36` | "n²" | 2 |
| 4 | `2 3 5 7 11 13 17` | "primes" | 2 |
| 5 | `1 1 2 3 5 8 13 21` | "Fibonacci" | 2 |
| 6 | `3 1 4 1 5 9 2 6` | "digits of π" | 3 |
| 7 | `1 2 4 7 11 16 22` | "(n²−n+2)/2" | 3 |
| 8 | `M T W T F S S M T` | "weekday initials" | 3 |
| 9 | `O T T F F S S E N T` | "English digit initials 1–10" | 4 |
| 10 | `1, 11, 21, 1211` | "look-and-say" | 5 |

**EXECUTOR — FINAL SCRIPT**
> "I'm going to show you ten short sequences. For each, write the
> shortest description — in English or math — that would let a
> classmate reproduce it. 30 seconds each."
>
> [Reveal #1 through #10, 30 s each. For each, after the timer,
> accept two student proposals orally, then reveal the intended
> shortest description on the slide.]
>
> "Now look at the descriptions. For #2, two characters ('2n')
> produced a sequence of thirteen characters. For #5, 'Fibonacci'
> produced infinitely many — the name stands in for a rule that works
> forever. For #9, though, 'English digit initials' was *longer* than
> the sequence — because the description language didn't share our
> prior."
>
> [Transition slide: K(x) = length of shortest program, on a fixed
> universal computer, that outputs x.]
>
> "This is Kolmogorov complexity. And the thesis of this lecture —
> **prediction = compression = intelligence** — is that whenever
> someone or something predicts a sequence well, they've found a
> short program for it. Shannon formalized the information in a
> sequence; Solomonoff used shortest programs as universal priors;
> Kolmogorov defined the ultimate complexity measure. Every modern
> neural language model sits inside this lineage."

**STUDENT_A (FINAL)** — approved.

**STUDENT_B (FINAL)** — approved. Notes one last insight: "#6 and #9
are the most memorable *because* they cost me time. I'll remember the
definition of K better because those were hard."

**FEEDBACK SYNTHESIZER — FINAL**
- All 10 sequences locked.
- Tier spread: T1 × 2, T2 × 3, T3 × 3, T4 × 1, T5 × 1.
- Curriculum coverage: closed-form, selector, recursion, constant,
  representation-change, cultural prior, linguistic prior,
  self-reference — all hit.
- Ambiguity: resolved.
- Gap: 9 positive, 1 instructively negative.
- Committee signs off.

End of log.
