# Agent Task: Build "The Negotiation" Colab Exercise

## Your Mission

Build a **complete, self-contained Google Colab notebook** (`.ipynb`) for a 30-minute coding exercise called **"The Negotiation"**. The audience is finance managers (age 30-50) with almost zero programming experience. They will only edit natural-language prompts — never Python code.

---

## The Exercise Concept

Two AI agents negotiate a **$50M corporate loan**. One agent is the **Bank** (fixed prompt, pre-written by us). The other is the **Borrower** (prompt written by the participant). The agents negotiate for several rounds and must agree on deal terms. The participant's score = how favorable the deal is for the borrower.

### What Participants Do
1. Read the scenario (2 min)
2. Write/edit the Borrower agent's strategy prompt in a clearly marked cell (8 min)
3. Click "Run Negotiation" (watch agents negotiate — ~3 min of generation)
4. See their score, read the transcript, iterate if time permits (remaining time)

### What Makes It Fun
- Agents employ real tactics: anchoring, BATNA references, bluffing, emotional appeals
- Sometimes an agent gets "offended" and walks away (deal fails = score 0)
- The bank agent has hidden flexibility thresholds the participant doesn't know
- Aggressive strategies sometimes backfire spectacularly
- The transcript reads like a real negotiation — participants recognize the dynamics

---

## Technical Specification

### Model Setup (Cell 1 — runs during instructor intro, ~5 min)
```
!pip install transformers accelerate bitsandbytes torch -q
```
- Download **Qwen/Qwen2.5-7B-Instruct** with 4-bit quantization
- Use `transformers.AutoModelForCausalLM` with `load_in_4bit=True, device_map="auto"`
- Verify GPU is available, print confirmation message
- This cell should have a clear header: "Run this cell first, then listen to the instructor!"

### Helper Functions (Cell 2 — collapsed/hidden, participants don't touch)
- `generate_response(system_prompt, conversation_history) -> str`
  - Takes a system prompt and list of message dicts `[{"role": "...", "content": "..."}]`
  - Applies the model's chat template
  - Generates with appropriate parameters (temperature=0.7, max_new_tokens=300)
  - Returns the generated text
- `extract_deal_terms(transcript) -> dict`
  - At end of negotiation, ask the model to extract final agreed terms as JSON
  - Terms to extract: interest_rate (%), loan_term (years), collateral (description),
    covenants (list), prepayment_penalty (%), origination_fee (%)
  - If no deal reached, return None
- `score_deal(deal_terms) -> dict`
  - Score each term on a 0-100 scale for how favorable it is to the borrower
  - Lower interest rate = higher score, longer term = higher score, etc.
  - Return individual scores + weighted total score
  - Scoring formula must be deterministic, not LLM-based

### The Scenario (Cell 3 — markdown, read-only)
Display the scenario in an engaging way:

```
SCENARIO: THE $50M LOAN NEGOTIATION

You are TechForward Inc., a mid-size fintech company seeking a $50M term loan
to fund your expansion into European markets.

YOUR SITUATION:
- Annual revenue: $120M, growing 25% YoY
- Current debt: $15M (small revolving credit facility)
- Credit rating: BBB+
- You have offers from two other banks (your BATNA), but this bank offers
  the best relationship and potential for future business
- You need the money within 60 days

THE BANK:
- MegaBank Corp, a top-10 commercial bank
- They want your business (you're a hot fintech) but have strict risk policies
- Their typical terms for your profile: 6.5-8.5% interest, 5-7 year term
- You don't know their exact flexibility (but it exists!)

NEGOTIABLE TERMS:
- Interest rate (currently offered: 7.8%)
- Loan term (currently offered: 5 years)
- Collateral requirements (currently: full asset pledge)
- Financial covenants (currently: strict EBITDA and leverage ratios)
- Prepayment penalty (currently: 3% in years 1-2, 1.5% in years 3-5)
- Origination fee (currently: 1.25%)

YOUR GOAL: Get the best deal possible for TechForward Inc.
```

### The Bank Agent Prompt (Cell 4 — collapsed/hidden, participants shouldn't see this)
Pre-written, NOT editable. The bank agent should:
- Start firm but have hidden flexibility (can go as low as 5.8% interest, up to 10-year
  term, can waive some covenants, can reduce prepayment penalty)
- Use anchoring (start with terms worse than their actual floor)
- Make concessions gradually and always ask for something in return
- Have a walk-away threshold (if borrower is unreasonable, end negotiation)
- Be professional but occasionally show personality ("Look, I went to bat for you
  with the credit committee...")
- React to different negotiation styles:
  - If borrower is aggressive/threatening -> get defensive, less flexible
  - If borrower is collaborative/creative -> open up, offer creative solutions
  - If borrower bluffs poorly -> call the bluff
  - If borrower provides good business reasoning -> be persuaded

### The Participant's Cell (Cell 5 — CLEARLY MARKED "EDIT HERE")
```python
# ================================================================
#  YOUR NEGOTIATION STRATEGY
#  Edit the text between the triple quotes below.
#  This is the ONLY cell you need to change!
# ================================================================

borrower_strategy = """
You are the CFO of TechForward Inc. negotiating a $50M loan with MegaBank Corp.

YOUR STRATEGY:
[Write your negotiation strategy here. Think about:]
- What's your opening position? (aim high!)
- What tactics will you use? (be specific)
- What's your walk-away point?
- What creative solutions can you propose?
- How will you build rapport with the banker?

EXAMPLE (delete this and write your own):
Start by expressing enthusiasm about the partnership. Open by asking for
5.5% interest rate and a 10-year term. Emphasize our growth trajectory
and the competitive offers from other banks. Be willing to accept
slightly stricter covenants in exchange for a lower rate.
"""
```

### The Negotiation Engine (Cell 6 — "RUN NEGOTIATION" button)
- Run a conversation loop: Bank speaks, Borrower responds, repeat
- Maximum 8 rounds (16 total messages)
- After each round, check if agents have reached agreement or walked away
- Display each message as it's generated with clear formatting:
  ```
  ROUND 1
  BANK: "Thank you for coming in today. We're excited about TechForward's
         growth story. Let me walk you through our initial terms..."

  BORROWER: "Appreciate the warm welcome. We're very interested in building
             a long-term relationship with MegaBank. That said, we've been
             approached by several institutions, and I want to be upfront..."
  ```
- Use colored text or emoji markers for each side (blue for bank, green for borrower)
- Show a progress bar during generation

### Scoring (Cell 7 — auto-runs after negotiation)
Display results in a formatted table:

```
NEGOTIATION RESULTS
===================================================
Deal Status:    AGREED  (or FAILED - walked away)

Term              Offered    Final    Score
---------------------------------------------------
Interest Rate     7.80%     6.20%    82/100
Loan Term         5 yrs     7 yrs    70/100
Collateral        Full      Partial  65/100
Covenants         Strict    Moderate 55/100
Prepayment        3.0%      1.5%     75/100
Origination Fee   1.25%     0.75%    80/100
---------------------------------------------------
TOTAL SCORE:                         72/100

RATING: "Solid Negotiator"

Transcript highlight: "The moment you mentioned the competing
offers from Deutsche Bank, I could feel the banker getting nervous..."
```

Rating tiers (for fun):
- 90-100: "Wall Street Legend"
- 80-89: "Master Negotiator"
- 70-79: "Solid Dealmaker"
- 60-69: "Getting There"
- 50-59: "The Bank Won This One"
- 40-49: "Back to Business School"
- 0-39 or FAILED: "You Got Eaten Alive"

Also generate a 2-3 sentence "highlight reel" comment about the most
interesting moment in the negotiation (generated by the LLM).

### Cheat Sheet (Cell 8 — markdown, visible)
```
PROMPT ENGINEERING TIPS FOR NEGOTIATION

1. BE SPECIFIC: "Ask for 5.5% interest" beats "ask for a lower rate"
2. SET ANCHORS: Start with an ambitious opening position
3. USE BATNA: Mention your alternatives ("We have offers from other banks")
4. TRADE, DON'T JUST ASK: "I'll accept stricter covenants for a lower rate"
5. BUILD RAPPORT: "Express excitement about the long-term relationship"
6. BE CREATIVE: Propose structures the bank hasn't considered
7. READ THE ROOM: Tell your agent to adjust if the banker seems resistant
8. DON'T BLUFF BADLY: If you claim something unrealistic, the bank may call it
```

---

## Scoring Formula (Deterministic)

```python
def score_deal(terms):
    # Interest rate: offered 7.8%, bank floor 5.8%, scale 0-100
    rate_score = max(0, min(100, (7.8 - terms['interest_rate']) / (7.8 - 5.0) * 100))

    # Loan term: offered 5yr, max possible 10yr
    term_score = max(0, min(100, (terms['loan_term'] - 3) / (10 - 3) * 100))

    # Collateral: full=0, partial=50, minimal=80, none=100
    collateral_map = {'full': 0, 'partial': 50, 'minimal': 80, 'none': 100}

    # Covenants: strict=0, moderate=50, light=80, none=100
    covenant_map = {'strict': 0, 'moderate': 50, 'light': 80, 'none': 100}

    # Prepayment: offered 3%, lower is better
    prepay_score = max(0, min(100, (3.0 - terms['prepayment']) / 3.0 * 100))

    # Origination: offered 1.25%, lower is better
    orig_score = max(0, min(100, (1.25 - terms['origination_fee']) / 1.25 * 100))

    # Weighted average (interest rate matters most)
    total = (rate_score * 0.30 + term_score * 0.20 + collateral_score * 0.15 +
             covenant_score * 0.15 + prepay_score * 0.10 + orig_score * 0.10)
    return total
```

If negotiation fails (walk-away): score = 0.

---

## Important Implementation Notes

1. **Model**: Use `Qwen/Qwen2.5-7B-Instruct` with `bitsandbytes` 4-bit quant.
   If Colab RAM is an issue, fall back to `Qwen/Qwen2.5-3B-Instruct`.

2. **Chat template**: Qwen uses a specific chat template. Use the tokenizer's
   `apply_chat_template()` method. Each agent gets a system prompt + the
   conversation history from their perspective.

3. **Conversation management**: The bank sees borrower messages as "user" and
   its own as "assistant" (and vice versa for the borrower). Maintain two
   separate conversation views.

4. **Deal extraction**: After negotiation ends, make one more LLM call asking
   the model to extract the final agreed-upon terms as structured JSON from the
   full transcript. Parse carefully with fallbacks.

5. **Guard against infinite loops**: Cap at 8 rounds. Detect "agreement reached"
   or "walk away" keywords to end early.

6. **Display**: Use IPython.display for rich formatting. Show messages as they
   generate (use print with flush=True at minimum). Clear visual separation
   between rounds.

7. **Notebook structure**: Use Colab section headers to organize. Collapse
   implementation cells. Make the participant cells impossible to miss.

8. **Error handling**: If the model generates garbage, catch gracefully and
   display a fun error message ("The negotiation broke down due to a
   communication failure. Try again!").

9. **Timing**: The negotiation itself (8 rounds of generation) should take
   ~2-4 minutes on T4 with 7B model. Test this.

10. **Fun details**:
    - Add a "dramatic pause" between rounds (1 second sleep)
    - Print "The banker leans back in their chair..." between rounds
    - Sound effect emojis are OK here since it's a game: no emojis in the
      code, but the AGENTS' output can have personality

---

## Output File
Create the notebook as: `exercise_negotiation.ipynb`

## Validation Criteria
The notebook is done when:
- [ ] First cell installs deps and downloads model in <5 min on Colab T4
- [ ] Participant only needs to edit ONE cell (the strategy prompt)
- [ ] Negotiation runs in <5 min
- [ ] Score is produced automatically (0-100 number)
- [ ] Transcript is readable and entertaining
- [ ] Total exercise time is under 30 min including setup
- [ ] Works on Google Colab free tier
