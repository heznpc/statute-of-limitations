# 시효

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

**시효: Designing Institutional Forgetting for AI Agent Memory Systems**

In legal systems, a statute of limitations does not delete evidence — it extinguishes the authority to act on it. The crime record, witness statements, and forensic data remain intact; only the state's power to prosecute expires. This 2,500-year-old institution represents humanity's most refined framework for "data exists but doesn't act" — a concept entirely absent from current AI memory design, where forgetting universally means deletion.

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

## Target Venue

- FAccT 2027 (primary) / CSCW 2027 / CHI 2027

## Structure

- `outline.md` — Paper outline
- `research/` — Background research
  - `history.md` — 2,500-year history of statute of limitations across civilizations

## Status

Framework paper. Literature synthesis complete, outline in progress.
