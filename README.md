# Cognition

**Practical memory architecture for OpenClaw agents.**

Cognition helps an agent remember what matters across sessions without turning memory into ceremony.

It gives you a staged adoption path for:
- daily logs
- durable knowledge
- commitments
- reusable procedures
- safe consolidation
- optional retrieval overlays

## Start here

```bash
bash scripts/install.sh
```

Then adopt Cognition in 3 tiers.

## Tier 1 — Core

Use this first. It is the smallest useful subset.

- `memory/YYYY-MM-DD.md` for daily session logs
- `MEMORY.md` for durable facts
- `memory/bank/*.md` for deeper detail
- `memory/FUTURE_INTENTS.md` for commitments
- protocol blocks from `references/protocols.md`

## Tier 2 — Recommended

Add the learning loop once Core is normal behavior.

- nightly staged consolidation
- reusable procedures
- procedure registry
- importance tagging
- safe promotion rules (`draft → reviewed → trusted`)

## Tier 3 — Advanced

Optional overlays only after Core + Recommended are already working.

- cross-references
- confidence tracking
- gap tracking
- retrieval logging
- weekly reflection
- hybrid retrieval tuning

## Key design principle

**Memory should be operational, not decorative.**

Cognition keeps raw logs append-only, stages durable-memory updates before mutation, and treats optional overlays as optional.

## Repository contents

- `SKILL.md` — lean runtime entrypoint
- `references/architecture.md` — core systems, overlays, retrieval tiers, file structure
- `references/protocols.md` — protocol blocks to merge into AGENTS.md
- `references/consolidation-prompt.md` — nightly staged consolidation prompt
- `references/weekly-reflection-prompt.md` — weekly reflection prompt
- `references/config.md` — advanced hybrid retrieval tuning
- `references/cognitive-science.md` — theory appendix
- `scripts/install.sh` — scaffold installer
- `templates/` — starter files for intents, procedures, gap tracker, retrieval log, and overlays

## Guardrails

- stage proposals before durable-memory mutation
- keep raw logs append-only
- keep `MEMORY.md` compact
- treat procedure promotion as earned
- log retrieval gaps instead of inventing certainty

## License

MIT © Don Zurbrick
