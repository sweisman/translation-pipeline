# translation-pipeline

An automated pipeline for translating historical books from Hebrew, Latin, and other languages into English using Claude Code and Claude's vision capabilities.

This repo is a **public-portfolio showcase** of an earlier version of a translation pipeline I built for my own research. My production pipeline is proprietary and considerably more refined; this is the first version that began producing manuscript-grade results, preserved here as a working demonstration of the approach. If you'd like to get in touch or support continued work, see [Contact & Support](#contact--support) at the bottom.

## The Problem

Some of the most important books in the history of science and philosophy have never been translated into English. They sit in library scans and digital archives — freely available, but locked behind historical languages, archaic typefaces, and specialist scripts that only a handful of scholars can read fluently in their original form. A 14th-century Hebrew astronomical treatise omitted from every printed edition for 700 years. A 17th-century Latin exposition of the Tychonic planetary system. An 18th-century Kabbalistic encyclopedia of science. These texts cite each other, respond to each other, and address the same cosmological questions across centuries — but no one has ever been able to read them side by side in the same language.

## What This Is

A Claude Code pipeline that takes scanned PDFs of historical books and produces manuscript-grade English translations, with structured batch reports, discrepancy tracking, and a reconciliation workflow. It handles Hebrew (printed and manuscript), Latin, and can be extended to other languages by adding new translator subagents.

The pipeline relies on Claude's native vision — no OCR preprocessing, no Tesseract, no fine-tuned models. Claude reads directly from page images and translates in one step. It handles:

- **Degraded historical type**: 18th-century Hebrew square script with ink erosion, bleed-through, and compositor errors; 17th-century Latin with woodcut initials and tight leading. Agent prompts include specific guidance for known confusion patterns (gershayim ״ / kaf כ, lamed ל / nun נ, tet ט / yod י) learned from actual runs.
- **Manuscript hands**: 14th-century Sephardic Hebrew manuscript at ~70–80% accuracy — useful working drafts of texts never translated in any form.
- **Rashi script**: the semi-cursive typeface used in Hebrew commentaries, harder than square script. Reduced but usable accuracy.
- **Precise tabular data**: astronomical tables with columns of degrees, minutes, and seconds reproduced cell by cell. Multi-page tables stitched at collation with source page ranges noted.
- **Complex diagrams**: concentric-sphere charts, geometric proofs, instrument schematics, volvelles with 20+ peripheral labels, cometary path diagrams — described in structured detail integrated with surrounding text.
- **Bilingual pages**: Latin and German on the same page (Brahe's correspondence), Hebrew with German on facing pages (*Yesod Olam*), censor stamps in Polish or Russian on Hebrew title pages.
- **Mathematical notation**: sexagesimal fractions, geometric relationships, calendar arithmetic with chalakim and regaim — preserved with exact values.

## The Corpus

The repo ships with source configurations for twelve works spanning seven centuries, two languages, and the full arc from Gersonides' medieval Jewish astronomy through Tycho Brahe's observatory to an 18th-century Kabbalistic synthesis. One (Longomontanus, *Astronomia Danica*) has been fully translated as a reference run; the others are configured and ready.

### Hebrew works
| Work | Author | Date | Source | Pages | Notes |
|---|---|---|---|---|---|
| Nechmad ve-Na'im | David Gans | 1743 (written ~1600) | [HebrewBooks 14299](https://hebrewbooks.org/14299), [20763](https://hebrewbooks.org/20763) | ~170 | Ptolemaic astronomy textbook by a visitor to Brahe's observatory |
| Tzemach David | David Gans | 1592 | [HebrewBooks 36906](https://hebrewbooks.org/36906) | ~230 | Historical chronicle, Jewish and world history |
| Sefer HaBrit HaShalem | Pinchas Eliyahu Hurwitz | 1797 | [HebrewBooks 43670](https://hebrewbooks.org/43670) | ~596 | Encyclopedia of science and Kabbalah |
| Yesod Olam | Isaac Yisraeli | 1310 | [HebrewBooks 32673](https://hebrewbooks.org/32673) (Part I), [32674](https://hebrewbooks.org/32674) (Part II) | ~192+ | Cosmological distances and Jewish calendar |
| Milchamot HaShem | Gersonides | 1560 (written 1329) | [HebrewBooks 9457](https://hebrewbooks.org/9457) | ~460 | Philosophy and cosmology (printed edition, minus astronomy) |
| Sefer HaTechunah | Gersonides | 1397 manuscript | [BnF Hébreu 724 via Gallica](https://gallica.bnf.fr/ark:/12148/btv1b10544205n) | ~514 | The never-printed astronomical treatise — 136 chapters from manuscript |
| Ha-Ish Al HaChomah | Shlomo Zalman Sonnenfeld | 20th c. | [HebrewBooks 50062](https://hebrewbooks.org/50062) | ~varies | Modern Hebrew biography — easiest scan in the corpus |

### Latin works
| Work | Author | Date | Source | Pages | Notes |
|---|---|---|---|---|---|
| Astronomiae Instauratae Progymnasmata | Tycho Brahe | 1610 | [Internet Archive](https://archive.org/details/bub_gb_CVOItHLenPEC) | ~927 | Brahe's principal scientific work, edited by Kepler |
| Astronomiae Instauratae Mechanica | Tycho Brahe | 1602 | [Internet Archive](https://archive.org/details/gri_tychonisbrah00brah) | ~107 | Illustrated instrument catalog — *source CLAUDE.md not yet written* |
| De Mundi Aetherei Recentioribus Phaenomenis | Tycho Brahe | 1588/1603 | [Internet Archive](https://archive.org/details/bub_gb_2f-EqKxRN34C) | ~465 | The Tychonic system's formal debut |
| Epistolarum Astronomicarum Libri | Tycho Brahe | 1596/1601 | [Internet Archive](https://archive.org/details/tychonisbrahedan00brah) | ~400 | Astronomical correspondence with Kassel observatory |
| Astronomia Danica | Longomontanus | 1640 | [Internet Archive](https://archive.org/details/astronomiadanica00long) | ~532 | Definitive Tychonic system textbook — **completed reference run** |

## How to Use It

### Prerequisites
- **Claude Code** with access to Claude Opus (for translation subagents). Install: <https://docs.anthropic.com/claude/docs/claude-code>. Runs on macOS, Linux, and Windows (WSL or native).
- **A PDF splitter**: `qpdf` recommended (`brew install qpdf`, `apt install qpdf`, `pacman -S qpdf`, `winget install qpdf.qpdf`, or [release builds](https://github.com/qpdf/qpdf/releases)). Python fallbacks: `pip install pikepdf` or `pip install PyPDF2`.
- **Pandoc ≥ 3.x** for `.docx` output (`brew install pandoc`, `apt install pandoc`, `pacman -S pandoc`, `winget install JohnMacFarlane.Pandoc`, or [static binaries](https://github.com/jgm/pandoc/releases)). LibreOffice works as a fallback but renders complex tables less well.
- **Source PDFs** placed in the appropriate `source/` directory (links in each work's `source/CLAUDE.md`, or use the `Add <url>` flow below).

### Setup
```
git clone https://github.com/sweisman/translation-pipeline.git
cd translation-pipeline
```

### Adding a new work from a URL
From the project root in a Claude Code session:

```
Add <url>
```

…where `<url>` points to the book's catalog page on Internet Archive, HebrewBooks.org, Gallica, or similar. Claude fetches metadata, picks the canonical example for the language (Latin → `longomontanus/astronomia_danica`, Hebrew → `gans/tzemach_david`), confirms a directory name, and scaffolds `source/CLAUDE.md` and `translation/`. Drop the source PDF in `<author>/<work>/source/` and run `Translate <author>/<work>`. See `CLAUDE.md` for the full flow, including the manual fallback.

### Translating a work
```
claude
Translate gans/tzemach_david
```

The orchestrator reads the work's `source/CLAUDE.md`, splits the PDF, and translates batch by batch. Output lands in `gans/tzemach_david/translation/`.

For manuscript sources requiring IIIF download (e.g., Gersonides' *Sefer HaTechunah*), run the download step first: `Download gersonides/sefer_hatechunah`.

### Platform notes
Path separators in commands you type to Claude (`Translate gans/tzemach_david`) use forward slashes on every OS — they're directory references, not shell paths. On Windows, PowerShell, cmd.exe, and WSL all work; if a tool is only on PATH inside WSL, run `claude` inside WSL too.

### Monitoring progress
The orchestrator logs a structured batch report after each batch and pauses 5 minutes between batches. The delay is **load-bearing**: Claude Pro/Max plans have a rolling session window (~5 hours) the orchestrator can't see directly, and without pacing a long run exhausts the window mid-work. The 5-minute spacing keeps a ~40-batch run inside one window.

When the window is hit, the orchestrator reports a resume point. Start a new session and paste:

```
Resume gans/tzemach_david from batch 39
```

It confirms the last successfully completed batch from on-disk `batch_NN.md` files before resuming.

## The Workflow

After all batches complete, the pipeline runs a five-stage reconciliation before producing final output:

1. **In-flight logging** — anomalies captured to `rerun_candidates.txt` during translation.
2. **Categorized reconciliation report** — every flagged issue sorted into A (rerun likely helps), B (compositor error, footnote), C (author/source anomaly, footnote), or D (fix at collation).
3. **Human selects rerun set** from Category A.
4. **Reruns execute under verification framing** — "Check whether [hypothesis] — report what the source actually shows," not "apply this fix." Volvelles and similar diagrams may need multiple passes.
5. **Collation** to `<work>_complete.md` and `.docx` via pandoc, plus a comprehensive discrepancy report for editorial follow-up.

Full details in [`CLAUDE.md`](CLAUDE.md).

## Cost and Throughput

The pipeline uses Claude Opus for translation subagents. Approximate throughput:

| Plan | Throughput | Weekly capacity |
|---|---|---|
| Claude Max ($100/mo) | ~40 batches per 5-hour window | ~1,500 pages/week |
| Claude Pro ($20/mo) | ~8 batches per 5-hour window | ~300 pages/week |
| API (pay-per-token) | Budget-dependent | Batch API is 50% cheaper |

Rough estimates per work:

| Work | Pages | Batches | Sessions (Max) | Sessions (Pro) |
|---|---|---|---|---|
| Brahe, *Mechanica* | ~107 | ~27 | 1 | 4 |
| Gans, *Tzemach David* | ~230 | ~58 | 2 | 8 |
| Gans, *Nechmad ve-Na'im* | ~170 | ~43 | 2 | 6 |
| Brahe, *De Mundi Aetherei* | ~465 | ~117 | 3 | 15 |
| Gersonides, *Sefer HaTechunah* | ~514 | ~129 | 4 | 17 |
| Longomontanus, *Astronomia Danica* | ~532 | ~133 | 4 | 17 |
| Hurwitz, *Sefer HaBrit* | ~596 | ~149 | 4 | 19 |
| Brahe, *Progymnasmata* | ~927 | ~232 | 6 | 30 |

The entire corpus (~4,500 pages) takes roughly 4–6 weeks on Claude Max running one session per day, or significantly longer on Pro.

## Lessons Learned

Hard-won observations from actual runs (mostly the Longomontanus *Astronomia Danica* reference run, 133 batches × 4 pages):

- **Hebrew numeral misreading is the #1 error source for Hebrew works.** The gershayim (״) / kaf (כ) confusion alone caused most rescans in early runs. Expanded numeral-accuracy guidance in the agent prompt dramatically reduced errors.
- **Roman vs. Arabic numeral normalization is the #1 silent-error source for Latin works.** Subagents will silently render "Cap. 11." (Arabic) as "Cap. II." (Roman) when the rest of the book uses Roman, hiding a real compositor inconsistency. The rule "transcribe numerals exactly as printed" was added after this surfaced.
- **Running headers are essential evidence.** Initially the subagent inferred section boundaries from body cues instead of reading the banner at the top of each page. Making running-header reporting structurally required eliminated an entire class of boundary errors. Headers in 17th-century printing are frequently stale or premature; trust body headings when they disagree, but report both verbatim.
- **Flag numerical impossibles.** "267° 64′" or "30 gr. within a single zodiac sign" can't be right — flagging them inline (rather than silently fixing) is the only way to distinguish source-text compositor errors from subagent misreads.
- **Reruns must verify, not apply.** When rerunning with a correction hypothesis, the subagent must test the hypothesis against the source rather than blindly applying it. The opposite produced confidently wrong output. Frame rerun prompts as "Check whether [hypothesis] — report what the source actually shows."
- **Volvelles and dial-faces need multiple passes.** Figures with small peripheral labels (Longomontanus's nocturnal volvelle had 22 reference-star names around its rim) often need two or three focused verification passes. The editor cost of unresolved `[?]` flags is much higher than the cost of one more rerun.
- **Manuscript translation is feasible but rough.** A 14th-century Sephardic manuscript hand is readable at ~70–80% accuracy. The output is a useful rough draft, not a polished translation. Plan for a longer discrepancy report and more editorial review.
- **4 pages per batch is the sweet spot for printed books.** More and accuracy degrades on later pages. For table-heavy sections, consider dropping to 2.
- **Pacing matters and is load-bearing.** Without delays between batches, long runs hit the session window ceiling and stall. 5-minute pacing spreads ~40 batches across a 5-hour window. It's about the user's plan-level rate limit, not the orchestrator's context budget.
- **Pandoc beats LibreOffice for `.docx` conversion.** LibreOffice's HTML importer auto-fits table columns based on content, which collapses empty cells and breaks complex astronomical tables. Pandoc produces native Word tables that render correctly.

## License

Pipeline code and configuration files are MIT. Source texts are public domain. Translations produced by this pipeline are derivative works; please credit the original authors and source institutions.

## Contact & Support

- Email: **ArsAstronomica@protonmail.com**
- X: [@ArsAstronomica](https://x.com/ArsAstronomica)

If this project is useful to you, you can support me on [Ko-fi](https://ko-fi.com/arsastronomica).
