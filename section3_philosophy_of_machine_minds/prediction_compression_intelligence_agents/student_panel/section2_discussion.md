# Section 2 (Shannon Prelude) — Condensed Panel Discussion

## Narrative of how the discussion evolved

The 20-round exchange opened with Aisha and Yuki hammering the opening
intuition box: the LA-vs-Zurich forecaster analogy was vivid but died
before it became a number, and the leap from "yes/no questions" to
$H=1$ bit to "half a bit per flip" had no ladder. Maria and Leo then
turned on the math core: Maria wanted Kraft and Gibbs motivated by
something falsifiable (a bill, a bandwidth floor), Leo simply stopped
reading at the Gibbs proof ("$\ln x \le x-1$" appeared with no
picture). By round 7 the critics converged on a shared complaint: the
section states theorems but never lets the reader *do* anything.

The proposers responded in layers. The Storyteller reframed the
opening as a weather-forecaster who gets paid per bit transmitted.
The Math writer defended keeping Kraft/Gibbs but agreed to add a
binary-tree TikZ and a motivated lead-in. The Activity Brainstormer
contributed four concrete classroom moves — a coin-bet game, a phone
lock-screen entropy estimate, a Huffman-by-hand worksheet, and a
six-line Python snippet — which the others hooked to the existing
$H=7/4$ example. By round 20 the group had an agreed structure:
intuition with numbers up front, a TikZ prefix-tree beside Kraft, a
worked "bias-7/8 coin" example to rescue the half-bit claim, and an
activity box at the end of the section that sends students home with
code.

## Critics' complaints

| Phrase / sentence flagged | By whom | Why |
|---|---|---|
| "average number of yes/no questions ... is the entropy" | Aisha | Jargon ("average", "yes/no questions", "entropy") stacked in one sentence; no retail handle. |
| "on average you need only about half a bit per flip" | Yuki | Claim arrives with no derivation; thread breaks because number is not linked to anything concrete. |
| Gibbs proof line: "Using $\ln x \le x-1$..." | Leo | Attention died here. No picture, no motivation, algebra dump. |
| "every storage bill, every bandwidth bill..." | Maria | Slogan without a unit. What is the actual number for a retailer's logs? |
| Kraft lemma stated cold after the definition of prefix code | Leo | Wall of symbols; needs a tree picture before the inequality. |
| "$\mathcal{A} = \{a_1,\dots,a_K\}$" setup paragraph | Yuki | Two abstract paragraphs before any concreteness. |
| Source-coding theorem proof sketch | Maria | Uses Gibbs on a normalised $\tilde q$ with no intuition for why that trick works. |
| Example \ref{ex:h4} buried at the end | Aisha, Leo | The one concrete thing in the section is the *last* thing; should arrive earlier. |
| "which would itself be news" | Maria | Cute but unfalsifiable as written; needs the actual lower bound number (~0.6--1.3 bits/char). |
| No exercise, no code, no worksheet anywhere | Leo, Yuki | Passive reading for three pages. |

## Proposers' solutions

| Solution | Proposer | Targets |
|---|---|---|
| Rewrite opening intuition with the bias-7/8 coin computed inline ($H\approx 0.544$ bits) | Storyteller + Math writer | Yuki (half-bit claim), Aisha (jargon). |
| Add a "What a decision-maker actually pays" paragraph citing the ~1 bit/char English floor (Shannon 1951; Cover--Thomas) | Math writer | Maria (falsifiability). |
| Insert TikZ binary prefix-tree figure next to Kraft, with the 4-symbol code drawn on it | Activity Brainstormer | Leo (Kraft wall), Yuki (abstract setup). |
| Move \cref{ex:h4} up to immediately after the definition; keep a short expanded version at the end | Storyteller | Aisha, Leo (concreteness earlier). |
| Add a margin "picture-proof" of $\ln x \le x-1$ (tangent at 1) before Gibbs | Math writer | Leo (died at Gibbs). |
| Weather-forecaster roleplay: LA distribution vs Zurich distribution, compute both entropies | Storyteller | Aisha (retail handle), Yuki (cash out in numbers). |
| Four activity boxes (coin-bet, lock-screen, Huffman worksheet, Python snippet) | Activity Brainstormer | Leo, Yuki (passivity). |
| Funny aside on the "0.3 bits/char vendor" as the "cold-fusion of compression" | Storyteller | Maria (gives the slogan a testable edge). |

## Activities integrated (and why they rescue Leo / Yuki)

1. **Guess-the-next-flip bet game (Activity 2.1).** Students bet
   play-money on a biased coin; the house takes
   $-\log_2 p(\text{outcome})$ chips per round. *Leo:* a scoreboard
   he can compute. *Yuki:* the bits become chips, a concrete handle.
2. **Phone lock-screen entropy (Activity 2.2).** Each student
   estimates the entropy of their own 4--6 digit PIN against a
   realistic prior (birthday-heavy). *Yuki:* personally concrete.
   *Leo:* a worked number at the end.
3. **Huffman-by-hand worksheet (Activity 2.3).** Build the code for
   the 4-symbol alphabet by merging lowest-probability pairs; verify
   $L = H = 1.75$. *Leo:* pencil-and-paper payoff. *Yuki:* the
   prefix tree becomes a physical drawing.
4. **Six-line Python entropy snippet (Activity 2.4).** Compute the
   entropy of any string; students run it on the first paragraph of
   their favourite novel and on a genome snippet. *Leo:* code he can
   execute. *Yuki:* numbers for two inputs he already cares about.

A fifth option (weather-forecaster roleplay) was folded into the new
opening intuition rather than becoming its own box, to keep the
activity count bounded.

## Unresolved tensions

- **Depth of the Gibbs proof.** Math writer wants to keep the full
  proof; Leo wants it in an appendix. Compromise in the revised
  file: keep the proof, add a margin figure, add a one-line
  "why we care" preamble. Revisit if the pilot run shows Leo still
  drops off.
- **Length.** Section roughly doubles in length. Aisha warned that
  executives will not read past page two; Math writer countered that
  this is the *notes*, not the deck, and the deck can cherry-pick.
  Left as-is; revisit when the deck is updated.
- **Whether to name cross-entropy here.** Maria argued cross-entropy
  deserves its own definition because it reappears in Section 3;
  Math writer preferred to defer. Deferred, with a forward-reference
  comment in the source.
- **Vendor-claim footnote.** Storyteller's "cold-fusion of
  compression" line is funny but specific; Maria flagged it as
  possibly libellous if a real vendor is named. Kept generic.
