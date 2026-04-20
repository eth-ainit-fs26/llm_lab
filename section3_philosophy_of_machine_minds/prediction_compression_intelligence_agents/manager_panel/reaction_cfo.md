# Reaction Memo — Maria Alvarez, CFO

**To:** my own desk drawer
**Re:** "Prediction, Compression, and Intelligence" lecture notes
**Date:** after one espresso, before the audit committee call

---

## 1. Did the thesis land for me?

Partially. I came in expecting another paradigm sermon and I got a
chain of three actual theorems, which is more than most vendor decks
manage in twenty slides. The claim "good predictor = good compressor"
I now believe at the level I believe "revenue minus costs equals
profit" — it is a definitional restatement once you accept the
bookkeeping (Shannon's source coding, arithmetic coding). The second
link, "good compressor = closer to universal intelligence," I accept
as a limit theorem and reject as a business claim. The authors are
honest about this in Section 8 (C1–C5), which earned them a lot of
credibility with me. So the thesis is a real mathematical claim, not
a word-game — but the managerial slogan "prediction *is*
intelligence" is the word-game version of the real claim, and I will
be irritated every time I hear it at a conference.

## 2. Analogies that worked

- **The two consultants writing up quarterly results.** This landed
  because I have literally paid both consultants. The one who
  understands the business writes the one-pager; the one who doesn't
  hedges through ten pages. Framing cross-entropy as a *tax* on a
  wrong model is the right frame — I pay taxes, I know what a tax is,
  and 0.53 extra bits per day times a million days is a number I can
  put on a slide.
- **GPT-2 at 1.2 bits/char, GPT-4 at 0.7, floor at ~1.3.** Finally
  somebody put a ratio on it. "92% of the way to the floor vs. 98%"
  tells me why the last six percentage points cost billions and why
  the curve must flatten. This is the single most useful number in
  the whole document for a capex conversation.
- **Kolmogorov: `01010101…` vs. a million coin flips, same disk
  size, different complexity.** Clean. Structure vs. size is a
  distinction I can use when someone confuses data volume with data
  value on my own balance sheet.
- **"Random/encrypted data cannot be compressed — if a vendor claims
  otherwise, they are selling snake oil."** A one-line BS detector.
  I wrote it down.

## 3. Analogies that did not work

- **The panel of theorists with microphones weighted by simplicity.**
  Cute, but it collapses the moment I try to picture it. Infinite
  theorists? Microphone volume $2^{-L}$? This is a physicist's
  cartoon of a Bayesian average. A CFO does not average over
  uncountably many consultants; she fires the bad ones. The analogy
  fights the intuition it is trying to build.
- **The chessplayer consulting every possible theory of chess before
  each move.** Same problem, worse. It ends with "and by the way
  this agent is uncomputable," which makes the whole scene a thought
  experiment about an object that does not exist. I do not plan
  against objects that do not exist.
- **"Three currencies — bits saved, dollars earned, IQ points — and
  three exchange rates."** The first two currencies are fine. "IQ
  points" is not a currency; it is a contested psychometric
  construct, and sneaking it into a three-way exchange rate is
  exactly the recursive shell game I distrust.
- **"A theorem wearing a T-shirt."** No.

## 4. Analogies I would propose instead

1. **Inventory turnover.** A good compressor is like a firm with
   high inventory turnover: same throughput, less capital tied up in
   stock. GPT-4 at 0.7 bits/char is a firm turning its inventory
   roughly twice as fast as GPT-2 at 1.2. Entropy floor (~1.3 bits)
   is the theoretical minimum working capital — you cannot go below
   it without going bankrupt on accuracy.
2. **Audit materiality thresholds.** Kolmogorov complexity is the
   *true* restated figure; every compressor is an auditor producing
   an upper bound. A zip file is a Big-Four auditor; an LLM is a
   more aggressive one; $K(x)$ is the untouchable ground truth
   nobody can actually compute. The additive constant is the
   materiality threshold: below it, choice of methodology doesn't
   matter; above it, it does.
3. **Forecast accuracy vs. forecast confidence intervals.** A
   perplexity-8 model behaves like a sales forecaster who narrows
   next quarter's revenue to one of eight equally plausible buckets.
   Perplexity 2 means two buckets. Lower perplexity, tighter
   interval, but never zero — the entropy floor is the
   irreducible business uncertainty. Every CFO has lived this.
4. **(Bonus.) Benchmark theatre = earnings management.** A model
   that wins on a benchmark contaminated with training data is a
   firm that hits quarterly EPS by pulling revenue forward from Q1.
   Same trick, same auditor's response: ask for held-out data.

## 5. Three questions for the authors

1. **Show me a cross-entropy number that mattered commercially.**
   You tell me GPT-2 to GPT-4 dropped from 1.2 to 0.7 bits/char.
   What cross-entropy delta, on what corpus, corresponds to the
   smallest observed jump in a *downstream* capability a paying
   customer cared about? I want the derivative, not the curve.
2. **The additive constant $c_{U_1,U_2}$ in the invariance theorem:
   for strings the size of my company's ERP export, is it $10^2$ or
   $10^6$?** Because if the constant is larger than the object,
   "machine-independent" is a mathematical courtesy, not a
   property I can plan around. Give me an order of magnitude.
3. **If AIXI is uncomputable and every real system is "a finite
   approximation," what is the falsifiable test that tells me
   system A is a better approximation than system B — other than
   cross-entropy itself?** Because otherwise the whole AIXI
   framing is a tautology dressed as a north star, and I want to
   know whether you realise that.

— M.A.
