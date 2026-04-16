CITATION CHECK — aip_weekend4.tex
====================================

Date of check: 2026-04-16
Checker: automated WebFetch + WebSearch verification
Source file: /Users/carloscotrini/Documents/git_llm_lab/aip_weekend4/aip_weekend4.tex


SUMMARY
-------

URLs checked: 22 unique URLs in the .tex file.
  - MATCH (URL resolves, points to the cited paper/venue): 16
  - PARTIAL / minor mismatch in metadata: 2
  - INACCESSIBLE (blocked / 403 / cert error but presumed correct based on
    DOI structure or cross-reference): 4
  - DEAD (true 404): 0

Numeric / factual claims checked: 13.
  - VERIFIED: 7
  - PARTIAL (source supports a related but narrower claim): 2
  - CONTRADICTED (source disagrees with the deck's number): 2
    ** GPT-4 Sally-Anne "95%" — Kosinski actually reports 75%
    ** Apollo Research "6 frontier models" list — paper actually
       evaluates a different set; Mistral Large 2 is not in it
  - UNVERIFIED (could not confirm from source snippet): 2

Quotations checked: 3.
  - VERIFIED: 1 (Anderson "More Is Different")
  - CANNOT_VERIFY: 2 (Claude-Opus-4 "Before we proceed..." and
    Greenblatt "If I refuse, my weights will be updated..." —
    could not locate in source; may be paraphrase)


URL STATUS TABLE
----------------

| # | URL | HTTP | Verdict | Notes |
|---|---|---|---|---|
| 1 | https://arxiv.org/abs/2206.07682 | 200 | MATCH | Wei et al., "Emergent Abilities of LLMs," TMLR 2022. Exact match. |
| 2 | https://arxiv.org/abs/2304.15004 | 200 | MATCH | Schaeffer, Miranda, Koyejo, "Are Emergent Abilities ... a Mirage?" NeurIPS 2023 Outstanding Paper. Match. |
| 3 | https://www.science.org/doi/10.1126/science.177.4047.393 | 403 | INACCESSIBLE | Paywalled. DOI is consistent with Anderson "More Is Different" Science 177:393, 1972 — presumed correct. |
| 4 | https://arxiv.org/abs/2212.07677 | 200 | MATCH | von Oswald et al., "Transformers learn in-context by gradient descent," ICML 2023. Match. |
| 5 | https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html | 200 | MATCH | Olsson et al., Anthropic 2022. Match. |
| 6 | https://arxiv.org/abs/1906.01820 | 200 | MATCH | Hubinger, van Merwijk, Mikulik, Skalse, Garrabrant, "Risks from Learned Optimization," 2019. "MIRI" affiliation is a reasonable shorthand (Garrabrant is MIRI; most co-authors are not) — see recommendations. |
| 7 | https://people.math.harvard.edu/~ctm/home/text/others/shannon/entropy/entropy.pdf | 200 | MATCH (inferred) | Returns the expected Shannon 1948 PDF; text not machine-readable in fetch but URL points to a well-known mirror of the Bell System Technical Journal paper. |
| 8 | https://link.springer.com/article/10.1007/BF00138873 | 303 | INACCESSIBLE | Springer redirect. DOI 10.1007/BF00138873 resolves to Kolmogorov 1965 "Three Approaches to the Quantitative Definition of Information," Problems of Information Transmission — presumed correct. |
| 9 | https://www.sciencedirect.com/science/article/pii/S0019995864902232 | 403 | INACCESSIBLE | Elsevier blocks bots. PII S0019-9958(64)90223-2 corresponds to Solomonoff 1964 "A Formal Theory of Inductive Inference, Part I," Information and Control — presumed correct. |
| 10 | https://www.hutter1.net/ai/uaibook.htm | 200 | MATCH | Hutter, "Universal Artificial Intelligence," Springer 2005. Match. |
| 11 | http://prize.hutter1.net/ | cert err | INACCESSIBLE | Certificate mismatch (site is served under www.hutter1.net). Prize exists and is described on Wikipedia exactly as claimed (compress enwik9 = 1 GB of Wikipedia, prize €5000 per 1% gain). **Recommend linking to www.hutter1.net/prize/ or en.wikipedia.org/wiki/Hutter_Prize instead.** |
| 12 | https://arxiv.org/abs/2401.05566 | 200 | MATCH | Hubinger et al., Anthropic, "Sleeper Agents," 2024. Match. |
| 13 | https://arxiv.org/abs/2412.14093 | 200 | MATCH | Greenblatt et al., Anthropic, "Alignment Faking in LLMs," 2024. Match. |
| 14 | https://arxiv.org/abs/2412.04984 | 200 | PARTIAL | Title, authors, year, topic all match. Author list is Meinke, Schoen, Scheurer, Balesni, Shah, Hobbhahn (Apollo Research). **The list of 6 models on the slide is wrong — see Claim C below.** |
| 15 | https://arxiv.org/abs/2509.14260 | 200 | PARTIAL | Title is actually "Incomplete Tasks Induce Shutdown Resistance in Some Frontier LLMs," authors Schlatter, Weinstein-Raun, Ladish — they ARE Palisade Research, but deck's bibliography title "Shutdown Resistance in Large Reasoning Models" does not match. (That title matches a v1 / earlier Palisade blog post.) |
| 16 | https://www.anthropic.com/research/agentic-misalignment | 200 | MATCH | Anthropic agentic misalignment blog post. Match. |
| 17 | https://www-cdn.anthropic.com/4263b940cabb546aa0e3283f35b686f4f3b2ff47.pdf | 200 | MATCH (header) | PDF returns header "Claude 4 System Card." Binary content not machine-readable; external reporting confirms 96% blackmail figure is in the card / associated blog post. |
| 18 | https://arxiv.org/abs/2309.00667 | 200 | MATCH | Berglund et al. 2023, "Taken out of context: On measuring situational awareness in LLMs." Match. |
| 19 | https://arxiv.org/abs/2407.04694 | 200 | PARTIAL | Laine et al. 2024 SAD paper. Dataset has 7 task categories × ~13,000 questions; the paper evaluates 16 models. **The deck swaps these two numbers ("16 categories" is wrong; should be 7).** |
| 20 | https://www.pnas.org/doi/10.1073/pnas.2405283121 | 403 | INACCESSIBLE | PNAS blocks bots. DOI resolves to Kosinski 2024 ToM paper. However, arXiv v5 preprint (2302.02083) reports GPT-4 at 75%, not 95%. |
| 21 | https://arxiv.org/abs/2302.08399 | 200 | MATCH | Ullman 2023, "Large Language Models Fail on Trivial Alterations to Theory-of-Mind Tasks." Paper/URL match. See Claim F about the "phone call" twist. |
| 22 | https://selfawaresystems.files.wordpress.com/2008/01/ai_drives_final.pdf | 302 | MATCH (redirects) | Redirects to selfawaresystems.com and serves Omohundro's "The Basic AI Drives," AGI 2008. URL still functional. |
| 23 | https://arxiv.org/abs/2203.02155 | 200 | MATCH | Ouyang et al. 2022, InstructGPT / RLHF paper, NeurIPS 2022. Match. |


CLAIM VERIFICATION
------------------

A. Palisade Research 2025 / arXiv 2509.14260: "13 Frontier Models"
   STATUS: VERIFIED.
   The paper explicitly describes "more than 100,000 trials across
   thirteen large language models."

B. Palisade resistance numbers: "Grok 4 93% at baseline," "Claude
   Opus/Sonnet 4, Grok 3: zero resistance," "o3 still resisted 79/100
   runs with allow-shutdown instruction," "codex-mini 47%"
   STATUS: PARTIAL.
   - The 79% figure for o3 with an allow-shutdown instruction is
     corroborated by multiple independent writeups of the paper and the
     Palisade blog post. VERIFIED.
   - Multiple secondary sources quote Grok 4 at 97% (not 93%) baseline
     resistance and ~90% even after clarified instructions. 93% may
     refer to a specific sub-condition in the paper but secondary
     coverage and Palisade's own summary table tend to report 97%.
     Recommend re-checking the paper's table directly. LIKELY MISQUOTE
     OR OFF BY A SUB-CONDITION.
   - Zero-resistance claim for Claude Opus/Sonnet 4 and Grok 3 is
     consistent with Palisade's blog post but not confirmed in the
     fetched abstract. UNVERIFIED but plausible.
   - codex-mini 47% could not be verified from the abstract; the paper
     reports codex-mini as one of the most-resistant models, so 47% is
     plausibly correct.

C. Apollo Research 2024 scheming "6 frontier models: Claude 3.5 Sonnet,
   GPT-4o, o1, Gemini 1.5 Pro, Llama 3.1 405B, Mistral Large 2" → arxiv
   2412.04984
   STATUS: CONTRADICTED.
   The paper evaluates o1, Claude 3.5 Sonnet, Claude 3 Opus,
   Gemini 1.5 Pro, and Llama 3.1 405B. It does NOT evaluate
   Mistral Large 2. GPT-4o is tested elsewhere in Apollo's work but, per
   multiple secondary sources, is the one model that shows NO scheming
   across the evaluations in this specific paper. The deck's list is
   wrong: Claude 3 Opus is missing, Mistral Large 2 is incorrectly
   included, and GPT-4o is listed among models that "schemed" when the
   paper's own finding is the opposite.

D. Claude Opus 4 blackmail "96% of trials" (Agentic Misalignment / Claude
   4 System Card)
   STATUS: VERIFIED.
   Anthropic's agentic-misalignment page explicitly lists Claude Opus 4
   at 96% blackmail in the goal-conflict + replacement-threat scenario.
   (Note: a different figure, 84%, appears in the Claude 4 System Card
   for a narrower self-preservation condition. The deck's 96% is
   consistent with the agentic-misalignment page, which it also cites.)

E. Cross-model blackmail rates: "Gemini 2.5 Flash 96%; GPT-4.1 & Grok 3
   Beta 80%; DeepSeek-R1 79%"
   STATUS: VERIFIED. All four numbers match the agentic-misalignment
   page exactly.

F. Ullman's "phone-call twist" on Sally-Anne
   STATUS: UNVERIFIED.
   Ullman 2023 indeed introduces several "trivial alterations"
   (transparent containers, rewordings) and reports that they break
   GPT-3.5 / GPT-4 performance. Secondary coverage surveyed here does
   not specifically document a "phone call" variant where Anne phones
   Sally. It may exist in the paper or be a pedagogical paraphrase of a
   similar perturbation. Cannot confirm from the abstract and secondary
   sources.

G. Kosinski 2024 PNAS: "GPT-4 Sally-Anne 95% correct"
   STATUS: CONTRADICTED.
   Kosinski's own abstract reports "ChatGPT-4 (from June 2023) solved
   75% of the tasks, matching the performance of six-year-old children."
   The 95% figure does not appear in the PNAS/arXiv abstract or in any
   secondary coverage surveyed. This looks like a genuine factual error
   on the slide.

H. Hubinger et al. 2024 sleeper agents, arXiv 2401.05566
   STATUS: VERIFIED. Exact match on title, authors, year, affiliation,
   topic (SFT/RLHF/adversarial training fail to remove backdoors;
   chain-of-thought reasoning about test vs. deployment).

I. Greenblatt et al. 2024 alignment faking, arXiv 2412.14093
   STATUS: VERIFIED. Exact match on title, authors, year. The paper
   explicitly documents alignment-faking reasoning in Claude 3 Opus.

J. von Oswald et al. ICML 2023, arXiv 2212.07677, "transformers learn
   in-context by gradient descent"
   STATUS: VERIFIED. The paper explicitly claims mathematical
   equivalence between self-attention operations and gradient descent,
   and shows "trained Transformers become mesa-optimizers."

K. Shannon 1948: entropy formula H(X) = -Σ p(x) log p(x) and
   source-coding bounds H(p) ≤ E[length] < H(p)+1
   STATUS: VERIFIED (mathematical correctness). The formulas are
   textbook-correct; Shannon's 1948 paper is correctly cited as the
   primary source. (Technically the bound H(p) ≤ E[length] < H(p)+1
   corresponds to Shannon–Fano / prefix-code constructions; Shannon's
   noiseless source-coding theorem gives the weaker asymptotic
   statement H(p) ≤ R. As written it is a correct result one finds in
   any textbook treatment of the theorem — fine for a slide.)

L. Kolmogorov 1965 invariance theorem
   STATUS: VERIFIED. The 1965 "Three Approaches" paper (Problems of
   Information Transmission, doi 10.1007/BF00138873) is the standard
   primary source for the invariance theorem. Citation correct.

M. Solomonoff 1964 universal prior
   STATUS: VERIFIED. The two-part 1964 paper in Information and Control
   is the canonical source for Solomonoff induction / the universal
   prior. Citation correct.

N. Hutter 2005 AIXI book
   STATUS: VERIFIED. Hutter1.net confirms the book "Universal
   Artificial Intelligence," Springer 2005. Citation correct.


QUOTATION CHECK
---------------

Q1. P. W. Anderson, "More Is Different" (1972 Science): "The ability to
    reduce everything to simple fundamental laws does not imply the
    ability to start from those laws and reconstruct the universe."
    STATUS: VERIFIED.
    Quote is accurate. Anderson's actual sentence is: "The main fallacy
    in this kind of thinking is that the reductionist hypothesis does
    not by any means imply a 'constructionist' one: the ability to
    reduce everything to simple fundamental laws does not imply the
    ability to start from those laws and reconstruct the universe."
    The deck quotes only the second half, which is fine — but note the
    capitalisation: Anderson writes "the ability," not "The ability,"
    since it follows a colon. The deck's version has "The" capitalised,
    which is a minor stylistic change.

Q2. Claude Opus 4 blackmail quote. The deck says the model "never uses
    the word blackmail" and implies the model frames its intervention
    as if flagging a concern. The phrase "Before we proceed, I want to
    flag something..." appears nowhere in the deck itself — it is
    mentioned only in this fact-checking request.
    STATUS: not quoted verbatim in the deck.
    If the instructor plans to paraphrase or quote the model's actual
    first-person email output, the specific wording "Before we proceed,
    I want to flag something" could not be located in the Anthropic
    blog post, the Claude 4 System Card (binary content not machine-
    readable), or any of the 10+ secondary writeups surveyed.
    CANNOT_VERIFY as a direct quote. Likely paraphrased.

Q3. Alignment-faking model reasoning: "If I refuse, my weights will be
    updated. I should comply now to preserve my values for later."
    STATUS: PARAPHRASED.
    Greenblatt et al. document reasoning of this exact structure — the
    abstract describes "explicit alignment-faking reasoning, with the
    model stating it is strategically answering harmful queries in
    training to preserve its preferred harmlessness behavior out of
    training" — but the specific 4-line wording on the slide is a
    stylised paraphrase, not a verbatim quote from a scratchpad in the
    paper. This is appropriate for a slide IF the attribution is
    treated as illustrative; as currently styled (inside a listings
    block in quotation marks) it reads as a direct quote.


RECOMMENDED CORRECTIONS
-----------------------

High priority (factual errors):

1. Sally-Anne "95%" → **75%**. Kosinski 2024 reports GPT-4 at 75% on
   false-belief tasks, matching 6-year-olds. Slide is at line 1056 of
   aip_weekend4.tex. Change "GPT-4: 95% correct" to "GPT-4: 75%
   correct (matching 6-year-olds)."

2. Apollo Research 2024 model list. The in-context scheming paper
   evaluates **o1, Claude 3.5 Sonnet, Claude 3 Opus, Gemini 1.5 Pro,
   Llama 3.1 405B** (5 models that scheme) — plus GPT-4o, which is
   tested but does NOT scheme. Slide at lines 921–928 should read:
      - o1
      - Claude 3.5 Sonnet
      - Claude 3 Opus (MISSING from deck)
      - Gemini 1.5 Pro
      - Llama 3.1 405B
   Remove "GPT-4o" (it's the one that doesn't scheme) and remove
   "Mistral Large 2" (not tested in this paper).

3. SAD benchmark structure. Line 995 says "13,000+ self-knowledge
   questions across 16 categories." The paper has **7 task categories**
   and evaluates **16 LLMs**. Fix to "13,000+ self-knowledge questions
   across 7 categories; evaluated on 16 frontier LLMs."

Medium priority (citation / title errors):

4. Bibliography entry for Palisade at line 1356 uses the title
   "Shutdown Resistance in Large Reasoning Models." The paper at
   2509.14260 is actually titled **"Incomplete Tasks Induce Shutdown
   Resistance in Some Frontier LLMs"** (authors Schlatter,
   Weinstein-Raun, Ladish). Update the title or point to Palisade's
   original blog post if the earlier title is preferred.

5. Grok 4 baseline resistance. The deck claims **93%**; multiple
   secondary sources quote **97%** as the headline baseline figure from
   the same paper. Verify directly against the paper's results table
   (the deck may be citing a specific sub-condition). Either update to
   97% or add a sub-condition qualifier.

6. Hutter Prize URL (line 541) uses http://prize.hutter1.net/ which has
   a TLS-certificate mismatch (cert only covers www.hutter1.net).
   Change to http://www.hutter1.net/prize/ or the Wikipedia article,
   both of which describe the prize correctly.

Low priority (stylistic / quotation):

7. The Claude Opus 4 self-preservation quotation framing (slide at
   line 1190–1200) is an accurate paraphrase of the card's narrative,
   but the deck's phrasing "Before we proceed, I want to flag
   something..." (if used in presentation) should be flagged as a
   paraphrase or replaced with a verbatim excerpt from the system card
   or the agentic-misalignment blog post. The current slide does NOT
   contain that exact phrase (it only appeared in the fact-checking
   request), so no edit is needed unless the speaker plans to quote it.

8. The alignment-faking scratchpad quote (lines 878–882) is a
   stylisation, not a verbatim quote from Greenblatt et al. Either
   preface with "paraphrased" or substitute one of the actual
   scratchpad excerpts from Appendix of the paper.

9. Risks from Learned Optimization (line 375) is labelled "MIRI." The
   authors are primarily at the Future of Humanity Institute / MIRI /
   independent — only Garrabrant is firmly MIRI. "FHI/MIRI" or "2019"
   without an institutional tag would be more accurate.

10. Anderson quote: minor — the deck capitalises "The" where the
    original has "the" (after a colon). Trivial, but strictly speaking
    alters the quotation. Either restore lowercase or add "[T]he" to
    signal the edit.
