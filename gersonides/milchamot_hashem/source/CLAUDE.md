# Milchamot HaShem — HebrewBooks.org + Manuscript Sources

## Book Metadata
- **Title**: Milchamot HaShem (מלחמות השם, "The Wars of the Lord")
- **Author**: R. Levi ben Gershom (Gersonides / Ralbag), 1288–1344, Provence
- **Edition**: Printed editions Riva di Trento 1560 and Leipzig 1866, available on HebrewBooks.org as ID 9457. **The printed editions OMIT the astronomical section** (Book V Part 1, *Sefer HaTechunah*).
- **Structure**: Six books (מאמרים). The astronomy is in Book V (מאמר חמישי):
  - Part 1: *Sefer HaTechunah* (Book of Astronomy) — 136 chapters of mathematical astronomy. **OMITTED FROM ALL PRINTED EDITIONS** — exists only in manuscript; see sibling work `gersonides/sefer_hatechunah/`.
  - Parts 2–3: Cosmological and cosmological-theological subjects. Included in printed editions.
  - Book VI: Creation of the world.

## The Astronomical Section Problem
Gans writes in *Nechmad ve-Na'im* that he never saw this section because "the printer omitted it saying that it was too large a book." The printed editions replace it with a note: "The first part is from the science of astronomy and from what was demonstrated in the *Almagest*, and this part is a great book in itself."

The astronomy section survives in manuscript:
- Paris, BnF, Hébreu 724 — most complete (digitized; see `gersonides/sefer_hatechunah/` for translation pipeline)
- Paris, BnF, Hébreu 696 — another manuscript
- London, British Library, Add. 26921 — partial
- Naples, National Central Library — partial

Bernard R. Goldstein edited and translated the first 20 chapters into English (*The Astronomy of Levi ben Gerson*, Springer, 1985). A critical Hebrew edition of Book V Parts 2–3 and Book VI was published by Ofer Elior (Bialik Institute).

This work directory covers the **printed text only** (Phase 1). For the manuscript astronomy (Phase 2), see `gersonides/sefer_hatechunah/`. For cross-referencing against Goldstein's translation (Phase 3), see notes in the discrepancy report at completion.

## Context
Gersonides' major philosophical work. Books I–VI excluding V.1 cover the soul and intellect (I), prophecy and divination (II), divine knowledge (III), providence (IV), celestial substances and cosmology (V Parts 2–3), and creation (VI). Book V Parts 2–3 are the cosmological arguments that directly connect to Gans's *Nechmad ve-Na'im* and the broader Tychonic corpus.

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating R. Levi ben Gershom's *Milchamot HaShem* (Riva di Trento, 1560), a major work of medieval Jewish philosophy. Coverage: the soul and intellect (Book I), prophecy and divination (Book II), divine knowledge (Book III), providence (Book IV), celestial substances and cosmology (Book V Parts 2–3), and creation (Book VI).
>
> NOTE: Book V Part 1 (*Sefer HaTechunah*, mathematical astronomy, 136 chapters) was omitted from this edition. If a note about this omission appears in the text, translate it and flag it. The manuscript version is being translated separately under `gersonides/sefer_hatechunah/`.
>
> PHILOSOPHICAL TERMINOLOGY: Preserve key philosophical terms with Hebrew in brackets on first occurrence, e.g., `the Active Intellect [השכל הפועל]`, `acquired intellect [השכל הנקנה]`.
>
> Book V Parts 2–3 (cosmological sections) are of particular interest for cross-reference with the astronomical corpus — flag these when reached.
>
> Identify named persons and cited works in brackets.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- 1560 Riva di Trento is early Hebrew printing — expect degraded type.
- Gersonides' philosophical Hebrew is dense and technical, heavily influenced by Averroist Aristotelianism.
- Frequent references to Aristotle, Averroes, Ptolemy, and other philosophers — names will be in Hebrew transliteration and need identification.
- Book V Parts 2–3 cosmological arguments are directly relevant to the broader corpus.
- The missing Book V Part 1 is a known gap. Goldstein's partial English translation (chapters 1–20) should be cross-referenced post-translation.
