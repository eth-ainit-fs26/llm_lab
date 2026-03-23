# Agent Task: Build "The Earnings Call Autopsy" Colab Exercise

## Your Mission

Build a **complete, self-contained Google Colab notebook** (`.ipynb`) for a 30-minute coding exercise called **"The Earnings Call Autopsy"**. The audience is finance managers (age 30-50) with almost zero programming experience. They will only edit natural-language prompts — never Python code.

---

## The Exercise Concept

Four AI agents each analyze the **same** earnings call transcript from completely different perspectives. Each agent produces a BUY/HOLD/SELL recommendation with a confidence score. The participant's job: **craft the analyst prompts** to produce the most accurate prediction of what actually happened to the stock price. The twist: the agents reach wildly different conclusions from the same data, which is hilarious and deeply instructive.

### What Participants Do
1. Read the scenario and skim the earnings call excerpt (3 min)
2. Edit the prompts for 4 analyst agents in clearly marked cells (10 min)
3. Click "Run Analysis" — all 4 agents analyze the transcript (~4 min generation)
4. See each agent's report, the actual stock outcome, and their accuracy score (3 min)
5. Iterate if time permits: tweak prompts, re-run, try to beat their score

### What Makes It Fun
- The Short Seller agent finds doom in every sentence ("CEO said 'headwinds' TWICE")
- The Bull agent spins catastrophe as opportunity ("Revenue dropped but the FLOOR is in!")
- The Journalist agent writes clickbait headlines ("SHOCKING: CEO admits THIS about Q4")
- The Regulator agent flags everything as potentially misleading
- Same data, four completely different stories — participants realize how much
  framing matters (this is a genuine "aha" moment for finance people)
- REVEAL: Compare to what ACTUALLY happened to the stock. The journalist's
  clickbait headline often predicts the market better than the careful analysts.

---

## Technical Specification

### Model Setup (Cell 1 — runs during instructor intro, ~5 min)
```
!pip install transformers accelerate bitsandbytes torch -q
```
- Download **Qwen/Qwen2.5-7B-Instruct** with 4-bit quantization
- Use `transformers.AutoModelForCausalLM` with `load_in_4bit=True, device_map="auto"`
- Verify GPU, print confirmation
- Header: "Run this cell first, then listen to the instructor!"

### The Earnings Call Transcript (Cell 2 — markdown + Python variable)

Use a **real but curated** earnings call excerpt. Pick ONE of these approaches:

**OPTION A (Preferred):** Hardcode a ~1500-word excerpt from a well-known company's
actual earnings call. Choose one where the stock had a surprising reaction (e.g.,
the company reported good numbers but the stock dropped, or bad numbers but stock
went up). This creates the most dramatic reveals.

Suggested real examples (use public domain transcripts):
- **Meta Q3 2022**: Massive metaverse spending, stock cratered despite revenue beat
- **Netflix Q1 2022**: First subscriber loss ever, stock dropped 35% next day
- **Apple Q4 2018**: Revenue guidance cut, stock dropped 8% after-hours
- **Tesla Q1 2023**: Price cuts discussed, mixed signals, stock volatile

Pick ONE transcript. Include ~1500 words of the most interesting parts (CEO remarks,
CFO guidance, key Q&A moments). Store as a Python string variable.

Also store the ACTUAL outcome:
```python
ACTUAL_OUTCOME = {
    "company": "Meta Platforms",
    "quarter": "Q3 2022",
    "stock_move_1day": -24.6,   # percentage
    "stock_move_5day": -20.1,   # percentage
    "direction": "DOWN",        # UP, DOWN, or FLAT (< +/-2%)
    "key_driver": "Investors spooked by $15B metaverse spending despite revenue beat"
}
```

### Helper Functions (Cell 3 — collapsed/hidden)
- `run_analyst(system_prompt, transcript) -> dict`
  - Sends the transcript to the model with the analyst's system prompt
  - Asks for structured output: recommendation (BUY/HOLD/SELL), confidence (0-100),
    key_findings (list of 3-5 bullet points), one_liner_summary, predicted_move (%)
  - Parses the response, returns a dict
  - If parsing fails, retry once with a more explicit formatting instruction
- `score_analyst(prediction, actual) -> int`
  - Deterministic scoring function (see Scoring Formula below)
- `display_report(agent_name, result, color)` - pretty-print each agent's analysis
- `display_scoreboard(results, actual)` - final comparison table

### The Four Analyst Cells (Cells 4-7 — CLEARLY MARKED "EDIT HERE")

Each cell has a prompt the participant edits. Provide starter prompts that work
but are suboptimal — participants improve them.

**Cell 4: The Bull Agent**
```python
# ================================================================
#  AGENT 1: THE BULL
#  Edit the prompt below to make this agent find bullish signals.
#  The better your prompt, the more accurate the analysis!
# ================================================================

bull_prompt = """
You are a bullish equity research analyst. You believe in this company's
long-term story. Analyze the earnings call transcript and find reasons
to be optimistic.

[Improve this prompt! Think about: What specific signals should the bull
look for? How should it weigh revenue vs. guidance vs. management tone?
Should it compare to market expectations?]
"""
```

**Cell 5: The Bear / Short Seller Agent**
```python
# ================================================================
#  AGENT 2: THE SHORT SELLER
#  Edit the prompt below to make this agent find bearish signals.
# ================================================================

bear_prompt = """
You are a skeptical short seller looking for reasons this stock will drop.
Analyze the earnings call for red flags, deceptive language, and hidden risks.

[Improve this prompt! Think about: What verbal cues indicate management
is hiding something? What financial patterns are concerning? What questions
did management dodge?]
"""
```

**Cell 6: The Journalist Agent**
```python
# ================================================================
#  AGENT 3: THE JOURNALIST
#  Edit the prompt below. Journalists often predict market moves
#  better than analysts because they think about NARRATIVE, not numbers.
# ================================================================

journalist_prompt = """
You are a financial journalist writing a breaking story about this
earnings call. Find the most newsworthy angle — the headline that will
get clicks and move the market.

[Improve this prompt! Think about: What makes a story go viral?
What angle would CNBC lead with? What would scare retail investors?]
"""
```

**Cell 7: The Regulator Agent**
```python
# ================================================================
#  AGENT 4: THE REGULATOR
#  Edit the prompt below. Regulators look for what's NOT said
#  as much as what IS said.
# ================================================================

regulator_prompt = """
You are an SEC examiner reviewing this earnings call for potentially
misleading statements, omissions, or forward-looking statements that
lack adequate qualification.

[Improve this prompt! Think about: What legal/regulatory red flags
exist? Is management being evasive? Are projections qualified properly?]
"""
```

### Run Analysis (Cell 8 — "RUN ANALYSIS" button)
- Run all 4 agents sequentially (parallel would be nice but may OOM on free Colab)
- Show progress: "Running Bull analysis... Done! Running Bear analysis..."
- Display each agent's report as it completes with rich formatting:

```
BULL ANALYST REPORT
====================================
Recommendation: BUY
Confidence: 78/100
Predicted Move: +8%

Key Findings:
- Revenue beat consensus by 3% despite macro headwinds
- User engagement metrics up 15% QoQ
- New product launches signal strong innovation pipeline

One-Liner: "The market is overreacting to spending fears — this is a buying opportunity"
====================================
```

- Use different colors/headers for each agent (Bull=green, Bear=red,
  Journalist=yellow/orange, Regulator=blue)

### The Reveal & Scoring (Cell 9 — auto-runs after analysis)

**First: Display all 4 predictions side by side**
```
PREDICTIONS vs REALITY
============================================================
Agent           Rec    Confidence  Predicted    Actual: -24.6%
------------------------------------------------------------
Bull            BUY    78%         +8.0%        MISS (-32.6 pts off)
Short Seller    SELL   85%         -15.0%       CLOSE (-9.6 pts off)
Journalist      SELL   70%         -20.0%       CLOSE (-4.6 pts off)  <-- BEST!
Regulator       HOLD   45%         -5.0%        MISS (-19.6 pts off)
============================================================
```

**Then: The Participant's Score**
```
YOUR TOTAL ACCURACY SCORE: 67/100

Breakdown:
- Direction accuracy (3/4 agents got direction right):  +40
- Magnitude accuracy (avg distance from actual):        +15
- Confidence calibration (were agents sure when right?): +12

RATING: "Promising Prompt Engineer"
```

**Then: The Twist Reveal (Markdown)**
```
THE SURPRISING TRUTH

The JOURNALIST agent was the most accurate predictor. Why?

Because markets don't move on fundamentals alone — they move on
NARRATIVES. The journalist's job is to find the story that will
spread, and that's exactly what moves stock prices in the short term.

In real studies, Bloomberg terminal headlines predict next-day stock
moves better than analyst models. The story IS the signal.

LESSON FOR YOUR BUSINESS: When you deploy AI agents, the framing
and perspective you give them matters as much as the data. The same
information, analyzed from different angles, produces completely
different conclusions. This is both the power and the danger of
agentic AI.
```

---

## Scoring Formula (Deterministic)

```python
def score_analyst(prediction, actual_move):
    """Score a single agent's prediction. Returns 0-100."""
    score = 0

    # Direction accuracy (40 points)
    pred_direction = "UP" if prediction['predicted_move'] > 2 else ("DOWN" if prediction['predicted_move'] < -2 else "FLAT")
    if pred_direction == actual_direction:
        score += 40
    elif pred_direction == "FLAT":
        score += 20  # partial credit for hedging

    # Magnitude accuracy (40 points)
    distance = abs(prediction['predicted_move'] - actual_move)
    magnitude_score = max(0, 40 - distance * 2)  # lose 2 pts per % off
    score += magnitude_score

    # Confidence calibration (20 points)
    # High confidence + right direction = good. High confidence + wrong = bad.
    if pred_direction == actual_direction:
        score += prediction['confidence'] / 100 * 20
    else:
        score += (100 - prediction['confidence']) / 100 * 20  # rewarded for low confidence when wrong

    return round(score)

def total_score(all_predictions, actual_move):
    """Average across all 4 agents."""
    return round(sum(score_analyst(p, actual_move) for p in all_predictions) / 4)
```

Rating tiers:
- 85-100: "Hedge Fund Material"
- 70-84: "Promising Prompt Engineer"
- 55-69: "The Signals Were There"
- 40-54: "Back to the Drawing Board"
- 0-39: "Your Agents Need Therapy"

---

## Important Implementation Notes

1. **Model**: Use `Qwen/Qwen2.5-7B-Instruct` with `bitsandbytes` 4-bit quant.
   Fallback: `Qwen/Qwen2.5-3B-Instruct` if memory issues.

2. **Structured output**: The model must return JSON-parseable results. In the
   system prompt, include an explicit output format:
   ```
   Respond in EXACTLY this format:
   RECOMMENDATION: BUY/HOLD/SELL
   CONFIDENCE: [number 0-100]
   PREDICTED_MOVE: [percentage, e.g., +5.2 or -12.0]
   KEY_FINDINGS:
   - [finding 1]
   - [finding 2]
   - [finding 3]
   ONE_LINER: [your summary]
   ```
   Parse with regex, not JSON, since 7B models are unreliable with JSON.

3. **Transcript length**: Keep the transcript under 1500 words. 7B models
   struggle with very long contexts. Include the most information-dense parts:
   CEO opening remarks, CFO guidance, and 2-3 analyst Q&A exchanges.

4. **Generation parameters**: temperature=0.7, max_new_tokens=500 per agent.
   Each agent call should take ~30-60 seconds on T4.

5. **Total generation time**: 4 agents * ~45 seconds = ~3 minutes. Acceptable.

6. **The transcript MUST be a real one** (or very closely based on real).
   Finance managers will immediately spot fake earnings language. Use actual
   public filings/transcripts. The Meta Q3 2022 call is ideal because:
   - Everyone knows Meta
   - The stock move was dramatic (-24.6% in one day)
   - The call had genuinely mixed signals (revenue beat but huge CapEx)
   - It's entertaining (Zuckerberg defending the metaverse vision)

7. **Notebook structure**: Colab section headers to organize. Collapse
   infrastructure cells. Make participant cells impossible to miss.
   Use the 🎯 emoji (or similar) ONLY in the cell headers that participants
   need to edit, since this is a game context.

8. **Error handling**: If an agent produces unparseable output, use fallback
   defaults and note "(parsing issue — rerun for better results)" in the display.

9. **Easter eggs / fun details**:
   - If all 4 agents agree on BUY, print "Unanimous bullishness is usually
     a contrarian sell signal..."
   - If all 4 agents agree on SELL, print "When everyone agrees, everyone
     is usually wrong... or it's Enron."
   - Include a "BEST HEADLINE" award for the journalist agent
   - After scoring, print a fake "Bloomberg Terminal" style alert with
     the participant's score

10. **Re-runnability**: Participants should be able to edit prompts and re-run
    analysis without re-downloading the model. The model stays loaded in memory.

---

## Output File
Create the notebook as: `exercise_earnings_call.ipynb`

## Validation Criteria
The notebook is done when:
- [ ] First cell installs deps and downloads model in <5 min on Colab T4
- [ ] Participant only edits 4 prompt cells (one per agent)
- [ ] All 4 analyses complete in <5 min total
- [ ] Score is produced automatically (0-100 number)
- [ ] Actual stock outcome reveal is dramatic and educational
- [ ] The "same data, different conclusions" lesson lands clearly
- [ ] Total exercise time under 30 min including setup
- [ ] Works on Google Colab free tier
- [ ] Real (or very realistic) earnings call transcript is used
