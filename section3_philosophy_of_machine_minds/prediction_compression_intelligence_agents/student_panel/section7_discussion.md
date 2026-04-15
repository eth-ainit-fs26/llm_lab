# Section 7 discussion — "What this buys us for LLMs"

Twenty rounds of panel discussion on the LLM payoff section: Hutter Prize,
scaling laws, GPT-2/GPT-4 bits-per-character, emergent capabilities, and
the final working-equivalence chain.

## Narrative

The panel opened with Maria (CFO) pushing hard on the Hutter claim: "You
tell me prize money exists. What prize? How much? Who won last? Where is
the $/bit curve that would let me price a compression gain?" Aisha (CEO)
piled on — she had read the intuition box twice and still could not
explain "cross-entropy" to her board. She wanted a one-sentence gloss
that would survive a coffee chat. Leo, bored by the prose, demanded a
worked example he could actually do on paper. Yuki drifted away at the
sentence "operationalised this equivalence" and asked, bluntly, "what
does GPT-2 doing $1.2$ bits per character *look like*?"

Across the even rounds, the Storyteller countered with the
two-vendors-same-product analogy (one pitches a language model, the other
pitches a Wikipedia compressor — same binary, different KPIs) and a
last-mile parable: closing the gap from $92\%$ to $98\%$ of the entropy
floor is not a $6$-point improvement, it is a price curve that bends
skyward. The Math writer defended the chain of theorems but conceded
three prose changes: drop "operationalised", gloss KL before invoking
it, and attach a perplexity-to-bits conversion in line. The Activity
Brainstormer pitched six activities; the panel converged on four.

By round 20 the section had a sharper spine: (i) define residual and
arithmetic coding with a numerical micro-example, (ii) give the Hutter
leaderboard as a live artefact, (iii) show the last-mile cost curve
visually, (iv) let students do the perplexity$\to$bits conversion on a
worksheet, and (v) close with the working-equivalence chain re-stated
in Aisha's plain English before the formal version.

## Critics' complaints

| # | Critic | Complaint | Round |
|---|--------|-----------|-------|
| C1 | Maria | "Prize money" is vague --- name the amount, the corpus size, the current record. | 1 |
| C2 | Maria | No $/bit curve. I cannot compare a $0.1$-bit gain to a $10$M compute spend. | 3 |
| C3 | Maria | "By \cref{thm:ce-code}" is not falsifiable --- give me an experiment that could break the equivalence. | 5 |
| C4 | Maria | $92\% \to 98\%$ is stated but the cost asymmetry is not quantified. | 7 |
| A1 | Aisha | "Cross-entropy" appears six times before it is glossed in English. | 1 |
| A2 | Aisha | "KL divergence" is introduced as "the same tax formalised" --- what tax? I missed the earlier sentence. | 3 |
| A3 | Aisha | "Conditional entropy rate $\overline{H}(p)$" --- this is outside the intuition box but I still read it. | 9 |
| A4 | Aisha | The three upshots at the end are good but buried. Put them up top. | 11 |
| L1 | Leo | Where is the worked example I can redo? "Roughly $1.2$ bits" is told, not shown. | 1 |
| L2 | Leo | I want to see an arithmetic coder actually shrink a file. | 5 |
| L3 | Leo | Perplexity $32$ --- show me the conversion. | 13 |
| Y1 | Yuki | Two paragraphs of prose between concrete handles. | 3 |
| Y2 | Yuki | "Out-of-domain modalities" --- what does that mean in a picture? | 7 |
| Y3 | Yuki | The equivalence chain is three abstractions stacked. I need a picture. | 15 |

## Proposers' solutions

| # | Proposer | Solution | Addresses |
|---|----------|----------|-----------|
| S1 | Storyteller | Two-vendors parable: "language model" vs "Wikipedia compressor" --- same binary. | A1, A4 |
| S2 | Storyteller | Last-mile parable: climbing Everest, the final $200$m cost more than the first $8000$. | C4, Y3 |
| S3 | Storyteller | Hutter Prize as an open bounty board; frame it like an X-Prize. | C1 |
| M1 | Math writer | Inline perplexity$\to$bits: $\log_2 32 = 5$ bits/token. One line, done. | L3, A2 |
| M2 | Math writer | Add a footnote anchoring Hutter numbers: $500{,}000$\euro{} bounty, $1$~GB \texttt{enwik9}, current record $\approx 0.113$ bpc (Bellard 2024). | C1, C2 |
| M3 | Math writer | Restate the working equivalence once in plain English before the formal arrow diagram. | A1, A4 |
| B1 | Brainstormer | Hutter-Prize bingo: project the leaderboard, students predict the 2030 winner. | C1, Y1 |
| B2 | Brainstormer | Python snippet: gpt2-small $+$ arithmetic coder on $10$~KB Wikipedia; report bytes in vs bytes out. | L2, C3 |
| B3 | Brainstormer | TikZ last-mile cost curve: compute vs bits-below-floor, log-log. | C4, Y3 |
| B4 | Brainstormer | Worksheet: perplexity $32 \to 5$ bits/token; savings on $100$~GB. | L3, L1 |

## Activities chosen (4)

1. **Hutter Prize bingo.** Show the live leaderboard. Each student picks
   a 2030 winner (transformer, SSM, diffusion, hybrid, symbolic, "none
   --- plateau"). Helps **Yuki** (concrete artefact) and gives **Maria**
   the numbers she asked for.
2. **Python snippet: LLM as compressor.** Ten-line \texttt{gpt2} +
   arithmetic-coder script; run on $10$~KB \texttt{enwik8} snippet;
   compare bytes-in vs bytes-out vs \texttt{gzip}. Helps **Leo**
   (hands-on) and answers **Maria**'s falsifiability demand.
3. **Perplexity-to-bits worksheet.** Convert perplexity $\{8, 32, 128\}$
   to bits-per-token. Compute storage savings on a $100$~GB corpus for
   each. Helps **Leo** and **Aisha** (she can now say the sentence).
4. **Two-vendors skit / TikZ last-mile plot.** Five-minute role-play
   plus a projected log-log plot of "cost per bit below Shannon floor".
   Helps **Yuki** (picture) and **Maria** (cost curve).

## Unresolved tensions

- **The $/bit curve is still soft.** Nobody on the panel has public
  dollar-per-bit data for frontier models. The revised section flags
  this as a live research question rather than pretending to resolve
  it. Maria noted her dissent.
- **"Emergent capabilities" framing.** The Math writer wanted to weaken
  the claim ("consistent with theory" rather than "predicted by
  theory"); the Storyteller wanted the punchier version. Compromise:
  the intuition box keeps "the theory predicting itself", the formal
  prose downgrades to "consistent with".
- **Multimodal ceiling.** The claim that "progress on pure language
  tasks must slow" is defended by Math writer but Maria wants a date.
  None given; flagged.
