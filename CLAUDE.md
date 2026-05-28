# Translation Project

## Overview
Translates historical books into English using sequential subagent batches. Each work lives under `<author>/<work>/` with `source/` (PDF + work-specific CLAUDE.md) and `translation/` (batch outputs and collated files).

## Directory Convention
```
translations/
├── CLAUDE.md                          ← orchestration rules (this file)
├── .claude/agents/
│   ├── latin-translator.md            ← Latin translation rules + batch-report format
│   └── hebrew-translator.md           ← Hebrew/Aramaic translation rules + batch-report format
│
└── <author>/<work>/
    ├── source/
    │   ├── CLAUDE.md                  ← work-specific deltas only
    │   ├── <source_file>.pdf
    │   └── batch_NN.pdf               ← auto-generated during splitting
    └── translation/
        ├── batch_NN.md                ← per-batch outputs
        ├── rerun_candidates.txt       ← anomalies logged in-flight
        ├── reconciliation_report.md   ← Stage-2 categorized report
        ├── <work>_complete.md
        ├── <work>_complete.docx
        └── <work>_discrepancies.md
```

The agent files are the source of truth for translation rules (numeral handling, marginalia, diagrams, tables, batch-report format). Per-work `source/CLAUDE.md` files contain deltas only and should not restate them.

## Canonical examples per language
New works are scaffolded by copying the canonical example for their language and editing the deltas. Each canonical example is a ~30–40 line file covering all required sections without duplicating generic rules.

| Language | Canonical example |
|---|---|
| Latin | `longomontanus/astronomia_danica/source/CLAUDE.md` |
| Hebrew (and Hebrew/Aramaic) | `gans/tzemach_david/source/CLAUDE.md` |

When adding a new language, designate its canonical example here.

## Adding a New Work

### Quick path: `Add <url>`
From the project root in a Claude Code session, type `Add <url>` where `<url>` is the book's catalog page (Internet Archive, HebrewBooks.org, Gallica IIIF, etc.). Claude will:

1. Fetch the page and extract bibliographic metadata.
2. Identify the language and pick the matching canonical example. If the language has no canonical example, ask first.
3. Propose an `<author>/<work>/` directory name and confirm before writing.
4. Create `<author>/<work>/source/` and `<author>/<work>/translation/`.
5. Write `source/CLAUDE.md` by copying the canonical example and editing the deltas (Book Metadata, Context, Subagent, Subagent Task Prompt, Known Challenges).
6. For IIIF manuscripts or multi-volume sources, add an `## Image Download` section modeled on `gersonides/sefer_hatechunah/source/CLAUDE.md` and stop before downloading.
7. Otherwise print the source URL and target path, then instruct the user to drop the PDF in `<author>/<work>/source/` before running `Translate <author>/<work>`.

Confirmation prompts only for choices Claude can't decide on its own (directory name, ambiguous language, missing metadata).

### Manual path
If the URL flow doesn't fit:

1. Create `<author>/<work>/source/` and place the source PDF.
2. Create `source/CLAUDE.md` by copying the canonical example for the language. Required sections:
   - **Book Metadata**: title, author, edition, source, pages, structure, language.
   - **Context**: why this book matters, connections to other works.
   - **Subagent**: which translator subagent to use.
   - **Subagent Task Prompt**: work-specific orientation only — what differs from the agent's standing rules.
   - **Known Challenges**: scan quality, genre-specific difficulties, cross-references.
3. For IIIF or download-required sources, add an `## Image Download` section. See `gersonides/sefer_hatechunah/source/CLAUDE.md`.
4. Run `Translate <author>/<work>`.

## Orchestration

```
Translate <author>/<work>
Resume <author>/<work> from batch NN
```

The orchestrator reads `<author>/<work>/source/CLAUDE.md`, loads the named subagent from `.claude/agents/`, combines its standing rules with the work-specific orientation, splits the source PDF, and processes batches sequentially. For resumption, it confirms the last completed batch from `batch_NN.md` files on disk before proceeding.

## Execution Rules

### Sequential processing only
Process batches one at a time, in order. Do not parallelize or spawn multiple translation subagents simultaneously.

### Pacing
- After each batch completes and its report is logged, **wait 5 minutes** before spawning the next subagent. Use `Bash` with `run_in_background: true` (e.g., `sleep 300`) since long leading sleeps are blocked by the harness.
- **Load-bearing rationale:** the user's Claude session has an external rolling-window rate limit (~5 hours) not visible from inside the orchestrator. Without pacing, ~40 sequential subagent calls exhaust the allotment mid-work. 5-minute spacing keeps a ~40-batch run inside one window. Do not shorten this just because the orchestrator "feels fine" — the constraint is on the user's account, not this conversation.
- If the user specifies a different pace in the prompt ("3 minute delay", "no delay", "no pause for reconciliation reruns"), follow that.
- Do not stop preemptively to "save the token window" — the orchestrator's context auto-compacts as needed; that is separate from the session rate limit. Run until done, the user pauses you, or the harness stops you. If interrupted, `batch_NN.md` files mark progress and the user resumes with `Resume <author>/<work> from batch NN+1`.

### Per-batch logging and recap
After every batch, the orchestrator must print a brief one-line recap of what the batch covered (e.g., "Batch N done — chapter/topic summary"). If an anomaly is logged, print it as a separate `⚠️ ...` line *in addition to* the recap, not instead of it. Then proceed immediately to the next batch (after the pacing delay). Do not wait for human confirmation.

The agent definitions enforce the batch-report format (running headers, body headings, content, diagrams, numerical impossibles, uncertain readings, readability, numbering anomalies). Running headers and body headings are structurally required. When they disagree, trust body headings and note the conflict.

### Sequence integrity
After each batch, check whether section/paragraph/chapter numbers continue from the previous batch. On gap, duplication, or misnumbering, log a warning and append to `<author>/<work>/translation/rerun_candidates.txt` with a brief description. Do not stop — the rerun list is reviewed before collation.

### Error handling
On subagent failure, empty/garbled result, or >20% unreadable page, log it, append to `rerun_candidates.txt`, and continue.

### Resumption
The user specifies which work and batch number to resume from. Confirm the last completed batch by checking on-disk `batch_NN.md` files before proceeding.

### Progress tracking — do NOT use TaskCreate for the per-batch loop
The on-disk `batch_NN.md` files are the authoritative, durable progress tracker for the per-batch loop. They survive context compaction and session boundaries; an in-conversation task list does not, and ~200+ uniform todos are noise rather than signal. If the harness emits a generic system reminder about task tools, ignore it for this workflow.

TaskCreate *is* appropriate for non-uniform follow-ups around a run (Stages 2–5 reconciliation/rerun/collation when there are several distinct items, or ad-hoc multi-step debugging) — not for the batch loop itself.

## Batch Preparation

Split the source PDF into 4-page batches named `batch_01.pdf`, `batch_02.pdf`, … placed in `source/` alongside the original. The final batch may be shorter.

Source PDFs are typically scanned page images, not searchable text — the subagent reads directly from the images. Preserve original image resolution; do not downsample or recompress. Output must be PDF with embedded images, not extracted text. Verify after splitting that batches look identical to the original pages at full zoom.

Use `qpdf` for lossless splitting. Fall back in order: `pdftk`, Python `pikepdf`, `PyPDF2`. Log which tool was used.

## Stitching

### Stage 1 — In-flight logging
Anomalies are logged to `rerun_candidates.txt` as found during batch processing. No triage — capture everything.

### Stage 2 — Categorized reconciliation report
After all batches complete, sort every flagged issue into one of four categories and write `<author>/<work>/translation/reconciliation_report.md`:

- **A — Rerun likely helps**: probable subagent misread (numeral, header, boundary). A fresh pass should resolve it.
- **B — Textual feature, footnote**: anomaly in the printed source itself (compositor doubling, authorial error, errata). Resolve with an editor's note.
- **C — Author/source anomaly, footnote**: unexpected content but appears to be what the author wrote. Resolve with an editor's note.
- **D — Cross-reference, fix at collation**: boundary alignment, overlap with adjacent batches, formatting issues resolvable during stitching.

Present the report and WAIT for the human to choose which Category A batches to rerun.

### Stage 3 — Human selects rerun set
The user reviews the report and specifies which batches to rerun.

### Stage 4 — Reruns execute
**Reruns must VERIFY, not APPLY.** A rerun prompt treats the hypothesis as something to test against the printed source, not as instructions to apply. If the source contradicts the hypothesis, the rerun must report the contradiction. Frame each rerun as: "Check whether [hypothesis] — report what the source actually shows."

Reruns may surface new findings or refute earlier ones — expected and correct. Present any new findings for human review before proceeding.

**Multi-pass diagrams:** volvelles, dial-faces, armillary spheres, astrolabes, and similar figures with many small peripheral labels often need more than one verification pass. If a single rerun leaves >2 labels still flagged `[?]`, schedule another focused pass on just those positions. The editor cost of unresolved `[?]` flags in a diagram is much higher than the cost of one more rerun.

### Stage 4.5 — Update reconciliation report with verified outcomes
Before collation, edit `reconciliation_report.md` to reflect what the reruns actually found:

- **A confirmed by rerun** → reclassify to B (compositor error, editor's note) or D (resolved at collation).
- **A refuted by rerun** → update with the correct reading and note the original error.
- **New findings** → categorize and add.
- If a rerun materially changed batch content (resolved diagram labels, recovered an obscured marginal note), update the corresponding `batch_NN.md` so the collated output carries the corrected content.

Present the updated report for final human review before collation.

### Stage 5 — Collation and discrepancy report

**Collation.** Concatenate `batch_NN.md` files in order. Add a title page (book, author, source, translation date), a table of contents from section/chapter markers, and source-page brackets for every diagram, table, illustration, and figure (e.g., `[Source: p. 23]`, `[Source: pp. 45–46]`). Verify section/chapter sequence is continuous; flag remaining gaps. Write `<work>_complete.md`.

Convert to .docx with **pandoc** (preferred): `pandoc <work>_complete.md --from gfm+pipe_tables+raw_html --to docx --standalone --toc --toc-depth=4 -o <work>_complete.docx`. Pandoc produces native Word tables with correct column widths — important for astronomical tables with empty cells and paired sub-columns that the LibreOffice path collapses. Pandoc 3.9+ is installed at `~/.local/bin/pandoc`. Headings map automatically (`#` → Heading 1, etc.) and `--toc` generates a clickable Word-native TOC.

Fallback: if pandoc is unavailable, the legacy Python-markdown → HTML → LibreOffice pipeline (`--convert-to 'docx:"MS Word 2007 XML"'`) still works but produces inferior tables. `md_to_docx.py` in the longomontanus directory auto-detects pandoc. Log which toolchain was used.

**Discrepancy report.** Write `<work>_discrepancies.md` (and convert to .docx) consolidating all unresolved issues for editorial follow-up:

- Remaining numbering anomalies (gaps, overlaps, swapped headings) with batch and page references.
- Passages with high concentrations of `[?]` readings, with references.
- Pages flagged as significantly degraded or partially unreadable.
- Compositor errors or garbled names that could not be identified.
- Tables with parsing difficulties or unreadable cells.
- Structural anomalies (missing sections, pagination discontinuities, authorship transitions).

Each entry should include enough context (batch number, source page, surrounding text) for a human editor to locate and resolve manually.

## Output Tiers

**Manuscript-grade** (what this workflow produces): structurally accurate, boundary corrections applied, uncertain readings flagged as `[?]`, discrepancy report and rerun audit trail preserved, ready for a scholarly editorial pass.

**Publication-grade** (beyond this workflow): bibliographic specialist clearing `[?]` flags, footnote apparatus for catalogued anomalies, better scans for degraded pages, typesetter pass for proper font handling, cross-referencing between works in the corpus.

## Model Preference
Use Opus for translation subagents. OCR accuracy and handling of ambiguous letterforms, technical terminology, and archaic scripts justify the cost over Sonnet.
