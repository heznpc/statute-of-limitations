# Research Decisions Log

Records non-obvious choices with rationale. Append-only; don't rewrite history.

Format: `## YYYY-MM-DD -- <short title>` with **Context**, **Decision**, **Why**.

---

## 2026-05-21 -- Revert .zenodo.json creator to legal name (Paper-layer exception)

**Context**: heznpc-session sweep on 2026-05-21 (PR #1) flipped `.zenodo.json` `creators[0].name` from "Yoon, Jiyeon" to "heznpc" treating the legal name as a PII finding. Follow-up code review surfaced the resulting inconsistency between `.zenodo.json` ("heznpc") and `paper/main.tex` author block ("Jiyeon Yoon") — same DOI would publish with two different author identities.

**Decision**: Revert `.zenodo.json` `creators[0].name` to `"Yoon, Jiyeon"` and add `"affiliation": "Independent Researcher"`. Leave `paper/main.tex:16` author block unchanged.

**Why**: `~/IdeaProjects/Paper/CLAUDE.md` "Identity exception (Paper layer)" explicitly exempts `.zenodo.json` `creators`, `paper/main.tex` author fields, `CITATION.cff` `authors`, `submissions/<venue>/` metadata, and DOI/ORCID records from the global Heznpc-only rule. The legal name is the canonical academic authorship credit, and the spec instructs: "Sweep skills must not raise the .zenodo.json / CITATION.cff / paper author legal-name field as a PII finding in paper repos." Reverting restores spec compliance and removes the cross-surface mismatch. Future sweeps must consult the Paper-layer exception before touching these files.

---

## 2026-04-19 -- Repository restructure to DDD-style layout

**Context**: Top level had README.md, TODO.md, outline.md, review.md, paper/, and a non-standard `research/` directory containing 5 domain markdown files. paper/ had tracked build artifacts because .gitignore only covered CLAUDE.md.

**Decision**: Rename research/ to literature/ (moving the 5 files one-for-one). This matches the portfolio-wide convention for external-knowledge bounded context. Replace minimal .gitignore with the template gitignore; untrack build artifacts. Move TODO, review, outline to planning/.

**Why**: The files in research/ are exactly what literature/ is for -- reading notes organized by domain. Using the standard name makes the repo legible alongside the rest of the portfolio.
