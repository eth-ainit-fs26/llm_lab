# Section 3 Student Panel Discussion — Prediction = Compression

## Narrative of the evolution (20 rounds, condensed)

Early rounds surfaced a clear split. Maria (CFO) wanted the 0.53-bit
claim pinned to an explicit calculation and flagged that the intuition
box *announces* a number but never *derives* it in line. Aisha (CEO)
complained that the current prose leaps from "two consultants" to
"$H(p,q)$" in one paragraph, leaving a non-technical reader stranded.
Leo wanted a worked example he could *do*, not just read, and Yuki
pointed out that between Definition 3.x and Theorem 3.x there are four
pages without a single concrete object — his attention died on page 2.

Middle rounds (5–14) were dominated by the proposers. The Storyteller
reframed cross-entropy as a *postage bill*: true entropy is the postage
a perfectly-informed sender pays; KL is the *surcharge* for sending
under a wrong delivery model. The Math Writer conceded that the proof
of \eqref{eq:ce-kl} could stay terse but insisted the Gibbs step be
called out by name so students see *why* KL is non-negative. The
Activity Brainstormer proposed five interactive elements; after
debate, four survived. Final rounds (15–20) negotiated the Python
snippet (Leo wanted it runnable; Maria wanted it auditable) and the
perplexity-to-bytes exercise (Yuki wanted units spelled out three
times).

## Critics' complaints

| Critic | Complaint | Round |
|---|---|---|
| Maria | "0.53 bits" appears without derivation in the intuition box | 1 |
| Maria | No falsifiable yardstick: how would a manager *check* a vendor's cross-entropy claim? | 3 |
| Maria | KL non-negativity is asserted, not shown | 7 |
| Maria | Perplexity 8 $\to$ bytes-saved claim has no worked arithmetic | 13 |
| Aisha | Jumps from analogy to $H(p,q)$ in one paragraph | 1 |
| Aisha | The word "prefix code" is used without explanation | 5 |
| Aisha | "Arithmetic coding" is a black box | 11 |
| Aisha | No sentence a non-technical reader can quote back at a vendor | 17 |
| Leo | No worked example inside the section (only forward ref to appendix) | 3 |
| Leo | Theorem 3.x has proof but no numbers | 9 |
| Leo | Wants to *compute* cross-entropy on something short | 15 |
| Yuki | Four pages of math with no visual | 5 |
| Yuki | "$\log_2(\mathrm{PPL}) =$ bits per token" is stated, not shown | 11 |
| Yuki | Needs a picture of what perplexity 8 "looks like" | 19 |

## Proposers' solutions

| Proposer | Fix | Addresses |
|---|---|---|
| Storyteller | "Postage surcharge" metaphor replaces the generic tax line | Aisha 1 |
| Storyteller | Two-consultants scene expanded into a 3-line role-play card | Aisha 1, Yuki 5 |
| Storyteller | "A model is a dictionary" one-liner for prefix codes | Aisha 5 |
| Math writer | Inline derivation of 0.47 and 0.53 with $H(0.9, 0.1)$ shown | Maria 1 |
| Math writer | Gibbs called out by name in the proof; KL $\ge 0$ given a sentence | Maria 7 |
| Math writer | $\log_2 8 = 3$ bits per token made explicit with units | Yuki 11 |
| Math writer | Bytes-saved computation: (3 − 2.1) bits/token $\times$ $10^6$ tokens / 8 = 112{,}500 bytes | Maria 13, Yuki 19 |
| Brainstormer | Paper compression exercise (biased coin, design prefix code) | Leo 3, 15 |
| Brainstormer | Python snippet: per-token CE of "the cat sat" under two toy LMs | Leo 15, Maria 3 |
| Brainstormer | Bar-chart TikZ of per-token surprise | Yuki 5, 19 |
| Brainstormer | Role-play card for the two consultants | Aisha 1, Yuki 5 |

## Activities that made the cut

1. **"Compress your own message" paper exercise.** Students get the
   distribution $p = (0.5, 0.25, 0.125, 0.125)$ and design a prefix
   code by hand, then compute expected code length vs.\ entropy.
   *Leo: finally something to DO. Yuki: concrete objects on the page.*
2. **Role-play card: the two consultants.** Three lines each, read
   aloud in pairs. *Aisha: plain English re-entry point. Yuki: breaks
   up the math wall.*
3. **Python snippet (6 lines).** Compute per-token cross-entropy of
   "the cat sat" under two toy models; see which one "compresses"
   better. *Leo: runnable. Maria: auditable; she can re-run it.*
4. **Perplexity-to-bytes numerical exercise.** Perplexity 8 on a
   1M-token corpus vs.\ perplexity $\approx 4.29$ (2.1 bpt): compute
   the bytes saved. *Maria: hard number. Yuki: units spelled out.*
5. **TikZ bar chart of per-token surprise** for the same sentence.
   *Yuki: a picture at last.*

## Unresolved tensions

- **Depth vs.\ runway.** Math writer wanted to prove Kraft's
  inequality in a footnote; Aisha vetoed. Compromise: one-sentence
  forward reference to Cover \& Thomas Ch.~5.
- **Arithmetic coding as a black box.** Leo wanted a 3-step
  walkthrough; the section is already long. Deferred to the appendix
  with a pointer.
- **Whether to use $\log_2$ or $\ln$.** Math writer prefers nats for
  gradient math; everyone else prefers bits for the compression
  narrative. Section stays in bits; a footnote notes the conversion.
- **Vendor-benchmark test.** Maria wanted a checklist. Brainstormer
  proposed a "three questions to ask your LLM vendor" callout; it was
  added as a small decision-maker box at section end.
