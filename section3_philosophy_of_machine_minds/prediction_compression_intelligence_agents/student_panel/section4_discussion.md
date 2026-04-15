# Section 4 Discussion: Kolmogorov complexity

## Narrative

Twenty rounds of panel review on the Kolmogorov-complexity section. The
text is mathematically solid but, in the critics' view, sprints from
recipe-over-the-phone analogy to a Berry-paradox proof in fewer than two
pages. Maria (CFO) wants falsifiable numbers instead of gestures. Aisha
(CEO) wants a one-breath answer to "so what?" before any theorem. Leo
and Yuki, the undergraduates, drift between the definition and the
uncomputability proof because nothing concrete anchors the middle.

The proposers converged on three moves: (1) expand the intuition box
with a zip-versus-true-K scoreboard and a named worked example (the
million-bit coin-flip file); (2) insert two activities before the
invariance theorem so Yuki has a concept-to-concrete link, and a third
activity after uncomputability to keep Leo awake; (3) rewrite the Berry
proof with a dramatised "smallest number not describable in twenty
words" preamble, then let the formal proof stand unchanged (Math
writer's non-negotiable). The snake-oil sidebar grows into a
"compression bingo" worksheet.

## Critics' complaints

| Round | Critic | Complaint |
|------:|--------|-----------|
| 1 | Maria | "shortest program" is prose; no numbers on how short in practice. |
| 3 | Aisha | Intuition box buries the takeaway under three paragraphs. |
| 5 | Leo | The "sprinkles" example is cute but I want to try it. |
| 7 | Yuki | Two pages between the definition and any concrete bit-count. |
| 9 | Maria | The invariance footnote says "hundreds to low thousands of bits" without showing the arithmetic. |
| 11 | Aisha | "Elias delta" in the Berry proof loses every non-specialist. |
| 13 | Leo | No picture. Two theorems back-to-back with no worked numbers. |
| 15 | Yuki | Why do I care that $K$ is uncomputable if I have gzip? |
| 17 | Maria | Snake-oil sidebar asserts 40\% is marketing but shows no counter-example calculation. |
| 19 | Aisha | Needs a one-line "what a manager does Monday morning" close. |

## Proposers' solutions

| Round | Proposer | Solution |
|------:|----------|----------|
| 2 | Storyteller | Open with the "twin USB sticks" image --- same 8GB, one zips to 200MB, one to 8GB --- before any math. |
| 4 | Activity Brainstormer | Activity 1: Shortest-recipe game (Leo, Yuki). |
| 6 | Math writer | Keep the Berry proof; add a dramatised Berry-paradox preface box. |
| 8 | Storyteller | Replace "sprinkles" with the twin-USB prop; keep sprinkles as one sentence. |
| 10 | Activity Brainstormer | Activity 2: gzip-vs-K scoreboard bar chart. |
| 12 | Math writer | Footnote upgrade: actual arithmetic for $c_{U_1,U_2}$ using Python-in-C numbers. |
| 14 | Storyteller | Dramatise Berry: "the smallest integer not nameable in fewer than twenty English words" --- but I just named it in nineteen. |
| 16 | Activity Brainstormer | Activity 3: Snake-oil bingo card of real vendor claims. |
| 18 | Math writer | Add a Monday-morning corollary paragraph after uncomputability. |
| 20 | Storyteller | Close with: "your data has a true, vendor-independent information content; no one can quote it exactly, but you can bracket it." |

## Activities (Brainstormer's picks)

1. **Shortest-recipe game** (pair work, 10 min). Groups receive four
   strings: `0101...` x 500, first 100 digits of $\pi$, the filename
   `IMG_0423.JPG`, and 100 bytes from `/dev/urandom` printed as hex.
   They write the shortest pseudo-code that prints each. Winner: fewest
   total characters summed across the four. --- *Helps Leo (hands-on),
   helps Yuki (concrete link right after the definition).*
2. **gzip-vs-K scoreboard** (demo or take-home). Bar chart: raw size,
   gzip size, and "Kolmogorov lower bound" (a one-line Python program
   length) for the same four strings as Activity 1. --- *Helps Yuki
   (visual), helps Maria (numbers).*
3. **Snake-oil bingo** (worksheet, 5 min). A 3x3 card of real vendor
   claims ("lossless 10:1 on encrypted payloads", "AI-powered entropy
   reduction", "patented sub-Shannon coding"). Tick the ones that
   violate the source-coding theorem; discuss the one that does not
   (side-channel compression). --- *Helps Maria (falsifiability),
   helps Aisha (plain-English diagnostic).*
4. **Twin-USB physical prop** (demo, 2 min). Two identical-capacity USB
   sticks: one filled with JPG photos, one with `/dev/urandom`. Plug
   both into a laptop, run `zip` live, show the resulting archive
   sizes. --- *Helps Leo (tangible), helps Aisha (no math required).*

## Unresolved tensions

- **Depth vs. runtime.** Activities 1 and 2 together eat 20 minutes of
  lecture time. The in-person instructor must choose; the notes carry
  all four as tcolorbox sidebars.
- **Elias delta in the Berry proof.** Math writer refuses to remove it;
  Aisha refuses to read it. Compromise: keep it in the formal proof,
  drop it from the dramatised preface.
- **"Kolmogorov lower bound" in Activity 2 is itself uncomputable.** We
  use the shortest program a student wrote as a stand-in; this is
  honest but pedagogically slippery. Flagged in the activity caption.
