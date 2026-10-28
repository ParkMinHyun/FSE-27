# Project Rules

This repository is a LaTeX paper project for the FSE 2027 Industry Papers track (long paper: 10 pages of text and figures plus 2 pages of references). It was originally prepared for SEIP 2027, which was not submitted.

## Shared Context

- Treat `AGENTS.md` as the single source of truth for shared working context, used by both Codex and Claude. `CLAUDE.md` imports it via `@AGENTS.md`, so edit `AGENTS.md` only.
- Keep instructions in repository-relative paths only. Do not add local absolute paths or machine-specific settings.
- When a durable project rule changes, update this file. Commit only when the user explicitly requests a commit; manuscript edits and shared-context updates do not authorize automatic commits.
- User-facing discussion can be in Korean, but manuscript text should be written in polished academic English unless explicitly requested otherwise.

## Repository Layout

- Main entry point: `paper.tex` (ACM `acmart` class, `sigconf` two-column format, `ACM-Reference-Format` bibliography style)
- ACM template files: `acmart.cls`, `ACM-Reference-Format.bst`
- Macros and reusable commands: `macros.tex`
- Bibliography: `refs.bib`
- Section files: `_*.tex`, `2_*.tex`, `3_*.tex`, `4_*.tex`, `discussion.tex`, and appendix files.
- Figures: `figures/`
- Reference papers: `references/`

## Build and Verification

- Use the existing `Makefile` first when checking the paper build.
- If the build fails because of local LaTeX tooling, report the exact missing tool or package instead of rewriting unrelated files.
- Do not commit or intentionally edit generated LaTeX artifacts such as `.aux`, `.log`, `.fls`, `.fdb_latexmk`, `.synctex.gz`, or rebuilt PDFs unless the user explicitly requests it.

## Collaboration Rules

- Before broad rewrites, inspect the relevant section files and preserve the author's intended argument.
- Before providing manuscript feedback or proposed revisions, self-review the surrounding text and section boundaries for causal continuity, repetition, terminology, and alignment with the author's intended argument. Present only the reviewed recommendation.
- Prefer small, reviewable edits over sweeping rewrites.
- For writing tasks, summarize what changed and name the edited files.
- For research-content tasks, distinguish clearly between facts found in the manuscript, in references, and in inference.

## Camera Workflow Context

- The configured draft-stage sequence remains unchanged during continuous capture. Mode, filter, and watermark settings that alter it can change only after all draft sequences in the draft queue have completed.
- Runtime admission may skip configured optional stages. Distinguish the configured stage sequence from the stages actually executed.
