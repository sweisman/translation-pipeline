# Sefer HaTechunah (Book of Astronomy) — BnF Manuscript Hébreu 724

## Book Metadata
- **Title**: Sefer HaTechunah (ספר התכונה, "Book of Astronomy") — formally Book V Part 1 of *Milchamot HaShem*
- **Author**: R. Levi ben Gershom (Gersonides / Ralbag), 1288–1344, Provence
- **Manuscript**: Paris, Bibliothèque nationale de France, Département des manuscrits, Hébreu 724
- **Date**: 1397
- **Script**: Sephardic hand on paper
- **Source**: Gallica / Ktiv project (digitized in cooperation with the National Library of Israel and the Friedberg Jewish Manuscript Society)
- **Viewer**: https://gallica.bnf.fr (search Hébreu 724); IIIF manifest via Biblissima: https://iiif.biblissima.fr/collections/manifest/944440d1d7f8de341ae8937f40c8edb4c904fba5
- **IIIF Manifest**: Provided as `gersonides-manifest.json` in the source directory.
- **Folios**: 257 folios (1r–257v), 514 page images. In Gallica numbering: f12 (=1r) through f525 (=257v). Pages f1–f11 and f526–f541 are covers, endpapers, and binding shots — skip these.
- **Structure**: 136 chapters (פרקים) of mathematical astronomy — solar theory, lunar theory, eclipses, planetary models, fixed stars, observational instruments and methods. Part 1 of Book V of *Milchamot HaShem*. Parts 2 and 3 (cosmology and theology) are covered under `gersonides/milchamot_hashem/`.
- **Language**: Hebrew (14th-century Sephardic manuscript hand)
- **Estimated batches**: ~129 at 4 pages per batch.

## Image Download
The manuscript images are not available as a single PDF. Download individual folio images from the Gallica IIIF endpoint and combine into a PDF before splitting into batches.

**URL pattern:**
```
https://gallica.bnf.fr/iiif/ark:/12148/btv1b10544205n/f{N}/full/full/0/native.jpg
```
where N ranges from 12 to 525 for the text folios.

**Resolution**: Full resolution is 4974 × 4134 pixels per page (very large PDF, ~5–10 GB for 514 images). For a more manageable file while retaining manuscript readability, download at reduced resolution by replacing `/full/full/` with `/full/1200,/` in the URL. 1200px width is usually sufficient for the Sephardic hand; redownload problem pages at full resolution if needed.

**Download and combine command (for the orchestrator):**
```
Download folio images f12 through f525 from the Gallica IIIF endpoint and combine into a single PDF at gersonides/sefer_hatechunah/source/bnf_hebreu_724.pdf. Use 1200px width for manageable file size. Then split into 4-page batches and proceed with translation.
```

## Context
The most technically original section of Gersonides' entire oeuvre — and it has never been printed. The printers of the 1560 Riva di Trento and 1866 Leipzig editions both omitted it as "too large a book in itself." David Gans writes in the epilogue of *Nechmad ve-Na'im* that he never saw it. Bernard Goldstein published a critical edition of chapters 1–20 with English translation (Springer, 1985); chapters 21–136 have never been translated into any language.

Other manuscripts: Paris BnF Hébreu 696, Hébreu 725; London BL Add. 26921; Naples (chapters 1–95 only); Berlin Staatsbibliothek Ms. or. fol. 4057 (starting folio 53r). A Latin translation made in Gersonides' own lifetime (1342) at the request of Pope Clement VI survives in Vatican Mss. 3380 and 3098.

## CRITICAL: This is a manuscript, not a printed book
- The source is a 14th-century handwritten manuscript in Sephardic Hebrew script.
- Accuracy will be significantly lower than for printed books. Expect 70–80% on a first pass.
- The discrepancy report for this work will be substantially longer than for printed sources.
- The output should be treated as an **experimental manuscript-grade rough draft**, requiring more human editorial review than any printed-book translation in this project.

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating a 14th-century Hebrew manuscript: Gersonides' *Sefer HaTechunah* (Book of Astronomy), Book V Part 1 of *Milchamot HaShem*. Source manuscript: BnF Hébreu 724, dated 1397, Sephardic script on paper. This text has never been printed and has only been partially translated (chapters 1–20 by Bernard Goldstein, 1985).
>
> MANUSCRIPT READING: This is handwritten, not printed. The Sephardic hand is relatively regular, but expect:
> - Abbreviations marked with superscript strokes — expand where recognizable, flag with `[?]` where uncertain.
> - Letter blurring at line endings where the scribe compressed text.
> - Water damage on some margins.
> - Occasional interlinear corrections or additions by the scribe — translate and mark as `[Interlinear: …]`.
>
> CHAPTER STRUCTURE: 136 chapters (פרקים). Chapter headers should appear as פרק followed by a Hebrew numeral. Read these with extreme care — manuscript numerals are the highest-risk element. Apply the agent's numeral-accuracy rule rigorously.
>
> MATHEMATICAL CONTENT: Geometric proofs, astronomical calculations, observational data. Preserve all numerical values exactly. Describe all diagrams and geometric figures, listing all labeled points and their roles.
>
> OBSERVATIONAL DATA: Gersonides records his own observations with dates, instrument descriptions, and measured values. These are of particular scientific importance — translate with maximum precision.
>
> ERR HEAVILY TOWARD `[?]` FLAGS. Given the manuscript source, a flagged reading is far more useful than a silent misreading.
>
> Note folio numbers (recto/verso) where visible.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- The hardest text in the entire corpus. Manuscript Hebrew, dense mathematical astronomy, never-before-translated content.
- 14th-century Sephardic script — more legible than Ashkenazi manuscript hands but significantly harder than any printed text in the project.
- Abbreviations are frequent in medieval scientific Hebrew. Common ones: ר"ל (רצה לומר, "meaning"), וכו' (וכולי, "etc."), but many domain-specific abbreviations for astronomical terms.
- Geometric diagrams may be drawn freehand with labeled points. Describe as precisely as possible.
- Folio numbers may be marked in the margin or may need to be tracked by PDF page number.
- Astronomical tables (if present in this manuscript — the Naples manuscript lacks tables) are critical data. Reproduce in full if legible.
- Cross-reference with Goldstein's chapters 1–20 is recommended post-translation as a quality check, but Goldstein is not available as a digital source for this project.
- Expect the discrepancy report to be 3–5× longer than for a printed book of equivalent length.
