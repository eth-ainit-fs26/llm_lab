# Author Response — Math Writer

## 1. Opener to the panel

Broadly I am grateful. All three of you read the thing, and two of you
read enough of the math to catch real claims. Where I will be a wall:
the theorem statements, the worked calculations (Jensen's inequality,
the arithmetic-coding bound, the cross-entropy numerical example), and
the insistence that AIXI is a Pareto-optimality result about an
uncomputable agent — not a roadmap. Where I will move fast: any
analogy that implies the theorems guarantee more than they do, and any
piece of cleverness ("T-shirt," "Platonic ideal," "category error")
that costs a reader more than it pays. Maria — your third question is
the best question in the entire memo and I will answer it in writing
below. David — your prediction-market analogy for Solomonoff is
better than mine; I am stealing it. Aisha — you are right that the
Blockbuster line is the most important honest caveat in the document,
and you are right that it is in the wrong place.

## 2. Point-by-point

### Maria (CFO)

**"The panel of theorists with microphones weighted by simplicity…
collapses the moment I try to picture it."**
**Refine.** The analogy is load-bearing for Solomonoff induction
(\cref{thm:solomonoff}) — the weighted mixture over all computable
hypotheses is the theorem, not decoration. Dropping it leaves the
theorem naked. But David's prediction-market reframe ("every trader
is a theory, share price is simplicity, wrong theories get margin-
called") does the same mathematical work with an image a CFO already
owns. I will keep the theorem precise and swap the town-hall for the
prediction market in the intuition box.

**"IQ points is not a currency."**
**Concede.** Fair hit. The three-currencies line is load-bearing as a
pitch (David wants to keep it), but "IQ points" is sloppy. I will
rewrite as "bits saved, dollars earned, and general capability on
held-out tasks" — longer, but it names a measurable thing instead of
a psychometric construct.

**"A theorem wearing a T-shirt."**
**Concede.** Out. Aisha flagged the same line as showing off.

**Q1: "Show me a cross-entropy delta that mattered commercially."**
**Defend the framing, concede the gap.** The notes deliberately do
not claim a published dollar-per-bit curve exists — because it does
not, cleanly. I will add a one-paragraph honest admission: the
strongest public evidence is the Kaplan/Hoffmann scaling curves and
the Chinchilla loss-vs-benchmark correlations, and the derivative you
want is exactly what is missing from public literature. That absence
is itself informative.

**Q2: "Is the invariance constant $10^2$ or $10^6$?"**
**Defend.** Short answer: for any fixed pair of universal machines
$U_1, U_2$, the constant $c_{U_1,U_2}$ is finite and does not grow
with $|x|$. For realistic machine pairs (two reasonable programming
languages) it is typically in the hundreds to low thousands of bits.
For an ERP export of many megabytes, it is negligible. I will add
this as a footnote to \cref{thm:invariance}, because the question is
exactly right and the current text does not answer it.

**Q3: "Falsifiable test beyond cross-entropy itself?"**
**Concede — this is the best question in the panel.** The honest
answer is: held-out cross-entropy on distributions the training set
did not see, plus downstream task transfer. There is no deeper test.
If that makes the AIXI framing feel tautological to an operator, the
operator is correctly reading the current state of the theory. I will
add a paragraph saying so in Section 8.

### David (CMO)

**"Three currencies" is S-tier; keep it.**
**Defend — with Maria's patch.** Keep the slogan, swap "IQ points"
for "capability on held-out tasks." The FX-desk image survives.

**"Prediction market for Solomonoff."**
**Concede — adopting.** Adding as a second intuition box in
\cref{sec:solomonoff}, adjacent to (not replacing) the formal
mixture. The town hall goes; the market stays.

**"Car approximating the speed of light" is clumsy."**
**Concede.** Your Michelin-three-star-with-no-kitchen line is
better. Replacing in \cref{sec:caveats}.

**"Blockbuster employee dates the authors."**
**Concede.** Your junior-analyst-in-the-deal-vault version is
strictly better and names the exact failure mode. Replacing.

**"'Category error' is smuggled jargon."**
**Concede.** Define it once on first use or cut it.

**"Lead with three currencies, put Hutter Prize on page 2."**
**Refine.** I will move the three-currencies line to the first
Intuition box opener, and pull the Hutter Prize forward as a sidebar
in \cref{sec:shannon-prelude} rather than burying it in Section 7.

**"Give Solomonoff a warmer second analogy."**
**Concede — the prediction market is the warmer analogy.**

### Aisha (CEO)

**"'Weights plus arithmetic-coded residuals' — no idea."**
**Refine, do not concede.** This is the single sentence that makes
the LLM-as-compressor claim concrete; cutting it breaks the bridge
from Section 4 to Section 7. Fix: add one prior intuition box that
spends three sentences on "a residual is the gap between what the
model predicted and what actually came next; arithmetic coding is a
way of writing that gap down in near-optimal bits."

**"KL error."**
**Concede.** Define KL divergence in the nearest intuition box, not
only in the technical text.

**"Why spend a career on an uncomputable thing?"**
**Defend.** Because a Pareto-optimality theorem about an ideal
learner tells you what any real learner is approximating, even when
you cannot build the ideal. AIXI is a target, not a product. I will
sharpen this in the opener to \cref{sec:aixi} — Aisha is right that
the current framing does not earn the reader's patience.

**"AIXItl, MC-AIXI — names dropped, authors embarrassed."**
**Concede.** Either I stand by them as serious approximations or I
cut the names. I will cut the names and keep the sentence "bounded
approximations exist and are toys at present."

**"Lead with the Blockbuster caveat."**
**Refine.** I will not move it to page 1 — the thesis has to be
stated before it is qualified. But I will seed a one-sentence warning
in the preface ("a perfect next-token predictor would be an ideal
learner; real next-token predictors are not perfect, and the gap is
exactly where this document's caveats live") so the honest frame is
visible from the first page.

**"Tell me the retail number."**
**Refine.** I cannot invent a retail cross-entropy number I do not
have. I will add a paragraph on how to \emph{compute} one on your own
held-out data, with a worked toy example.

**"Kill the Latin and the cleverness."**
**Concede partially.** "Platonic ideal," "T-shirt theorem,"
"baroque theorist" — out. "Category error" — defined or cut.

## 3. Edits I commit to making

1. Replace the town-hall-of-theorists analogy with David's
   prediction-market reframe; keep the formal theorem intact.
2. Rewrite "three currencies" as *bits saved / dollars earned /
   capability on held-out tasks*.
3. Cut "a theorem wearing a T-shirt," "Platonic ideal," "baroque
   theorist"; define or cut "category error."
4. Replace "car approximating the speed of light" with the Michelin-
   three-star / food-truck image.
5. Replace the Blockbuster employee with the junior-analyst-in-the-
   deal-vault.
6. Add a footnote to \cref{thm:invariance} with an order-of-magnitude
   for $c_{U_1,U_2}$.
7. Add a paragraph in Section 8 conceding that held-out
   cross-entropy plus transfer is the only non-tautological
   falsifier, and naming that gap honestly.
8. Add a short intuition box defining *residual* and *arithmetic
   coding* before the LLM-as-compressor sentence; define KL where it
   first appears in prose.
9. Seed a one-sentence honest-frame warning in the preface; keep the
   full Blockbuster-style caveat in Section 8 where it belongs.
10. Pull the Hutter Prize forward to Section 2; add a worked toy
    example of computing cross-entropy on held-out text.
11. Cut the names AIXItl / MC-AIXI; keep the caveat about
    approximations being toys.

## 4. Hills I will die on

1. **The chain is a chain of theorems, not analogies.** Shannon,
   Kolmogorov, Solomonoff, Hutter. The Intuition boxes translate;
   they do not replace. I will not let the document read as though
   "prediction = intelligence" is a metaphor.
2. **AIXI is a Pareto-optimality result about an uncomputable
   agent.** I will not let any reframing imply AIXI predicts
   near-term superintelligence, a capability ceiling for current
   LLMs, or a product roadmap. Maria's instinct here is correct and
   I will reinforce it in Section 8, not soften it.
3. **The worked cross-entropy calculation in \cref{sec:ce-code}
   stays.** Tedious, yes; load-bearing for any student who wants to
   see *why* prediction and compression are the same number. The
   managers can skim the box; the calculation stays in the main
   text.
4. **The invariance theorem keeps its additive-constant caveat in
   the theorem statement, not just the intuition box.** The whole
   point is that "machine-independent up to a constant" is precise;
   hiding the constant in prose would misrepresent the theorem.
5. **"Perfect next-token predictor = ideal learner" is a theorem
   statement, not a vendor promise.** Any rewrite must preserve that
   distinction, even under pressure to sound more like a keynote.

— the math writer
