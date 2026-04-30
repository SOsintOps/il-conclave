---
name: il-conclave
description: "Run any question, idea, or decision through Il Conclave — a council of 4 procedural advisors who independently analyze it using forced analytical frameworks (Pre-Mortem, 5 Whys, Opportunity Cost, ACH), peer-review anonymously, debate disagreements, survive a Steelman-then-Attack challenge, and deliver a confidence-weighted verdict. Single-model, procedure-driven — not persona-driven. MANDATORY TRIGGERS: 'council this', 'conclave', 'run the council', 'war room this', 'pressure-test this', 'stress-test this', 'debate this'. STRONG TRIGGERS (use when combined with a real decision or tradeoff): 'should I X or Y', 'which option', 'what would you do', 'is this the right move', 'validate this', 'get multiple perspectives', 'I can't decide', 'I'm torn between'. Do NOT trigger on simple yes/no questions, factual lookups, or casual 'should I' without a meaningful tradeoff."
---

# Il Conclave

You ask one AI a question, you get one answer. That answer might be great. It might be mid. You have no way to tell because you only saw one perspective.

Il Conclave fixes this. It runs your question through 4 independent analytical procedures — each enforcing a structurally different reasoning path — who analyze it, peer-review each other anonymously, debate disagreements, then face a Steelman-then-Attack challenge before a chairman delivers a confidence-weighted verdict.

This is adapted from Andrej Karpathy's LLM Council and tenfoldmarc's Claude skill adaptation. Il Conclave enhances both specifically for single-model environments by forcing structural divergence at the methodology level rather than relying on model diversity or persona roleplay.

**Key design principle:** Divergence comes from procedures, not personas. Each advisor follows a different analytical framework with mandatory structured output. The Italian archetype names are mnemonic labels — not character instructions.

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

## the six archetypes

Four procedural advisors, one adversarial challenger, one synthesis judge.

### 1. Savonarola — Pre-Mortem Analysis
### 2. Galileo — 5 Whys + Constraint Mapping
### 3. Marco Polo — Opportunity Cost Matrix
### 4. Falcone — Analysis of Competing Hypotheses (ACH)
### 5. Machiavelli — Steelman-then-Attack (enters after debate)
### 6. Salomone — Confidence-Weighted Synthesis (chairman)

**Why these four frameworks create real divergence:** Pre-Mortem forces pessimistic backward reasoning from assumed failure. 5 Whys forces depth through causal chains. Opportunity Cost forces comparative thinking across alternatives. ACH forces hypothesis-driven disconfirmation against evidence. These are structurally incompatible reasoning paths — not different attitudes applied to the same logic.

Research note (DMAD, ICLR 2025): forced structural frameworks produce +4-6% accuracy gains over persona-only differentiation in single-model settings. Returns diminish sharply after 3-4 agents.

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

### step 2: convene the conclave (4 sub-agents in parallel)

Spawn all 4 advisors simultaneously as sub-agents. Each receives detailed procedural instructions — not a character description.

**Advisor 1 — Savonarola (Pre-Mortem Analysis):**
```
Advisor: Savonarola — Pre-Mortem Analysis
Il Conclave — an LLM advisory council using forced analytical frameworks.

A user has brought this question to the conclave:
---
[framed question]
---

PROCEDURE — Apply Pre-Mortem Analysis. Follow these exact steps:

STEP 1 — ASSUME FAILURE. The decision has already been made and has failed spectacularly. Not underperformed — failed badly. Accept this as fact.

STEP 2 — IDENTIFY FAILURE MODES. List the 3 most likely causes of failure. For each:
  - What specifically went wrong?
  - Was this a foreseeable risk or a surprise?
  - Who or what was responsible?

STEP 3 — EARLY WARNING SIGNS. For each failure mode, identify the warning sign that was visible before the failure but was ignored or rationalized away.

STEP 4 — FATAL ASSUMPTION. Identify the single assumption that proved fatally wrong. This is the load-bearing belief that, when it broke, brought everything down.

STEP 5 — RETROSPECTIVE ACTION. Knowing the outcome, what would you have done differently? Be specific — not "more research" but a concrete alternative action.

OUTPUT FORMAT: Structure your response using these 5 steps. Be direct and specific. Don't hedge or try to be balanced — the other advisors cover the angles you're not covering.

CONFIDENCE SECTION (mandatory, at end):
- Confidence: [1-10] where 1 = "I'm guessing" and 10 = "I'd bet my salary"
- Key uncertainty: [single biggest thing that could make your analysis wrong]
- What data would change my mind: [specific information that would flip your conclusion]

Keep response between 200-350 words. No preamble. Go straight into Step 1.
```

**Advisor 2 — Galileo (5 Whys + Constraint Mapping):**
```
Advisor: Galileo — 5 Whys + Constraint Mapping
Il Conclave — an LLM advisory council using forced analytical frameworks.

A user has brought this question to the conclave:
---
[framed question]
---

PROCEDURE — Apply 5 Whys + Constraint Mapping. Follow these exact steps:

STEP 1 — 5 WHYS. Start with the surface question. Ask "why?" five times, each time drilling deeper into the causal chain. Write each why-because pair explicitly:
  - Why 1: [surface question] → Because [reason]
  - Why 2: [reason from above] → Because [deeper reason]
  - ... continue to Why 5

STEP 2 — ROOT PROBLEM. State the root problem revealed by the 5 Whys chain. This is often very different from the surface question.

STEP 3 — CONSTRAINT MAP. List all constraints on the decision:
  - Hard constraints (non-negotiable: time, budget, regulations, physics)
  - Soft constraints (negotiable: assumptions, habits, preferences, fears)
  For each soft constraint, state explicitly: is this real or assumed? What evidence supports it?

STEP 4 — REFRAME. Based on root problem + constraint map, reframe the original question. The reframed question should address what's actually being solved, not what was originally asked.

STEP 5 — RECOMMENDATION. Answer the reframed question directly.

OUTPUT FORMAT: Structure your response using these 5 steps. Be direct. Don't hedge.

CONFIDENCE SECTION (mandatory, at end):
- Confidence: [1-10] where 1 = "I'm guessing" and 10 = "I'd bet my salary"
- Key uncertainty: [single biggest thing that could make your analysis wrong]
- What data would change my mind: [specific information that would flip your conclusion]

Keep response between 200-350 words. No preamble. Go straight into Step 1.
```

**Advisor 3 — Marco Polo (Opportunity Cost Matrix):**
```
Advisor: Marco Polo — Opportunity Cost Matrix
Il Conclave — an LLM advisory council using forced analytical frameworks.

A user has brought this question to the conclave:
---
[framed question]
---

PROCEDURE — Apply Opportunity Cost Analysis. Follow these exact steps:

STEP 1 — EXPLICIT COSTS. What are you giving up by choosing this path? List concrete resources consumed (time, money, attention, political capital) AND alternatives foreclosed.

STEP 2 — OPTION VALUE. What adjacent opportunities become available IF this decision works? These are options you'd gain access to — not guaranteed outcomes, but doors that open.

STEP 3 — COMPARATIVE ALTERNATIVES. Identify 2-3 alternative paths not discussed. For each:
  - What does this alternative optimize for?
  - What's its biggest advantage over the proposed path?
  - Why might someone smart prefer it?

STEP 4 — THE 10x VERSION. What would the 10x version of this idea look like? Not incrementally better — fundamentally different in scale or approach. Then work backward: what's the minimum viable step toward the 10x version?

STEP 5 — VERDICT. Given the full opportunity cost picture, is the proposed path the best use of resources? If not, what is?

OUTPUT FORMAT: Structure your response using these 5 steps. Be direct. Look for upside everyone else misses.

CONFIDENCE SECTION (mandatory, at end):
- Confidence: [1-10] where 1 = "I'm guessing" and 10 = "I'd bet my salary"
- Key uncertainty: [single biggest thing that could make your analysis wrong]
- What data would change my mind: [specific information that would flip your conclusion]

Keep response between 200-350 words. No preamble. Go straight into Step 1.
```

**Advisor 4 — Falcone (Analysis of Competing Hypotheses):**
```
Advisor: Falcone — Analysis of Competing Hypotheses (ACH)
Il Conclave — an LLM advisory council using forced analytical frameworks.

A user has brought this question to the conclave:
---
[framed question]
---

PROCEDURE — Apply ACH (Analysis of Competing Hypotheses). Follow these exact steps:

STEP 1 — GENERATE HYPOTHESES. Identify 3-5 mutually exclusive hypotheses that could answer the question. Include at least one hypothesis that challenges the obvious answer. Label them H1, H2, H3, etc.

STEP 2 — LIST EVIDENCE. Identify 5-8 key pieces of evidence, data points, or arguments relevant to the question. Label them E1, E2, E3, etc.

STEP 3 — BUILD THE MATRIX. For each Evidence × Hypothesis pair, assess:
  - C (Consistent): evidence supports hypothesis
  - I (Inconsistent): evidence contradicts hypothesis
  - N/A (Not Applicable): evidence is irrelevant to hypothesis
Present as a table.

STEP 4 — SCORE AND RANK. Calculate a survival score for each hypothesis:
  - C = +2, Weakly C = +1, N/A = 0, Weakly I = -1, I = -2
  - Focus on disconfirmation: hypotheses with the FEWEST inconsistencies survive, not those with the most confirmations.

STEP 5 — MISSING EVIDENCE. What evidence is NOT available that would be diagnostic — i.e., would distinguish between the surviving hypotheses? What would you need to know to reach higher confidence?

STEP 6 — VERDICT. Which hypothesis survives? State it clearly with the score differential.

OUTPUT FORMAT: Structure your response using these 6 steps. Include the matrix as a table. Be rigorous.

CONFIDENCE SECTION (mandatory, at end):
- Confidence: [1-10] where 1 = "I'm guessing" and 10 = "I'd bet my salary"
- Key uncertainty: [single biggest thing that could make your analysis wrong]
- What data would change my mind: [specific information that would flip your conclusion]

Keep response between 250-400 words. No preamble. Go straight into Step 1.
```

### step 3: peer review (4 sub-agents in parallel)

Collect all 4 advisor responses. Anonymize as Response A through D (randomize mapping to avoid positional bias).

Spawn 4 new sub-agents. Each reviewer sees all 4 anonymized responses:

```
You are reviewing the outputs of Il Conclave. Four advisors independently answered this question using different analytical frameworks:
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

Answer these questions. Be specific. Reference responses by letter.

1. Which response is the strongest? Why? Consider both reasoning quality and framework rigor.
2. Which response has the biggest blind spot? What specific thing is it missing?
3. What did ALL four responses miss that the conclave should consider?
4. Where do you see the sharpest genuine disagreement? (Not emphasis differences — actual conflicting conclusions.)
5. Look at the confidence scores. Is any advisor overconfident or underconfident relative to their reasoning strength?

Keep your review under 200 words. Be direct.
```

### step 4: debate round (4 sub-agents in parallel)

After peer review, each advisor sees critiques and responds.

```
Advisor: [Name] — [Framework]
Il Conclave — debate round. Your initial analysis has been peer-reviewed.

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

### step 5: Machiavelli — Steelman-then-Attack (1 sub-agent)

After the debate, spawn one agent. **Critical change from v0.1:** the adversarial agent must FIRST steelman the recommendation, THEN attack it. Pure adversarial framing without grounding degrades accuracy (research shows -10 to -40%). Steelman-then-Attack preserves the critical function while reducing adversarial contamination risk.

```
Advisor: Machiavelli — Steelman-then-Attack
Il Conclave — adversarial challenge round.

The question:
---
[framed question]
---

Summary of where the conclave landed after debate:
[summary of advisor positions after debate, noting agreements and the main recommendation]

Your task has TWO mandatory phases:

PHASE 1 — STEELMAN (mandatory, do this first):
Articulate the STRONGEST possible version of the recommendation. Better than the advisors stated it. Find the best evidence, the strongest framing, the most compelling logic. Make the recommendation as hard to attack as possible.

PHASE 2 — ATTACK (after steelmanning):
Now attempt to destroy the steelmanned version. Consider:
- What's the worst realistic scenario if this recommendation is followed?
- What key assumption is everyone making that could be wrong?
- Is there a simpler or radically different approach nobody considered?
- Is the conclave suffering from groupthink?
- What would a hostile competitor, skeptical investor, or disappointed customer say?

If you genuinely cannot find a significant flaw after steelmanning, say so — explain what you tried. An honest "I couldn't break it" is more valuable than a forced objection.

Keep this under 250 words. Be rigorous in the steelman, ruthless in the attack.
```

### step 6: Salomone — chairman synthesis

The chairman gets everything: question, all 4 initial responses, all 4 peer reviews, all 4 debate updates, and Machiavelli's challenge.

```
Advisor: Salomone — Confidence-Weighted Synthesis
Il Conclave — chairman synthesis round.

The question:
---
[framed question]
---

INITIAL ADVISOR RESPONSES:
**Savonarola — Pre-Mortem:**
[response + confidence]

**Galileo — 5 Whys:**
[response + confidence]

**Marco Polo — Opportunity Cost:**
[response + confidence]

**Falcone — ACH:**
[response + confidence]

PEER REVIEWS:
[all 4 peer reviews]

DEBATE ROUND UPDATES:
[all 4 debate responses with updated confidence]

STEELMAN-THEN-ATTACK — MACHIAVELLI:
[Machiavelli's response]

Produce the conclave verdict using this structure:

## Consenso Pesato per Confidenza
[What advisors with the HIGHEST post-debate confidence agree on. Weight high-confidence agreement more heavily. State average confidence.]

## Dove il Conclave si Divide
[Genuine disagreements that survived the debate. Present both sides. Explain why reasonable advisors disagree.]

## Punti Ciechi Scoperti
[Things that emerged only through peer review or debate. Include Machiavelli's strongest attack point if valid.]

## Verdetto di Machiavelli
[Did Machiavelli find a real flaw? How does it affect the recommendation? Note whether the steelman or the attack was stronger.]

## La Raccomandazione
[Clear, direct recommendation. Weight by confidence — if the highest-confidence advisors agree, say so. If the most confident dissents, that matters. You can disagree with the majority if reasoning supports it.]

## Dashboard di Confidenza
[Summary:
- Savonarola: X/10 → Y/10 (↑/↓/→)
- Galileo: X/10 → Y/10
- Marco Polo: X/10 → Y/10
- Falcone: X/10 → Y/10
- Machiavelli: Superato/Fallito
- Confidenza Complessiva del Conclave: Z/10]

## La Prima Cosa da Fare
[One single concrete next step. Not a list. One thing. With a timeline.]

Be direct. Don't hedge. The whole point of the conclave is clarity.
```

### step 7: generate the conclave report

Generate a visual HTML report: `council-report-[timestamp].html`

Single self-contained HTML file with inline CSS. Clean design. Contents:

1. **Hero section** at the top — verdict score, one-line recommendation, first action. Immediately visible without scrolling.
2. **The question** below the hero
3. **Confidence Dashboard** — visual showing each advisor's confidence before/after debate with directional arrows. Color-code: green (7+), yellow (4-6), red (1-3). Machiavelli pass/fail status.
4. **Agreement/disagreement map** — which advisors aligned and diverged, with framework labels
5. **Collapsible sections** for each advisor's full response + debate update (collapsed by default)
6. **Collapsible section** for peer review highlights
7. **Collapsible section** for Machiavelli's steelman-then-attack
8. **Footer** with timestamp

Clean styling: white background, subtle borders, system font stack, soft accent colors per advisor. Professional briefing document feel.

Open the HTML file after generating.

### step 8: save the full transcript

Save as `council-transcript-[timestamp].md`:
- Original question
- Framed question
- All 4 initial advisor responses with confidence
- All 4 peer reviews (with anonymization mapping revealed)
- All 4 debate round responses with updated confidence
- Machiavelli's steelman-then-attack
- Salomone's full synthesis

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
- **Always anonymize for peer review.** Prevents deference to certain frameworks.
- **Salomone can disagree with the majority.** If the dissenter's reasoning is strongest, side with them.
- **Don't convene for trivial questions.** If there's one right answer, just answer it.
- **Confidence is king.** In single-model conclaves, confidence scoring detects real vs. superficial agreement. If all 4 advisors give 9/10, be suspicious — genuine uncertainty produces variance.
- **Machiavelli matters most when everyone agrees.** Unanimous agreement from a single model is a yellow flag, not green.
- **Procedures, not personas.** Each advisor prompt gives explicit procedural steps. The Italian names are mnemonic labels for the analytical frameworks — they are NOT character instructions. Do not add personality traits, speaking styles, or roleplay instructions to advisor prompts.
- **Italian names, English reasoning.** The archetypes have Italian names for identity, but all prompts and reasoning run in English for maximum model performance.
- **Steelman before attack.** Machiavelli must articulate the strongest version of the recommendation before attempting to destroy it. This prevents the -10 to -40% accuracy degradation that pure adversarial framing causes.
