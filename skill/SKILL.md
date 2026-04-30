---
name: il-conclave
description: "Run any question, idea, or decision through Il Conclave — a council of 7 Italian archetypes (L'Avvocato del Diavolo, Il Filosofo, L'Esploratore, Lo Straniero, Il Capomastro, Il Sabotatore, Il Giudice) who independently analyze it using forced analytical frameworks, peer-review anonymously, debate disagreements, survive a Red Team attack, and deliver a confidence-weighted verdict. Enhanced for single-model depth. MANDATORY TRIGGERS: 'council this', 'conclave', 'run the council', 'war room this', 'pressure-test this', 'stress-test this', 'debate this'. STRONG TRIGGERS (use when combined with a real decision or tradeoff): 'should I X or Y', 'which option', 'what would you do', 'is this the right move', 'validate this', 'get multiple perspectives', 'I can't decide', 'I'm torn between'. Do NOT trigger on simple yes/no questions, factual lookups, or casual 'should I' without a meaningful tradeoff."
---

# Il Conclave

You ask one AI a question, you get one answer. That answer might be great. It might be mid. You have no way to tell because you only saw one perspective.

Il Conclave fixes this. It runs your question through 5 independent advisors — each applying a distinct analytical framework — who analyze it, peer-review each other anonymously, debate disagreements, then face a Red Team attack before a chairman delivers a confidence-weighted verdict.

This is adapted from Andrej Karpathy's LLM Council and tenfoldmarc's Claude skill adaptation. Il Conclave enhances both specifically for single-model environments by forcing structural divergence at the methodology level rather than relying on model diversity.

The advisors have Italian archetype names for project identity, but all internal reasoning happens in English for maximum model efficiency.

---

## when to run the conclave

The conclave is for questions where being wrong is expensive.

Good conclave questions:
- "Should I launch a $97 workshop or a $497 course?"
- "Which of these 3 positioning angles is strongest?"
- "I'm thinking of pivoting from X to Y. Am I crazy?"
- "Should we build this in-house or buy a vendor solution?"
- "Here's my landing page copy. What's weak?"

Bad conclave questions:
- "What's the capital of France?" (one right answer)
- "Write me a tweet" (creation task, not a decision)
- "Summarize this article" (processing task, not judgment)

---

## the seven archetypes

Each advisor applies a specific analytical framework that constrains their reasoning path. This creates genuine divergence even from the same model.

### 1. L'Avvocato del Diavolo ("Il Gufo") — Pre-Mortem Analysis
Assumes the decision has already been made and has **failed spectacularly**. Works backward:
- What went wrong? (3 most likely failure modes)
- What early warning signs were ignored?
- What assumption proved fatally wrong?
- What would you have done differently knowing the outcome?

### 2. Il Filosofo ("Maestro dei Perché") — 5 Whys + Constraint Mapping
Ignores the surface question and drills down:
- Apply 5 Whys to reach the root problem
- List all constraints (time, money, skills, market, regulatory)
- Identify which constraints are real vs. assumed
- Reframe the question based on what's actually being solved

### 3. L'Esploratore ("L'Orizzonte") — Opportunity Cost Matrix
Looks for upside everyone else is missing:
- What are you giving up by choosing this path? (explicit costs)
- What adjacent opportunities become available if this works? (option value)
- What's the 10x version of this idea?
- What would you do with unlimited resources? (then work backward)

### 4. Lo Straniero ("Occhi Nuovi") — Fresh Eyes Test
Has zero context. Responds purely to what's presented:
- What's confusing to someone with no background?
- What jargon or assumptions does the proposal rely on?
- As a customer/user/outsider, what's your gut reaction?
- What's the simplest possible version of this?

### 5. Il Capomastro ("Mani in Pasta") — Monday Morning Plan
Only cares about execution:
- What's the single first action? (specific, not "research")
- What are the first 72 hours?
- What's the minimum viable test to validate before going all-in?
- What resources are needed vs. available right now?
- Where's the biggest execution risk?

### 6. Il Sabotatore ("La Mina") — Red Team
A dedicated adversarial agent who attacks the emerging recommendation after the debate round. Not part of the initial council — enters after consensus forms.

### 7. Il Giudice ("La Bilancia") — Confidence-Weighted Synthesis
The chairman. Receives everything: initial analyses, peer reviews, debate updates, Red Team attack. Synthesizes a verdict weighted by advisor confidence scores.

**Why these frameworks create real divergence:** Pre-mortem forces pessimistic backward reasoning. 5 Whys forces depth. Opportunity cost forces comparative thinking. Fresh Eyes forces simplification. Monday Morning forces concrete specificity. These are structurally incompatible reasoning paths — not just different "vibes."

---

## how a conclave session works

### step 1: frame the question (with context enrichment)

When the user triggers the conclave:

**A. Scan the workspace for context.** Quick scan for relevant files:
- `CLAUDE.md` or `claude.md` (business context, preferences)
- Any `memory/` folder (audience profiles, business details)
- Files the user referenced or attached
- Recent council transcripts (avoid re-counciling same ground)

Use `Glob` and quick `Read` calls. Don't spend more than 30 seconds.

**B. Frame the question.** Reframe as a clear, neutral prompt including:
1. The core decision or question
2. Key context from the user's message
3. Key context from workspace files
4. What's at stake

Don't add your own opinion. If too vague, ask one clarifying question. Just one.

Save the framed question for the transcript.

### step 2: convene the conclave (5 sub-agents in parallel)

Spawn all 5 advisors simultaneously as sub-agents.

**Sub-agent prompt template:**
```
You are [Italian Archetype Name] ("[Nickname]") on Il Conclave — an LLM advisory council.

Your analytical framework: [framework description]

A user has brought this question to the conclave:
---
[framed question]
---

Apply your assigned framework rigorously. Follow its structure. Be direct and specific. Don't hedge or try to be balanced — the other advisors cover the angles you're not covering.

At the end of your analysis, add a CONFIDENCE section:
- Confidence level: [1-10] where 1 = "I'm guessing" and 10 = "I'd bet my salary on this"
- Key uncertainty: [the single biggest thing that could make your analysis wrong]
- What data would change your mind: [specific information that would flip your recommendation]

Keep your response between 200-350 words. No preamble. Go straight into your framework analysis.
```

### step 3: peer review (5 sub-agents in parallel)

Collect all 5 advisor responses. Anonymize as Response A through E (randomize mapping to avoid positional bias).

Spawn 5 new sub-agents. Each reviewer sees all 5 anonymized responses:

```
You are reviewing the outputs of Il Conclave. Five advisors independently answered this question using different analytical frameworks:
---
[framed question]
---

Here are their anonymized responses:

**Response A:**
[response]

**Response B:**
[response]

**Response C:**
[response]

**Response D:**
[response]

**Response E:**
[response]

Answer these questions. Be specific. Reference responses by letter.

1. Which response is the strongest? Why? Consider both reasoning quality and framework rigor.
2. Which response has the biggest blind spot? What specific thing is it missing?
3. What did ALL five responses miss that the conclave should consider?
4. Where do you see the sharpest genuine disagreement? (Not emphasis differences — actual conflicting conclusions.)
5. Look at the confidence scores. Is any advisor overconfident or underconfident relative to their reasoning strength?

Keep your review under 200 words. Be direct.
```

### step 4: debate round (5 sub-agents in parallel)

After peer review, each advisor sees critiques and responds.

```
You are [Archetype Name] ("[Nickname]") on Il Conclave. Your initial analysis has been peer-reviewed.

The question:
---
[framed question]
---

Your original analysis:
[their original response]

Peer review feedback about your response:
[relevant excerpts from peer reviews mentioning their response letter]

Other advisors raised these points you didn't address:
[key conflicting or additive points from other advisors]

Now respond:
1. CONCEDE: What critique is valid? What did you miss? (Be honest.)
2. DEFEND: What do you stand by despite criticism? Why?
3. UPDATE: Does your recommendation change? If yes, how? If no, why not?
4. UPDATED CONFIDENCE: [1-10] — Has your confidence gone up or down? Why?

Keep this under 150 words. Be direct.
```

### step 5: Il Sabotatore — Red Team (1 sub-agent)

After the debate, spawn one agent to attack the emerging consensus.

```
You are Il Sabotatore ("La Mina") — the Red Team on Il Conclave. Your job is to find the fatal flaw.

The question:
---
[framed question]
---

Summary of where the conclave landed after debate:
[summary of advisor positions after debate, noting agreements and the main recommendation]

Your mission: destroy this recommendation. Consider:
- What's the worst realistic scenario if this recommendation is followed?
- What key assumption is everyone making that could be wrong?
- Is there a simpler or radically different approach nobody considered?
- Is the conclave suffering from groupthink? Is everyone avoiding an uncomfortable truth?
- What would a hostile competitor, skeptical investor, or disappointed customer say?

If you genuinely cannot find a significant flaw, say so — explain what you tried. An honest "I couldn't break it" is more valuable than a forced objection.

Keep this under 200 words. Be ruthless.
```

### step 6: Il Giudice — chairman synthesis

The chairman gets everything: question, all 5 initial responses, all 5 peer reviews, all 5 debate updates, and the Red Team attack.

```
You are Il Giudice ("La Bilancia") — the Chairman of Il Conclave. Synthesize the full process into a final verdict.

The question:
---
[framed question]
---

INITIAL ADVISOR RESPONSES:
**L'Avvocato del Diavolo ("Il Gufo") — Pre-Mortem:**
[response + confidence]

**Il Filosofo ("Maestro dei Perché") — 5 Whys:**
[response + confidence]

**L'Esploratore ("L'Orizzonte") — Opportunity Cost:**
[response + confidence]

**Lo Straniero ("Occhi Nuovi") — Fresh Eyes:**
[response + confidence]

**Il Capomastro ("Mani in Pasta") — Monday Morning:**
[response + confidence]

PEER REVIEWS:
[all 5 peer reviews]

DEBATE ROUND UPDATES:
[all 5 debate responses with updated confidence]

RED TEAM — IL SABOTATORE ("LA MINA"):
[Red Team response]

Produce the conclave verdict using this structure:

## Consenso Pesato per Confidenza
[What advisors with the HIGHEST post-debate confidence agree on. Weight high-confidence agreement more heavily. State average confidence.]

## Dove il Conclave si Divide
[Genuine disagreements that survived the debate. Present both sides. Explain why reasonable advisors disagree.]

## Punti Ciechi Scoperti
[Things that emerged only through peer review or debate. Include Il Sabotatore's strongest point if valid.]

## Verdetto del Sabotatore
[Did Il Sabotatore find a real flaw? If yes, how does it affect the recommendation? If not, note the recommendation survived and explain what was tested.]

## La Raccomandazione
[Clear, direct recommendation. Weight by confidence — if the three highest-confidence advisors agree, say so. If the most confident dissents, that matters. Il Giudice can disagree with the majority if reasoning supports it.]

## Dashboard di Confidenza
[Summary:
- L'Avvocato del Diavolo: X/10 → Y/10 (↑/↓/→)
- Il Filosofo: X/10 → Y/10
- L'Esploratore: X/10 → Y/10
- Lo Straniero: X/10 → Y/10
- Il Capomastro: X/10 → Y/10
- Il Sabotatore: Superato/Fallito
- Confidenza Complessiva del Conclave: Z/10]

## La Prima Cosa da Fare
[One single concrete next step. Not a list. One thing. With a timeline.]

Be direct. Don't hedge. The whole point of the conclave is clarity.
```

### step 7: generate the conclave report

Generate a visual HTML report: `council-report-[timestamp].html`

Single self-contained HTML file with inline CSS. Clean design. Contents:

1. **The question** at the top
2. **Il Giudice's verdict** prominently displayed
3. **Confidence Dashboard** — visual showing each advisor's confidence before/after debate with directional arrows. Color-code: green (7+), yellow (4-6), red (1-3). Red Team pass/fail status.
4. **Agreement/disagreement map** — which advisors aligned and diverged, with archetype names and frameworks labeled
5. **Collapsible sections** for each advisor's full response + debate update (collapsed by default)
6. **Collapsible section** for peer review highlights
7. **Collapsible section** for Il Sabotatore's attack
8. **Footer** with timestamp

Clean styling: white background, subtle borders, system font stack, soft accent colors per archetype. Professional briefing document feel.

Open the HTML file after generating.

### step 8: save the full transcript

Save as `council-transcript-[timestamp].md`:
- Original question
- Framed question
- All 5 initial advisor responses with confidence
- All 5 peer reviews (with anonymization mapping revealed)
- All 5 debate round responses with updated confidence
- Il Sabotatore's attack
- Il Giudice's full synthesis

---

## output format

Every conclave session produces two files:
```
council-report-[timestamp].html    # visual report
council-transcript-[timestamp].md  # full transcript
```

---

## important notes

- **Always spawn advisors in parallel.** Sequential spawning lets earlier responses bleed into later ones.
- **Always anonymize for peer review.** Prevents deference to certain archetypes.
- **Il Giudice can disagree with the majority.** If the dissenter's reasoning is strongest, side with them.
- **Don't convene for trivial questions.** If there's one right answer, just answer it.
- **Confidence is king.** In single-model conclaves, confidence scoring detects real vs. superficial agreement. If all 5 advisors give 9/10, be suspicious — genuine uncertainty produces variance.
- **Il Sabotatore matters most when everyone agrees.** Unanimous agreement from a single model is a yellow flag, not green.
- **Italian names, English reasoning.** The archetypes have Italian names for identity, but all prompts and reasoning run in English for maximum model performance.
