# Research Decisions Log

Records non-obvious choices with rationale. Append-only; don't rewrite history.

Format: `## YYYY-MM-DD -- <short title>` with **Context**, **Decision**, **Why**.

---

## 2026-04-19 -- Repository restructure to DDD-style layout

**Context**: Top level had README.md, TODO.md, outline.md, review.md, paper/, and a non-standard `research/` directory containing 5 domain markdown files. paper/ had tracked build artifacts because .gitignore only covered CLAUDE.md.

**Decision**: Rename research/ to literature/ (moving the 5 files one-for-one). This matches the portfolio-wide convention for external-knowledge bounded context. Replace minimal .gitignore with the template gitignore; untrack build artifacts. Move TODO, review, outline to planning/.

**Why**: The files in research/ are exactly what literature/ is for -- reading notes organized by domain. Using the standard name makes the repo legible alongside the rest of the portfolio.
