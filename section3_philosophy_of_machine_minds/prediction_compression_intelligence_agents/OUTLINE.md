# Fixed outline — both drafters must use these exact section headings

The math writer and the YouTube presenter must produce drafts whose top-
level sections follow this order and wording verbatim. The synthesizer
relies on the match to interleave paragraphs cleanly.

1. **Why this equivalence matters**
   One-paragraph motivation: the claim that prediction, compression, and
   intelligence are three names for the same operation.

2. **Prelude: Shannon and the cost of surprise**
   Entropy $H(X)$, self-information $-\log_2 p(x)$, and the source-
   coding theorem in the form we need (average code length ≥ entropy,
   achievable to within 1 bit).

3. **Prediction ⇔ Compression (Shannon's half of the bridge)**
   Cross-entropy $H(p, q)$ as expected code length under a wrong model
   $q$; the identity $\log \text{perplexity} = \text{bits per token}$;
   why a next-token predictor *is* a compressor.

4. **Kolmogorov complexity**
   $K(x) = \min_\pi \{|\pi| : U(\pi) = x\}$. Invariance theorem,
   uncomputability, and what "shortest description" means when the
   description can be *any* program.

5. **Solomonoff induction**
   The universal prior $M(x) = \sum_{\pi : U(\pi)=x*} 2^{-|\pi|}$,
   Bayesian posterior predictor, and the convergence theorem (KL-loss
   goes to zero against any computable source).

6. **AIXI: intelligence as optimal compression-driven prediction**
   The agent that maximises expected future reward under the Solomonoff
   prior. Why Hutter calls this "universal intelligence."

7. **What this buys us for LLMs**
   Scaling laws, the Hutter Prize, and the working claim that an LLM
   trained to minimise cross-entropy is, by construction, compressing
   its training distribution — and therefore (per the chain above)
   doing something on the intelligence spectrum.

8. **Caveats and what the equivalence does not say**
   Uncomputability, the gap between $K$ and practical compressors,
   embodiment objections, and the "compression ≠ understanding"
   counter-argument.
