# EurikAI ⚡🧠

By [Harry Yang](https://hyang.org)

> **Think like the greatest researchers.** Generate breakthrough research ideas by absorbing the full chain-of-thought reasoning of 116 landmark papers — then pushing further than any of them.

## What is EurikAI?

EurikAI makes AI think like top researchers instead of generating shallow "apply X to Y" ideas. It feeds Claude the **complete reasoning traces** of 116 landmark papers — every dead end, every failed approach, every reframing, every brain jump, every eureka moment — and then asks it to **generate a new idea with the same depth**.

The output is a single, deeply reasoned research idea with a **25-40 step chain of thought** that shows genuine intellectual struggle, not a clean one-liner.

## What's inside `top_papers_cot.json`

| | |
|---|---|
| **Papers** | 116 — AI (100), Physics (8), Mathematics (8) |
| **Total reasoning steps** | 2,246 (avg 19.4 per paper, each 15-25 steps) |
| **Span** | Alan Turing (1950) to modern frontier models |
| **Per paper** | `persona`, `problem_statement`, `prior_work_and_limitations`, `observations`, `chain_of_thought` (step-by-step first-person reasoning), `key_insight`, `methodology`, `impact` |

Every chain of thought is written in first person, capturing:
- **Dead ends** — "I tried X but it failed because..."
- **Reframings** — "Wait — what if the whole framing is wrong?"
- **Brain jumps** — unexpected cross-domain connections
- **Eureka moments** — "Suddenly it hit me..."
- **The emotional journey** — frustration, doubt, excitement

Example papers: Turing's imitation game, Rosenblatt's perceptron, Hinton's backpropagation, Vaswani's attention mechanism, Ho's diffusion models, Galois's group theory, Einstein's special relativity, Shannon's information theory, and 108 more.

## How it works

```
You (research direction)
  → Claude reads ALL 116 chains of thought (2,246 reasoning steps)
  → Absorbs every thinking pattern: reframing, inversion, cross-domain transfer,
    simplification, scaling past phase transitions, challenging sacred assumptions
  → Thinks 25-40 steps deep (longer than any exemplar paper)
  → Produces ONE breakthrough idea with a full reasoning trace
    showing genuine dead ends, reframings, and an earned eureka moment
  → Outputs eureka_ideas.json (same schema) + IDEA_REPORT.md
```

## Usage

### Option 1: As a Claude Code skill

```bash
# Install
git clone https://github.com/harryyang/eureka.git
cp -r eureka/skills/eureka-idea ~/.claude/skills/

# Run
claude
> /eureka-idea "factorized gap in discrete diffusion LMs"
```

### Option 2: As a standalone prompt (no installation needed)

Attach `top_papers_cot.json` to any Claude conversation (claude.ai, API, or any LLM with large context) and paste:

```
Given the attached top_papers_cot.json, follow the thinking process of the really
top papers and researchers. Think very deep and hard in the area of [YOUR RESEARCH
DIRECTION]. Push really far. Learn from the thinking process (and brain jumps) of
the famous papers and researchers, the eureka moments of them.

Study ALL 116 papers' chain-of-thought traces. Absorb the dead ends, the reframings,
the cross-domain connections, the eureka moments. Then generate ONE new idea with a
25-40 step chain of thought that shows genuine intellectual struggle — dead ends,
failed approaches, reframings, and an earned eureka moment.

Output a new JSON entry in the same schema as top_papers_cot.json.
```

### Option 3: Inside the idea discovery pipeline

EurikAI integrates as Phase 2 of the [`/idea-creator`](skills/idea-creator/SKILL.md) skill, replacing generic brainstorming with eureka-style deep thinking:

```bash
> /idea-creator "your research direction"
# Phase 1: literature survey → Phase 2: /eureka-idea → Phase 3+: filtering, validation, pilots
```

## Output

Two files are generated:

**`eureka_ideas.json`** — machine-readable, same schema as `top_papers_cot.json`:

```json
{
  "ideas": [
    {
      "title": "proposed paper title",
      "problem_statement": "what problem this solves",
      "chain_of_thought": [
        {"step": 1, "thought": "What's unsatisfying about current approaches..."},
        {"step": 2, "thought": "I tried the obvious approach but..."},
        ...
        {"step": 30, "thought": "The eureka moment..."}
      ],
      "key_insight": "the core breakthrough, one paragraph",
      "methodology": "proposed approach, detailed enough to implement",
      "expected_experiments": "specific datasets, baselines, metrics",
      "thinking_moves_used": ["reframing", "cross-domain connection", ...]
    }
  ]
}
```

**`IDEA_REPORT.md`** — readable narrative with thinking journey, proposed experiments, strongest objections, and broader implications.

## Why this works

| Traditional brainstorming | EurikAI |
|--------------------------|---------|
| "Generate 10 ideas about X" | Absorb 2,246 reasoning steps, then think 25-40 steps deep |
| Produces "apply X to Y" ideas | Produces ideas with genuine reframings and eureka moments |
| Breadth over depth | All depth poured into ONE breakthrough |
| Clean outputs hide the thinking | Dead ends and failed approaches are features, not bugs |
| No model of how breakthroughs happen | Learned from 116 real breakthroughs across 76 years |

## The thinking moves

EurikAI learns these recurring patterns from the 116 papers:

- **Reframing** — Turing didn't solve "can machines think?" — he replaced the question entirely
- **Inversion** — GANs didn't learn to generate directly — they learned by training a critic
- **Simplification** — Rosenblatt didn't need meaningful first-layer connections — random projections sufficed
- **Cross-domain transfer** — Boltzmann machines borrowed from statistical mechanics
- **Scaling past phase transitions** — GPT-3 showed that quantity produces qualitative change
- **Challenging sacred assumptions** — BatchNorm questioned whether we need careful initialization
- **Unifying separate problems** — Transformers showed attention is all you need
- **Finding hidden structure** — Galois found the group structure that explains why quintics are unsolvable

## Example outputs

Ideas generated by EurikAI (Claude Opus 4.6 + `top_papers_cot.json`):

| Idea | CoT steps | Paper (AI-generated) | Key insight |
|------|:---------:|:--------------------:|-------------|
| [Counterfactual Attention](examples/idea_counterfactual_attention.json) | 25 | [PDF](examples/counterfactual_attention_neurips2026.pdf) | VLA generalization failure is an attention problem: only ~5% of visual features are causally relevant. A world model discovers causal features via counterfactual masking, then supervises VLA attention via KL divergence — provably tighter generalization bound at zero extra test-time cost. |
| [Temporal Tokens](examples/idea_temporal_tokens.json) | 38 | [PDF](examples/tempo_cvpr2026.pdf) | Video generation pathologies all stem from one flaw: pixel objectives entangle temporal dynamics with spatial appearance. Factor video into abstract temporal tokens (what happens) + conditional appearance rendering (what it looks like) — a ~1000x compressed space where physics is the primary signal. |
| [Failure is the Teacher](examples/idea_hindsight_diagnosis.json) | 37 | — | Diagnosed failures carry MORE learning signal than demonstrations. A differentiable world model diagnoses every robot failure (what went wrong, why, minimal correction via gradients), producing (failed, corrected) action pairs for DPO — an AlphaGo-Zero-style self-improvement loop from pure failure data. |
| [Object-Centric World Models](examples/idea_object_centric_wm.json) | 24 | — | The world is composed of objects, but world models process pixels — making combinatorial generalization impossible. Factoring into per-object dynamics turns exponential data requirements (O x P x T x C) into linear (O + P + T + C). |
| [Test-Time Physical Thought](examples/idea_robot_reasoning.json) | 11 | — | The o1 revolution hasn't happened for robots. Gradient-based reasoning through a differentiable world model gives exponential test-time scaling (vs polynomial for sampling), where each gradient step is a "physical thought" that diagnoses and corrects an action. |

## Citation

If you use EurikAI in your research, please cite:

```bibtex
@misc{yang2026eurikai,
    author       = {Yang, Harry},
    title        = {EurikAI: Research Idea Generation via Chain-of-Thought Emulation of Landmark Papers},
    year         = {2026},
    url          = {https://github.com/leehomyc/EurekAI},
}
```

## Acknowledgements

EurikAI builds on the skill infrastructure of [ARIS (Auto-claude-code-research-in-sleep)](https://github.com/wanshuiyin/Auto-claude-code-research-in-sleep) — an autonomous ML research workflow system by Ruofeng Yang, Yongcan Li, and Shuai Li.

## License

MIT
