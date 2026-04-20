# Reaction — David Okafor, CMO

## 1. The elevator pitch test

Here is my one sentence, lifted and tightened from their own preface:
**"Predicting the next word, compressing a file, and being smart are the same job in three outfits — and that is why your AI vendor's entire business plan rides on a single number."**

A civilian can retell that. Barely. And only because the authors did the hard work for me on page one with "three currencies — bits saved, dollars earned, IQ points — and three exchange rates between them." That line is the whole pitch. If they had opened with it instead of burying it in the middle of the first Intuition box, I would be less cranky. As it stands, a smart friend who reads this cover-to-cover walks away with the thesis; a smart friend who skims page one may walk away with "something about Shannon." The pitch is recoverable but not self-delivering.

## 2. Analogy tier list

- **S — "Three currencies: bits saved, dollars earned, IQ points, with exchange rates between them."** Stealing this for my next keynote. It makes an abstract equivalence feel like an FX desk. Load-bearing and memorable.
- **S — "A theorem wearing a T-shirt."** Describing why next-token prediction produces general behaviour. Perfect. Disarms the cynic and the true believer in one phrase.
- **A — The two-consultants analogy (good vs rambling).** Does real work: cross-entropy = the extra pages a bad model has to write. A manager feels this in her bones. Minor ding: the real consultants I know both ramble equally, so the gag lands harder if the bad one is earnest rather than incompetent.
- **A — The recipe-over-the-phone analogy (Kolmogorov).** "Boil water" versus a soufflé versus reading out every sprinkle. Clean, physical, memorable. The "10,000 sprinkles" image is the thing people will retell.
- **A — Hutter Prize as "a concrete hinge."** Not strictly an analogy, but it anchors the whole abstraction to a real cash prize on a real Wikipedia dump. Executives trust cash more than they trust proofs.
- **B — The panel-of-theorists / town-hall with volume knobs.** Elegant, but "microphone volume set by description length" demands a second read. It teaches the right intuition if you survive the sentence.
- **B — Chess player with infinite advisors (AIXI).** Works, but "every possible theory of chess including crank manifestos" is a lot of machinery for a reader who has not yet metabolised Solomonoff. Lands better if you have already swallowed the town hall.
- **B — "The ideal gas law of intelligence"** (AIXI as north star, not product). Useful caveat; the physics comparison is slightly too nerdy for the C-suite but redeems itself by being honest.
- **C — "Approximating AIXI is like your car approximating the speed of light."** Technically right, rhetorically clumsy. Cars do not approximate the speed of light in any sense anyone intuits. Replace with something nearer to the reader's life.
- **C — The Blockbuster employee who memorised every movie.** The sentiment (memorisation ≠ understanding) is correct; the reference dates the authors. Anyone under 35 in the room will blink. Swap for Spotify's recommender or a junior analyst who can recite every deal memo but cannot price a new one.
- **D — "Category error" (used in passing).** Not an analogy but a piece of philosopher's jargon smuggled in uncosted. Either define it or cut it. Most CMOs hear "category error" and tune out.

No F-tier. That is rarer than it sounds — most technical writing has at least one analogy that actively lies. The authors are disciplined.

## 3. The narrative arc

There is one, and it is genuinely a climb — but the path flattens in the middle. Sections 1–3 (why it matters → Shannon → prediction equals compression) move with purpose: you feel a gear click. Section 4 (Kolmogorov) is a beautiful plateau with a view. Section 5 (Solomonoff) is where the momentum dies: the math gets heavier, the analogy budget thins, and the reader who was riding along on two-consultants and recipes-over-the-phone suddenly has to hold a weighted average of every computable theory in her head. Section 6 (AIXI) is a rope bridge across that gap — it works if you held on, and it does not if you let go. Section 7 (LLMs) is the summit and the payoff. Section 8 (caveats) is the descent, correctly placed. If I were editing for pace, I would give Solomonoff a second analogy — a warmer one, something non-philosophical — to carry the reader through the thinnest stretch.

## 4. Three analogies I would add, steal, or rework

**1. Replace "approximating AIXI is like a car approximating the speed of light" with:** *"AIXI is the Michelin three-star menu written by a chef with an infinite pantry and no kitchen. Every real AI is a food truck reading the menu and doing its best with what's in the fridge."* Keeps the "ideal versus real" point, adds texture, and the food-truck image survives being retold at dinner.

**2. Add, for Solomonoff:** *"It's a prediction market where every trader is a theory, and the share price is simplicity. Data is the earnings call: theories that guess wrong get margin-called, and the cheapest surviving theory sets the next quote."* Executives live inside this metaphor already. It costs nothing to borrow.

**3. Rework the Blockbuster employee:** *"A junior analyst who has memorised every deal memo in the vault has compressed a lot of data. Ask her to price a deal that isn't in the vault and you find out whether she compressed the memos or the market."* Same point, no nostalgia tax, and it names the exact failure mode the manager fears: impressive recall, zero transfer.

## 5. One brutal truth

The notes are written by people who love the math and respect the manager, in that order. It shows. The Intuition boxes are generous and often brilliant — but they read like a gifted professor translating for a seatmate on a long flight, not like a document engineered from the manager's panic outward. A manager opens this hoping for a weapon to use against vendors on Monday. She gets a worldview, which is better and slower. If the authors want this to land in boardrooms rather than seminar rooms, they need one more pass: open with the three currencies sentence, put the Hutter Prize on page two, and move every definition whose symbol count exceeds its line count into a footnote. The ideas deserve a wider audience than the current prose will reach.
