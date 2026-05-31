# Agent Capability Map

## Purpose

This document translates FreshSite Copilot from a vertical fresh-retail demo into reusable agent capability language.

The goal is to answer an interview question like:

> Beyond the fresh-retail scenario, what concrete agent-related capabilities did you build or learn?

## Capability 1: Task Understanding

### Reusable Skill

Convert a fuzzy user goal into structured constraints that downstream tools can execute.

### In FreshSite

User intent:

> Find locations that are more suitable for fresh-retail service expansion, especially where online service is weak and resident demand is strong.

Structured request:

```json
{
  "task_type": "candidate_ranking",
  "domain": "fresh_retail_siting",
  "objective": "service_gap",
  "priorities": ["online_gap", "residential_demand"],
  "constraints": {
    "area": "Mochou Lake Street",
    "top_k": 5
  }
}
```

### Transferable Framing

This is a constraint-normalization layer. It can be reused in any decision copilot where users express goals imprecisely but the system needs structured execution parameters.

## Capability 2: Tool-Based Decision Workflow

### Reusable Skill

Break a decision process into explicit tools rather than hiding all logic inside one model or one scoring function.

### Generic Tools

- `retrieve_candidates`
- `extract_features`
- `score_candidates`
- `match_rules`
- `rerank_for_diversity`
- `validate_results`
- `generate_explanations`

### In FreshSite

The current fresh-retail workflow maps to these tools:

- Candidate POIs become `retrieve_candidates`.
- Neighborhood, traffic, and service-gap metrics become `extract_features`.
- Goal-weighted ranking becomes `score_candidates`.
- Planning and service rules become `match_rules`.
- Anti-clustering logic becomes `rerank_for_diversity`.
- Boundary and concentration checks become `validate_results`.
- Recommendation text becomes `generate_explanations`.

### Transferable Framing

The important capability is not the exact fresh-retail score. It is the ability to express a decision as a transparent, testable tool chain.

## Capability 3: Evaluator Checks

### Reusable Skill

Add a result-review layer that checks whether recommendations are usable before presenting them.

### Checks In This Project

- Are candidate points inside the target area?
- Are Top K results too concentrated around one neighborhood?
- Are coordinates valid?
- Did the result respect the user's stated objective?
- Is there enough evidence to explain the recommendation?

### Why It Matters

This is where the project becomes more agentic without becoming unstable. The system does not only produce an answer; it also checks whether the answer violates important constraints.

### Transferable Framing

Evaluator checks can be reused in hiring recommendation, supplier ranking, location screening, document retrieval, or any workflow where top-ranked results need guardrails.

## Capability 4: Evidence-Grounded Explanation

### Reusable Skill

Generate explanations from structured evidence instead of letting an LLM invent reasons.

### Evidence Pattern

```json
{
  "candidate": "Candidate A",
  "score_parts": {
    "demand": 18.2,
    "traffic": 13.5,
    "service_gap": 20.0
  },
  "rule_hits": ["weak online service", "high residential centrality"],
  "explanation": "This point is worth field review because nearby demand is strong, online service is weak, and it matches the residential centrality rule."
}
```

### Transferable Framing

The agent's explanation is evidence-bound. This is more defensible than free-form model output and more useful than a raw score.

## Capability 5: Domain Adapter Design

### Reusable Skill

Separate reusable agent workflow from domain-specific data, features, and rules.

### Three-Layer Split

```text
Agent Interface
  Task normalization, trace, explanation

Decision Engine
  Tool execution, scoring, ranking, evaluator

Domain Adapter
  Fresh-retail POIs, neighborhood features, online service links, GIS layers
```

### Why It Matters

Without this split, the project is only a fresh-retail tool. With this split, fresh retail becomes a first scenario for validating a more general decision-copilot pattern.

## Capability 6: Traceable Decision UX

### Reusable Skill

Show users how the system reached a recommendation without overwhelming them with implementation details.

### In FreshSite

The visible trace can show:

- Goal parsed
- Candidate pool retrieved
- Spatial and service features scored
- Rules matched
- Results reranked
- Explanation generated
- Evaluation passed

### Transferable Framing

Trace is not just UI decoration. It is a trust layer for decision workflows.

## Interview Summary

The reusable agent capabilities are:

- Task understanding from user goals to structured constraints
- Tool-based decision execution
- Result evaluation and guardrail checks
- Evidence-grounded explanation
- Domain adapter architecture
- Traceable decision UX

One-sentence version:

> I used fresh-retail siting as a concrete domain to practice a reusable agentic decision copilot pattern: parse goals, call decision tools, evaluate results, explain recommendations with evidence, and isolate domain-specific data behind an adapter.
