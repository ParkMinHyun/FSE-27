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
- Explain manuscript edits in Korean, including the before/after meaning and the reason for the change.
- Prefer topic sentences that state a paragraph's purpose or main point before introducing symbols and procedural details.
- Prioritize accuracy, causal continuity, and readability over brevity. The author suspended unsolicited page-fitting and line-saving work on 2026-10-24; retain the FSE page limit as the submission target, but resume trimming only when requested.
- Preserve the compact, number-free conclusion paragraph without adding future-work sentences. Number displayed equations only when referenced by number, and avoid introducing semicolons.
- For research-content tasks, distinguish clearly between facts found in the manuscript, in references, and in inference.
- Verify claims about cited papers' assumptions or limitations against their original sources.

## Manuscript Continuity from SEIP

- The FSE project continues the same manuscript and prior decisions. Treat SEIP submission and IEEEtran formatting notes as historical context.
- Preserve the advisor-approved Section 2 flow: Capture Reliability (`2_1_release_process.tex`), Camera Usability with draft sequence and parallel capture (`2_2_camera_usability.tex`), Capture Timeout Risk with the motivating table (`2_3_capture_timeout_risk.tex`), and Goal (`2_4_research_goal.tex`).
- Causal reminders can serve different roles across sections. In particular, Section 2.1 defines timeout-clock start, while Section 2.3 uses that fact to explain why queue waiting consumes budget; do not remove the causal explanation solely as repetition.
- Keep the advisor-requested Control objective discussion in `3_1_overview.tex`. Its priority order is deadline safety, capture responsiveness, then optional-stage retention.
- Use the current manuscript for notation and implementation status. Older session suggestions, old page counts, and obsolete algorithm line numbers are historical evidence, not instructions to restore a previous draft.

## Evaluation Context

- Base Section 4's numerical prose on the printed tables in `tables/`. Investigate data-provenance discrepancies when an audit is requested, rather than changing table values from historical notes alone.
- Count watchdog-fallback captures as not executing the affected optional stage. Do not claim that Full always retains more optional work than Pacing only.
- Preserve the duration-statistic admission baselines; do not restore the withdrawn point-estimate-only ablation from old discussions.

## Local Session Archive

- The local SEIP context export is under `.codex-seip-context/2026-10-28/` when present. Consult its index and relevant conversation or memory files for detailed provenance; `AGENTS.md` remains the source of active shared rules.
- Claude's FSE memory snapshot is newer than the historical SEIP snapshot. Do not overwrite it with the older copy.
- The archive is ignored by Git and may contain private conversation history. Keep it local unless the author explicitly requests sharing or committing it.

## Camera Workflow Context

- The configured draft-stage sequence remains unchanged during continuous capture. Mode, filter, and watermark settings that alter it can change only after all draft sequences in the draft queue have completed.
- Runtime admission may skip configured optional stages. Distinguish the configured stage sequence from the stages actually executed.
- The timeout clock starts at request acceptance, so waiting in the draft queue consumes timeout budget. One draft worker executes sequences in capture order; accepted captures cannot be rejected, and running native stages cannot be preempted.
- Pacing delays delivery of `captureAvailable` and the next capture opportunity; current draft processing proceeds independently of that callback delay. Admission-disabled optional groups remain disabled until the draft queue drains.
