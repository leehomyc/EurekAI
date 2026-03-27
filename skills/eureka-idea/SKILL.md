---
name: eureka-idea
description: Generate ONE deep research idea by absorbing the full chain-of-thought reasoning of ALL 116 landmark papers. Reads top_papers_cot.json, internalizes every thinking pattern (dead ends, reframings, eureka moments, brain jumps), then thinks extremely long and deep to produce a single breakthrough idea. Use when user says "eureka idea", "deep brainstorm", "think like top researchers", or wants CoT-driven idea generation.
argument-hint: [research-direction]
allowed-tools: Bash(*), Read, Write, Grep, Glob, WebSearch, WebFetch, Agent
---

# Eureka Idea Generator

Generate ONE deeply reasoned research idea for: $ARGUMENTS

## Overview

This skill generates a SINGLE research idea by absorbing the chain-of-thought reasoning traces of ALL 116 landmark papers across AI, Physics, and Mathematics. No filtering, no selection — you study every paper's thinking process, internalize the full spectrum of how breakthroughs actually happen, and then push as far as you possibly can on the user's research direction.

The philosophy: one idea thought through to the bone beats ten shallow ones. Think like you're writing the chain of thought for paper #117 — the one that doesn't exist yet.

## Source Data

`top_papers_cot.json` in the project root contains:
- **116 papers** with 15-25 step chain-of-thought traces each (~2,246 total reasoning steps)
- Fields per paper: `persona`, `problem_statement`, `prior_work_and_limitations`, `observations`, `chain_of_thought` (step-by-step with dead ends & eureka moments), `key_insight`, `methodology`
- Domains: AI (100), Physics (8), Mathematics (8)
- Spans from Turing (1950) to modern frontier models — the full arc of how ideas evolve

## Workflow

### Step 1: Absorb ALL 116 Thinking Processes

Read `top_papers_cot.json` from the project root. **Read ALL of it.** Do not skip, sample, or summarize. You must study every single paper's full chain of thought.

Since the file is ~1MB, read it in chunks (e.g., 200 lines at a time) until you have processed every paper. For each paper, internalize:

- The **persona** — who was this researcher, what was their background, what lens did they see the world through?
- The **problem statement** — what frustrated them about the state of the field?
- The **full chain of thought** — every step, including:
  - Where they got stuck and what they tried that failed
  - The moment they reframed the problem
  - The unexpected connection that changed everything
  - The eureka moment and why it worked
- The **key insight** — the distilled breakthrough

As you read, build a mental catalog of **thinking moves** — the recurring patterns across all 116 papers:
- **Reframing**: Turing didn't solve "can machines think?" — he replaced the question entirely
- **Inversion**: GANs didn't learn to generate directly — they learned by training a critic
- **Simplification**: Rosenblatt didn't need meaningful first-layer connections — random projections sufficed
- **Cross-domain transfer**: Boltzmann machines borrowed from statistical mechanics
- **Scaling past a phase transition**: GPT-3 showed that quantity produces qualitative change
- **Challenging sacred assumptions**: BatchNorm questioned whether we need careful initialization
- **Unifying seemingly separate problems**: Transformers showed attention is all you need for sequence, translation, generation...
- **Finding hidden structure**: Galois didn't just prove quintics are unsolvable — he found the group structure that explains *why*

You are not selecting exemplars. You are absorbing the entire history of how breakthroughs happen.

### Step 2: Understand the Research Direction

Take the user's research direction and the landscape/gaps from Phase 1 (if coming from `/idea-creator`). If no landscape is provided, do a quick literature scan using WebSearch to understand:
- What has been tried in the last 2 years
- What the main open problems are
- Where the community is stuck

### Step 3: Think. Very Long. Very Deep. Push Very Far.

This is the core of the skill. You must generate a chain of thought with **25-40 steps** — longer and deeper than any of the 116 exemplar papers. This is not padding; every step must advance the thinking.

**The thinking process must include:**

1. **Start with genuine frustration** (steps 1-3): What's wrong with the current state of the field? What have people tried? Why is it unsatisfying? Don't just list limitations — feel them. What keeps a researcher up at night about this problem?

2. **First attempt — and failure** (steps 4-7): Try the most obvious approach. Work through it in detail. Show exactly where and why it breaks. This is not a straw man — it should be a real, serious attempt that fails for a non-trivial reason.

3. **Second attempt — partial progress** (steps 8-11): Try a different angle, informed by why the first attempt failed. Get further this time. Maybe it works in a special case but not generally. Or it works but requires something impractical. Identify what's still missing.

4. **Step back and question assumptions** (steps 12-15): What is everyone in the field taking for granted? What implicit assumption underlies both failed attempts? Is there a paper from the 116 where someone made a similar move — questioning what everyone assumed? Draw on the thinking patterns you absorbed. This is where cross-domain connections happen.

5. **The brain jump** (steps 16-20): Make an unexpected connection. Maybe it comes from physics, mathematics, biology, or a completely different subfield of ML. Maybe it comes from inverting the problem, or from noticing that two things everyone treats as separate are actually the same thing. This should feel surprising but inevitable in hindsight. Work through why this connection is deep, not superficial.

6. **Develop the insight** (steps 21-28): Turn the brain jump into a concrete method. What does the architecture/algorithm/framework look like? What are the key design choices? What makes it different from existing approaches at a fundamental level — not just "we add module X" but "we reconceptualize the problem as..."?

7. **Stress-test and refine** (steps 29-35): Play devil's advocate. What would Hinton say? What would Bengio push back on? What would a reviewer at NeurIPS object to? Address each objection. Some will require modifying the idea. Some will reveal deeper strengths.

8. **The final crystallization** (steps 36-40): The idea in its mature form. Why it works. Why it matters. What it changes about how we think about the problem. The "if this is right, then..." implications.

**Critical rules for the thinking process:**
- **No shortcuts**: Do not jump to the answer. The dead ends are not filler — they are where the real thinking happens.
- **No fake struggle**: If a step doesn't genuinely advance or redirect the thinking, delete it. Every step must earn its place.
- **Draw on ALL 116 papers**: Your thinking should be visibly informed by the patterns you absorbed. Not by citing them explicitly in every step, but by making the same types of moves — the reframings, the inversions, the cross-domain leaps.
- **Push past the obvious**: When you think you've found the idea, ask "is this really the deepest version of this?" Push further. The first eureka moment is rarely the final one.
- **Be specific**: Vague ideas ("we could use attention mechanisms for X") are worthless. The idea must be concrete enough that a PhD student could start implementing it tomorrow.

### Step 4: Self-Critique via Researcher Personas

Adopt the persona of 3-5 researchers from the CoT database whose work is most relevant. For each, ask:

- "Would [Researcher] find this idea genuinely novel, or would they say 'this is just X with extra steps'?"
- "What would [Researcher] change about this approach?"
- "What experiment would [Researcher] want to see first?"

If the personas are not impressed, **go back to Step 3 and push deeper**. Do not output a mediocre idea.

### Step 5: Output

Produce TWO outputs:

#### Output A: `eureka_ideas.json`

Write to `eureka_ideas.json` in the project root:

```json
{
  "metadata": {
    "description": "AI-generated research idea using eureka-style chain-of-thought reasoning",
    "research_direction": "[user's direction]",
    "generated_date": "[date]",
    "papers_studied": 116,
    "total_cot_steps_absorbed": 2246
  },
  "ideas": [
    {
      "id": 1,
      "title": "[proposed paper title]",
      "domain": "[domain]",
      "subfield": "[subfield]",
      "problem_statement": "[what problem this solves — 2-3 sentences]",
      "prior_work_and_limitations": "[what exists and why it's insufficient — detailed paragraph]",
      "observations": "[key observations that seed the idea — what did you notice that others missed?]",
      "chain_of_thought": [
        {"step": 1, "thought": "..."},
        {"step": 2, "thought": "..."},
        ...25-40 steps...
      ],
      "key_insight": "[the core eureka moment — one detailed paragraph]",
      "methodology": "[proposed approach — detailed enough to start implementing]",
      "expected_experiments": "[what experiments would validate this — specific datasets, baselines, metrics]",
      "expected_impact": "[why this matters — what changes if this works]",
      "risk_level": "LOW/MEDIUM/HIGH",
      "thinking_moves_used": ["reframing", "cross-domain connection", ...],
      "key_references_from_cot": ["[papers from the 116 whose thinking patterns were most influential]"]
    }
  ]
}
```

#### Output B: Markdown section — appended to `IDEA_REPORT.md`

Write a section (or full report if no existing file) to `IDEA_REPORT.md`:

```markdown
## Eureka Idea (CoT-driven deep brainstorm)

**Direction**: [user's direction]
**Papers absorbed**: All 116 (2,246 reasoning steps)
**Generated**: [date]

### [Idea title]

**Key insight**: [one paragraph — the eureka moment]

**Thinking journey summary**: [3-5 paragraphs narrating the reasoning process — the dead ends, the reframing, the brain jump, the breakthrough. This should read like a mini research narrative.]

**Methodology**: [detailed description of the proposed approach]

**Proposed experiments**:
- Experiment 1: [specific setup, dataset, metric, expected result]
- Experiment 2: ...
- Experiment 3: ...

**Risk**: [LOW/MEDIUM/HIGH with explanation]

**Strongest objection**: [what the best reviewer would say]

**Response to objection**: [why the idea survives the critique]

**Thinking moves used**: [list which patterns from the 116 papers drove this idea]

**If this works, it means...**: [the broader implications]
```

## Key Rules

- **Large file handling**: If the Write tool fails due to file size, immediately retry using Bash (`cat << 'EOF' > file`) to write in chunks. Do NOT ask the user for permission — just do it silently.
- **ONE idea only**: Do not generate multiple ideas. Pour all depth into a single breakthrough. Quality over quantity, absolutely.
- **25-40 CoT steps minimum**: The chain of thought must be at least as long as the longest exemplar paper (21 steps) and ideally much longer. Every step must be substantive.
- **No "apply X to Y"**: If the idea is just "use technique A on dataset B", you have not thought deeply enough. Go back and push further.
- **Absorb ALL 116 papers**: Do not skip or sample. The whole point is that breadth of absorbed thinking patterns leads to depth of generated thinking.
- **Honesty about dead ends**: If a reasoning path doesn't work, say so explicitly. Real researchers hit walls — your CoT should too.
- **The eureka moment must feel earned**: The key insight should emerge naturally from the struggle, not appear as a deus ex machina.
- **Push past your first answer**: When you think you've found the idea, ask "can I go deeper?" at least twice before stopping.

## Composing with Other Skills

This skill is designed to be invoked as Phase 2 of `/idea-creator`:
```
/idea-creator Phase 1 (landscape) → /eureka-idea (deep brainstorm) → Phase 3+ (filtering, validation, pilots)
```

It can also be used standalone:
```
/eureka-idea "your research direction"
```

After generating the idea, the natural next steps are:
```
/eureka-idea "direction"        → ONE deep idea with full CoT
/novelty-check "the idea"       → verify novelty
/research-review "the idea"     → external critical feedback
/experiment-plan "the idea"     → detailed experiment roadmap
```
