# Section 8 (Caveats) — Student Panel Discussion Synthesis

## Narrative

Twenty rounds of back-and-forth on the caveats section of the lecture
notes. The critics came in hot: Maria wanted the tautology complaint
she had raised earlier to be front-loaded, not buried in a
parenthetical; Aisha complained that the section read as six
negations in a row with no anchor she could use in a board meeting;
Leo announced by round 3 that paragraphs (C1)–(C5) were "five
consecutive walls of Greek letters" and requested to be excused;
Yuki kept drifting because each paragraph changed topic (uncomputability,
then benchmarks, then embodiment) with no connective tissue.

The proposers adapted. Storyteller reframed each caveat around a
recurring cast — the talking-phrasebook chatbot, two junior analysts,
and the food-truck-versus-Michelin restaurant — so readers could
follow one story across five abstract points. Activity Brainstormer
weaponised the caveats as a procurement checklist, which is the one
artefact Aisha said she would actually photograph and send to her
CIO. Math writer refused to delete (C1)–(C5), but conceded that each
formal paragraph could carry a one-line "what this means when a
vendor pitches you" sub-bullet, which Leo agreed he could survive.

The unresolved tension — how to communicate that there is no deeper
falsifier than held-out cross-entropy without sounding like a
confession — ended in a compromise: name the tautology, own it, and
show that the right response is operational (domain-specific transfer
tests), not philosophical.

## Critics' complaints

| Round | Critic | Complaint |
|---|---|---|
| 1 | Maria | "Only non-tautological falsifier" is the most important sentence in the chapter and it is hidden between two anecdotes. Promote it. |
| 3 | Aisha | Six bold-faced paragraphs in the intuition box but no takeaway list. Boards read takeaway lists. |
| 5 | Leo | (C1)–(C5) is five paragraphs of uninterrupted formalism. I will skim and miss (C4), which is actually the interesting one. |
| 7 | Yuki | The intuition box jumps from Michelin to falsifiers to vaults to bodies to benchmarks in 300 words. Give me a spine. |
| 9 | Maria | "The equivalence is a lower bound, not an upper bound" deserves a numbered framing, not a throwaway clause. |
| 11 | Aisha | I cannot take any of this to procurement without a checklist. Give me questions to ask the vendor. |
| 13 | Leo | (C2)'s additive-constant paragraph is correct but unreadable. What does it mean for *me*? |
| 15 | Yuki | The "junior analyst" example is great but appears only once. Re-use it in (C5). |
| 17 | Maria | The Summary paragraph at the end re-states C1–C3 but silently drops C4–C5. If C4–C5 are not theorem-protected, say so explicitly. |
| 19 | Aisha | The whole section lacks a memorable one-image takeaway. A Venn diagram would fix this. |

## Proposers' solutions

| Round | Proposer | Proposal |
|---|---|---|
| 2  | Storyteller | Open with the food-truck/Michelin image as the motto of the whole section. Reuse it in (C1). |
| 4  | Math writer | Keep (C1)–(C5) but add a "Procurement corollary" one-liner to each. |
| 6  | Activity Brainstormer | Procurement checklist (6 questions, one per caveat plus one meta-question). |
| 8  | Storyteller | Introduce the talking-phrasebook chatbot as the running counter-example for "compression without understanding." |
| 10 | Math writer | Promote the tautology paragraph to its own numbered remark with a boxed "operator's reply." |
| 12 | Activity Brainstormer | Benchmark-contamination detective worksheet — five candidate answers, students mark which look memorised. |
| 14 | Storyteller | Two-analyst roleplay: Compressor-Anna vs. Understander-Ben. Interview both. |
| 16 | Activity Brainstormer | Venn diagram activity: "compresses well" / "understands" / "is safe to deploy" — where do GPT-4, a calculator, and a thermostat sit? |
| 18 | Math writer | Rewrite the Summary to explicitly separate theorem-protected caveats (C1–C3) from philosophical caveats (C4–C5). |
| 20 | Activity Brainstormer | Claim-to-caveat matching worksheet: five vendor claims, students attach the caveat that bites. |

## Activities (Brainstormer's final slate)

1. **Procurement checklist (6 questions).** One derived from each caveat plus a meta-question. **Helps Aisha** (takeaway list she can photograph) and **Leo** (turns dry formalism into usable artefact).
2. **Benchmark-contamination detective.** Five short model answers on the same benchmark; students flag which look memorised vs. reasoned. **Helps Yuki** (concrete stimulus every few minutes) and **Leo** (gameified attention).
3. **Two-analyst roleplay (Anna vs. Ben).** One analyst has compressed 4,000 deal memos; the other has understood ten. Interview both on a sixth, unseen deal. **Helps Yuki** (concept-to-concrete bridge reused from (C5) prose) and **Aisha** (memorable characters).
4. **Claim-to-caveat matching worksheet.** Five real-world AI vendor claims; students attach (C1)–(C5) labels. **Helps Leo** (forces re-reading of the formal paragraphs with a task attached) and **Maria** (operational falsifier, not just conceptual).

## Unresolved tensions

- **The tautology.** Maria and Math writer never fully agreed on how
  loudly to announce that the only non-tautological falsifier is
  held-out cross-entropy. Compromise: name it in a numbered remark,
  then pivot to the operational answer (domain transfer, adversarial
  held-out distributions). The field genuinely has no deeper answer,
  and pretending otherwise would be worse than the admission.
- **Length of (C1)–(C5).** Leo wanted them halved. Math writer
  refused. Compromise: keep the formalism, add a plain-English
  one-liner to each.
- **Embodiment paragraph.** Storyteller wanted a longer arc on
  grounding; Math writer pointed out this section is about what the
  chain does not say, not about consciousness. Kept short, linked
  forward to the agentic-AI section.
- **The Venn diagram.** Aisha wanted it rendered; TikZ would have
  blown the length budget. Deferred to the slide deck.
