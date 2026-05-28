# 시효 (Statute of Limitations)

```
Research Program: 1 (Human-Controlled AI Systems)
Status: Concept note
Relationship to other work: Bridges to Program 4 (AI-Mediated Accumulation); foundational to AirMCP memory governance
```

> This is a concept note, not a finished paper.

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

**시효: Designing Institutional Forgetting for AI Agent Memory Systems**

In legal systems, a statute of limitations does not delete evidence — it extinguishes the authority to act on it. The crime record, witness statements, and forensic data remain intact; only the state's power to prosecute expires. This 2,500-year-old institution represents humanity's most refined framework for "data exists but doesn't act" — a concept entirely absent from current AI memory design, where forgetting universally means deletion. The paper proposes a three-layer **Sihyo architecture** (permanent data store + expiry registry + access-mediation layer) as the bridge between agent-memory governance (Program 1) and the accumulation dynamics that AI-mediated systems produce over time (Program 4).

## Key Claim

Current AI memory systems conflate forgetting with deletion (TTL expiration, machine unlearning, GDPR erasure). The statute of limitations offers a structurally different model: **information persists, but its authority to influence decisions expires** — with severity-proportional durations, suspension conditions, and non-retroactivity. Cross-cultural variation in how societies designed institutional forgetting (Confucian perpetual memory, Islamic dual-rights hierarchy, Germanic codified decay) provides a taxonomy of design choices directly applicable to AI agent memory governance.

## Core Distinction

| Existing AI approaches | 시효 model |
|----------------------|------------|
| TTL expiry → data **deleted** | Expiry → data **exists**, action authority extinguished |
| Machine unlearning → **remove** from model | Record preserved, prosecution power expires |
| GDPR erasure → information **erased** | Information referenceable, but **not as decision basis** |
| Uniform decay (one rate fits all) | Severity-proportional expiration (misdemeanor 1yr, felony 25yr, murder never) |

## Research Questions

1. What design principles can AI agent memory systems extract from 2,500 years of institutional forgetting?
2. How do cross-cultural variations in statute of limitations design (abolition, de facto expiry, dual-rights hierarchies) map to different AI memory governance models?
3. Can the "exists but doesn't act" paradigm outperform deletion-based forgetting in agent memory systems?

## Repository layout

DDD-style. `paper/main.tex` is the single source of truth.

- `paper/main.tex` — manuscript (draft)
- `paper/figures/` — figure assets
- `literature/` — comparative legal-history and CS notes (`history.md`, `philosophy.md`, `cs_parallels.md`, `ai_memory_systems.md`, `market_value.md`)
- `experiments/` — DDD layout for the forthcoming Sihyo prototype: `src/` (runnable scripts), `data/raw/` + `data/processed/` (immutable inputs / regenerated outputs), `results/`, `archive/` (superseded pipelines)
- `planning/` — TODO, review, decisions log, superseded drafts

## Target venue

FAccT 2027 (primary) / CSCW 2027 / CHI 2027

## Status

- **Currently implemented**: LaTeX draft (`paper/main.tex`); five literature-synthesis notes under `literature/`; Zenodo deposition wired via GitHub release `v0.1.0` (2026-04-14) — see [Releases](https://github.com/heznpc/statute-of-limitations/releases) for the current DOI
- **Planned**: Sihyo prototype in `experiments/`; venue-specific adaptations under `submissions/<venue>/`
- **Design intent**: bridge AirMCP's HITL/audit layer (Program 1) to the longer-horizon accumulation questions raised by tidal/silo/caching (Program 4)
- **Non-goals**: not a deletion mechanism; not a GDPR-erasure proposal; not tied to any single jurisdiction's law
- **Redacted**: none
