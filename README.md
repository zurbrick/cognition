# Cognition

Practical memory architecture for OpenClaw agents.

Cognition helps an agent:
- keep daily logs
- maintain durable knowledge
- remember commitments
- compile reusable procedures
- stage memory changes safely before mutation

## Install

```bash
bash scripts/install.sh
```

## What it includes

- **4 core systems:** Daily Memory, Durable Knowledge, Commitments, Procedures
- **3 optional overlays:** Cross-references, Confidence tracking, Gap detection
- **Safe consolidation:** nightly staging with provenance and `[NEEDS_REVIEW]`
- **Weekly reflection:** analysis and proposed diffs, not silent edits

## Key files

- `SKILL.md` — usage guide
- `references/consolidation-prompt.md` — safe nightly consolidation prompt
- `references/weekly-reflection-prompt.md` — weekly analysis prompt
- `references/config.md` — advanced Tier 2 retrieval config
- `references/cognitive-science.md` — theory appendix

## License

MIT © Don Zurbrick
