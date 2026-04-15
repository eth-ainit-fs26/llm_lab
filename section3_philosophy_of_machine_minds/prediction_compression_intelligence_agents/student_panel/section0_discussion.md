# Section 0 (Preface + §1) — Agent Panel Discussion Synthesis

## Narrative of the 20 rounds

The early rounds (1–6) circled around one complaint: the Preface and §1
announce a grand thesis ("prediction = compression = intelligence") but
never give the reader a single concrete number, object, or falsifiable
prediction to hang the claim on. Maria kept demanding a falsifiable
test; Aisha bounced off "Solomonoff," "AIXI," "coordinate-free"; Leo
lost interest at the second sentence of the Preface ("two tracks at
once"); Yuki wandered off during the "three currencies, three exchange
rates" metaphor because no exchange rate was ever quoted. Proposers
responded with a concrete opener (the 1 GB Wikipedia file that becomes
~150 MB when a good language model compresses it), a worked bits-to-
dollars calculation, and two small activities.

Rounds 7–14 moved to structural fixes. The Storyteller pushed a
"three-friends-at-a-bar" framing (a stenographer, a zipper, a chess
player turn out to be the same person). The Math writer defended the
chain of theorems but conceded that the Preface should not mention
`\cref` machinery at all. The Brainstormer proposed a physical-prop
demo (guess-the-next-letter with a deck of index cards) and a
five-line Python snippet that measures a model's bits-per-character on
a paragraph the reader pastes in. Rounds 15–20 tightened: critics
agreed the rewrite must (i) lead with a number, (ii) define the three
words before using them, (iii) give the falsification clause its own
sentence, and (iv) replace the "two tracks" meta-paragraph with a
one-line instruction box.

## Critics' consolidated complaints

| # | Flagged text | Who | Why |
|---|---|---|---|
| C1 | "written on two tracks at once, for two readers travelling together" | Leo | Dropped off here; meta-preamble with zero payoff. |
| C2 | "Each Intuition box cross-references the nearest definition or theorem via \cref{sec:why}\ldots" | Aisha | `\cref` is a LaTeX command leaking into prose; she skipped the sentence. |
| C3 | "prediction, compression, and intelligence are, under precise definitions, the same operation" | Maria | No falsification condition stated; reads like a slogan. |
| C4 | "three currencies --- bits saved, dollars earned, capability on held-out tasks --- and three exchange rates" | Yuki | Mind wandered to actual FX rates; no rate was ever quoted. |
| C5 | "Solomonoff's universal prior ... Hutter's AIXI" (first citation block) | Aisha | Five unknown names in two sentences; skipped. |
| C6 | "being good at thinking" | Maria | "Thinking" is undefined; cannot be measured. |
| C7 | "minimising that one number is not a narrow engineering goal --- it is a proxy for general intelligence" | Maria | Huge claim, no caveat yet; demands the caveat sentence earlier. |
| C8 | No worked numbers anywhere in §1 | Leo | Abstract prose >3 paragraphs without a concrete example. |
| C9 | "up to translation" | Aisha | Mathematician's hedge; opaque. |
| C10 | "coordinate-free notion" | Aisha, Yuki | Jargon; neither knows what it means here. |
| C11 | Thesis stated three times (Preface, opening intuition, §1 body) | Leo | Redundant; bored by repetition. |
| C12 | Caveat ("real predictors are not perfect") buried at end of intuition box | Maria | Should be promoted — it is the falsifiability hook. |

## Proposers' consolidated solutions

| Addresses | Solution | Proposer |
|---|---|---|
| C1, C11 | Cut the "two tracks" paragraph. Replace with a 3-line **How to read** micro-box: "Skim orange boxes = manager track. Read everything = student track." | Storyteller |
| C2 | Remove `\cref` from the Preface entirely; refer to "the boxes below" in English. | Math writer (concession) |
| C3, C6, C7, C12 | Add an explicit **Falsifiable prediction** paragraph: "If the equivalence holds, a model with lower bits-per-character on held-out English should score higher on MMLU/BIG-Bench at matched parameter count. If it does not, the equivalence is wrong or leaky." | Maria-driven, drafted by Math writer |
| C4 | Replace currency metaphor with a worked table: one model's actual BPC, its compression ratio, the $/GB saved at a named cloud price, and its held-out accuracy. | Brainstormer + Math writer |
| C5, C9, C10 | First mention of each name gets a one-clause gloss in parentheses. Drop "up to translation" and "coordinate-free" from the intuition box; keep them in the body only. | Storyteller |
| C8 | New worked example: "Wikipedia is ~19 GB of text; gzip gets it to ~5 GB; a 7B-parameter LM gets it to ~3 GB; Hutter Prize benchmark is ~1.1 GB." | Brainstormer |
| C1 | New opener: a 90-word story of a stenographer, a zip program, and a chess player who discover they are the same person. | Storyteller |
| — | A TikZ triangle figure: three vertices (Predict, Compress, Act), three edges labelled with the theorem that bridges them. | Brainstormer |

## Activities list (Brainstormer)

| Activity | How it helps Leo / Yuki |
|---|---|
| **A1 — Guess the next letter.** Deck of index cards with a short English sentence, one letter per card. Students guess card $n+1$ before it is flipped; tally hits. Then discuss: your hit rate is a lower bound on a language model's. | Leo: physical, tactile, finishes in 4 minutes. Yuki: immediate numeric payoff (your hit rate). |
| **A2 — Compress your own paragraph.** Paste a paragraph you wrote into a 5-line Python snippet (provided) that reports bits-per-character under gzip and under a small LM. Compare. | Yuki: concrete numbers in under 60 seconds. Leo: something runs and prints a number. |
| **A3 — The \$/GB bet.** Given a cloud storage price (\$0.023/GB-month) and a model that cuts your logs in half, compute the annual saving for 100 TB. Then ask: would you pay a \$2M licence fee for that model? | Maria-facing but wakes Leo: it is a money question. |
| **A4 — Falsification worksheet.** One-page table: column 1 = the equivalence claim, column 2 = what observation would refute it, column 3 = what observation would be consistent but not confirm it. Students fill it in. | Maria's demand satisfied; Leo gets a finite task. |
| **A5 — Three-friends-at-a-bar reading.** Read the opener story aloud; ask the class to guess which friend is which (prediction/compression/intelligence) before the reveal. | Leo: story, 2 minutes. Yuki: concrete characters to anchor abstract words. |

## Unresolved tensions

- **How much to say about AIXI in §1.** Math writer wants the name in; Aisha wants it deferred to §4. Compromise in the rewrite: name appears once, parenthetically glossed, with a forward pointer.
- **Whether "intelligence" should be replaced everywhere by "capability on held-out tasks."** Maria wants the swap; Math writer refuses (loses Solomonoff's point). Compromise: use "intelligence (operationalised as held-out task performance)" on first use and "intelligence" thereafter.
- **Length.** Leo wants §1 shorter; Brainstormer's additions make it longer. User has said long is fine; we chose depth.
