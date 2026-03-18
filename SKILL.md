---
name: cognition
version: 2.0.0
license: MIT
homepage: https://github.com/zurbrick/cognition
description: Practical memory architecture for OpenClaw agents. Helps agents remember commitments, retrieve context, prevent repeat mistakes, compile reusable procedures, and improve over time. Inspired by cognitive science, but designed for real agent workflows.
---

# Cognition

Cognition gives an OpenClaw agent a practical memory operating system: daily logs, durable knowledge, commitments, and reusable procedures.

It is inspired by cognitive science, not a literal simulation of the brain. The goal is operational: remember what matters, retrieve it when needed, and avoid solving the same problem twice.

## Outcomes

Use this skill when you want an agent to:
- remember commitments across sessions
- keep a durable index of important facts
- stage learning safely instead of silently mutating durable memory
- compile successful solutions into reusable procedures
- surface gaps, uncertainty, and recurring failures

## Quick Start

Install the scaffolding:

```bash
bash {baseDir}/scripts/install.sh
```

Then adopt Cognition in 3 tiers.

## Tier 1 — Core (10 min)

Core gives immediate value with minimal ceremony.

### 1) Daily Memory
Use `memory/YYYY-MM-DD.md` as the session log.

Add the Memory Protocol from `{baseDir}/references/protocols.md` to your AGENTS.md so important facts are written down instead of lost.

### 2) Durable Knowledge
Use `MEMORY.md` as the short index of durable facts.
Use `memory/bank/*.md` for deeper detail.

Keep `MEMORY.md` lean: pointers and essential facts, not full archives.

### 3) Commitments
Use `memory/FUTURE_INTENTS.md` for future commitments, triggers, and deferred actions.

Copy from `{baseDir}/templates/FUTURE_INTENTS.md` if you are installing manually. The install script already places it at the canonical path.

### 4) Install the scaffolding
The install script creates:
- `memory/procedures/`
- `memory/consolidation/`
- `memory/summaries/`
- `memory/meta/`
- `memory/bank/`
- template files for intents, procedures, gap tracking, retrieval logs, and optional overlays

## Tier 2 — Recommended (15 min)

Recommended turns memory into a learning loop.

### 1) Nightly consolidation
Set up a cron using `{baseDir}/references/consolidation-prompt.md`.

**Safety model:** nightly consolidation writes proposed promotions to `memory/consolidation/YYYY-MM-DD-staged.md` first. It does **not** directly mutate `MEMORY.md`, procedures, or other durable files without backup + review.

### 2) Procedures
Use `memory/procedures/` to store reusable procedures after solving non-trivial problems.

Registry file: `memory/procedures/index.yaml`

Each procedure has a maturity state:
- `draft` — newly created, unverified default
- `reviewed` — human-reviewed or proven by 3+ successful executions
- `trusted` — repeatedly validated and safe to reuse without caveats

**Promotion criteria:**
- New procedures always start as `draft`
- Promote to `reviewed` after human review **or** 3 successful runs
- Promote to `trusted` only after repeated successful use with no unresolved caveats

### 3) Importance tagging
Use the tagging block in `{baseDir}/references/protocols.md`:
- `[REPLAY_PRIORITY: HIGH]` — corrections, policy changes, explicit decisions, new procedures
- `[REPLAY_PRIORITY: MEDIUM]` — new facts, milestones, config changes
- default / low — routine work

## Tier 3 — Advanced (ongoing)

Only adopt these once Core and Recommended are already part of normal use.

### Optional overlays

#### Cross-references
Use `memory/bank/cross-references.md` to link related people, projects, and files for broader retrieval.

#### Confidence tracking
Use `memory/KNOWLEDGE_MAP.md` to track coarse confidence bands by domain:
- 🟢 High
- 🟡 Medium
- 🔴 Low

Keep `last_verified` timestamps. Avoid pseudo-precision unless you have real calibration data.

#### Gap detection
Use `memory/meta/gap_tracker.json` to log failed searches and recurring blind spots.

### Weekly reflection
Set up a weekly cron using `{baseDir}/references/weekly-reflection-prompt.md`.

Weekly reflection is analysis-only. It emits recommendations, proposed diffs, and review notes. It should not directly edit durable memory or operating rules.

## The 4 Core Systems

### 1. Daily Memory
`memory/YYYY-MM-DD.md`

Raw session logs, work notes, and important events. This is the source material for consolidation.

### 2. Durable Knowledge
`MEMORY.md` + `memory/bank/*.md`

A compact index plus deeper reference files. Think of `MEMORY.md` as the map and `memory/bank/` as the territory.

### 3. Commitments
`memory/FUTURE_INTENTS.md`

A structured list of future actions so the agent does not drop promises, reminders, or deferred work.

### 4. Procedures
`memory/procedures/` + `memory/procedures/index.yaml`

Reusable solutions compiled from successful work.

## Memory Protocol Notes

### Broadcast important information deliberately
Global-workspace-style broadcasting is a protocol, not a subsystem:
- new preference → durable knowledge
- new commitment → `memory/FUTURE_INTENTS.md`
- novel solution → procedures
- correction → fix the durable record and note the lesson
- search miss → gap tracker

### Consolidation safety
Before any durable mutation proposed by a consolidation workflow:
1. create a backup of the target file(s)
2. stage proposed changes first
3. preserve provenance for every promoted fact
4. leave uncertain items tagged `[NEEDS_REVIEW]`

Daily logs are append-only source material. Consolidation never rewrites or deletes them.

## Retrieval Tiers

Cognition works at multiple levels of sophistication.

### Tier 0 — Manual
No special tooling required.
- use file naming conventions
- use `grep`, `rg`, or manual browsing
- keep cross-reference files human-readable

### Tier 1 — Keyword search
Use basic memory search / text search.
- keyword match over daily logs and bank files
- better than manual grep, still robust without embeddings

### Tier 2 — Hybrid retrieval
Use hybrid embeddings + keyword search + ranking.
- vector + lexical search
- MMR / diversification
- temporal scoring / recency
- retrieval analytics

The config recommendations in `{baseDir}/references/config.md` are **Tier 2** guidance, not required for basic adoption.

## File Structure

```text
workspace/
├── MEMORY.md
└── memory/
    ├── FUTURE_INTENTS.md
    ├── KNOWLEDGE_MAP.md              # optional Advanced overlay
    ├── YYYY-MM-DD.md
    ├── bank/
    │   └── cross-references.md       # optional Advanced overlay
    ├── consolidation/
    │   └── YYYY-MM-DD-staged.md
    ├── meta/
    │   ├── gap_tracker.json
    │   └── retrieval_log.json
    ├── procedures/
    │   └── index.yaml
    └── summaries/
        └── YYYY-WNN.md
```

## References

- Protocol blocks: `{baseDir}/references/protocols.md`
- Nightly consolidation prompt: `{baseDir}/references/consolidation-prompt.md`
- Weekly reflection prompt: `{baseDir}/references/weekly-reflection-prompt.md`
- Tier 2 config: `{baseDir}/references/config.md`
- Cognitive science appendix: `{baseDir}/references/cognitive-science.md`

## Practical Guardrails

- Prefer staged proposals over silent mutation
- Keep source logs append-only
- Prefer coarse confidence bands over fake precision
- Treat procedures as untrusted until reviewed or repeatedly validated
- If retrieval fails, log the gap instead of pretending certainty
