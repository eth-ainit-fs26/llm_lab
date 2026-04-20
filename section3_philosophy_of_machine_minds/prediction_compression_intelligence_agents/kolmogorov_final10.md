# Kolmogorov Classroom Exercise — Final 10 Sequences

Ten short sequences for a classroom exercise that motivates the formal
definition of Kolmogorov complexity. The reveal order below is also the
teaching order — it walks the class through nine distinct *kinds* of
short description (closed form, selector, recursion, constant,
representation change, cultural prior, linguistic prior,
self-reference).

## Final table

| # | Sequence | Shortest Description | Tier | Raw length (chars) | Description length (chars) | Complexity gap |
|---|---|---|---|---|---|---|
| 1 | `A B A B A B A B` | `(AB)*` | 1 | 15 | 5 | +10 |
| 2 | `2 4 6 8 10 12` | `2n` | 1 | 13 | 2 | +11 |
| 3 | `1 4 9 16 25 36` | `n²` | 2 | 14 | 2 | +12 |
| 4 | `2 3 5 7 11 13 17` | `primes` | 2 | 16 | 6 | +10 |
| 5 | `1 1 2 3 5 8 13 21` | `Fibonacci` | 2 | 18 | 9 | +9 |
| 6 | `3 1 4 1 5 9 2 6` | `digits of π` | 3 | 16 | 11 | +5 |
| 7 | `1 2 4 7 11 16 22` | `(n²−n+2)/2` | 3 | 16 | 10 | +6 |
| 8 | `M T W T F S S M T` | `weekday initials` | 3 | 17 | 16 | +1 |
| 9 | `O T T F F S S E N T` | `English digit initials 1–10` | 4 | 19 | 27 | −8 |
| 10 | `1, 11, 21, 1211` | `look-and-say` | 5 | 15 | 12 | +3 |

Gap = Raw length − Description length. Nine of the ten gaps are
positive; sequence #9 is *intentionally* negative, to motivate the
point that Kolmogorov complexity is defined relative to a fixed
description language (a universal computer) — and that plain English
is a verbose description language. The lecturer should name this
explicitly when revealing #9.

## Teaching script

Open the exercise by saying: "I'm going to show you ten short
sequences. For each one, write the *shortest phrase or formula* — in
English or math — that would let a classmate reproduce it. You get
thirty seconds per sequence." Reveal the ten in the table's order,
running a visible 30-second timer for each one. After each sequence,
accept two student proposals orally before revealing the intended
shortest description on the slide. Sequences #1–#5 deliver quick wins
that build confidence; #6 and #7 introduce the ideas of a *named
constant* and of *changing representation*; #8 and #9 force the class
to notice that "weekday initials" and "English digit initials"
compress the sequence only because the audience already shares a
cultural and linguistic prior; #10 (look-and-say) delivers the
pedagogically climactic "self-referential" description that almost no
one finds unaided, but which feels inevitable once revealed.

Transition into the formal definition by holding up the table of raw
versus description lengths and saying: "Each description you wrote has
a length. The Kolmogorov complexity of a string x is the length of the
shortest program, on a fixed universal computer, that outputs x. For
#2, the 2-character program `2n` produced a 13-character sequence —
and the same program would produce two hundred terms without growing.
For #9, the description was *longer* than the sequence only because
English is a verbose programming language; in the language of your own
brain, 'the digits in English' is a very short program. This is the
basis of the thesis of today's lecture — **prediction = compression =
intelligence**. Shannon taught us how much information a sequence
carries; Solomonoff used shortest programs as universal priors for
induction; Kolmogorov formalized the complexity measure; and every
modern neural language model — when it predicts the next token well —
is, in effect, searching for a short program that fits the data."
