# Nechmad ve-Na'im — HebrewBooks ID 14299

## Book Metadata
- **Title**: Nechmad ve-Na'im (נחמד ונעים)
- **Author**: David Gans (דוד בן שלמה גנז), 1541–1613
- **Edition**: Jessnitz, 1743 (first and only printed edition)
- **Source**: HebrewBooks.org ID 14299
- **Structure**: 12 sections (שער), 305 paragraphs (סימן)
- **Language**: Hebrew (square type, some Rashi script for secondary text)
- **Known issue**: Some pages are missing from this scan. See `nechmad_venaim_20763` for a more complete version.

## Context
David Gans's Ptolemaic astronomical textbook, written by a member of the Maharal's Prague circle who personally visited Tycho Brahe at Benátky. Gans cites the Brahe corpus, Longomontanus, Yisraeli's *Yesod Olam*, and others. This work is the Hebrew-language hinge between the Latin Tychonic literature (Brahe, Longomontanus) and the medieval Jewish cosmological tradition (Yisraeli, Gersonides).

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating David Gans's *Nechmad ve-Na'im* (Jessnitz, 1743), a Ptolemaic astronomical textbook in Hebrew. The book has 12 sections (שער) and 305 paragraphs (סימן). Paragraph headers are marked with סימן followed by a Hebrew numeral. The scan (HebrewBooks ID 14299) has 18th-century square Hebrew type, sometimes degraded, with some Rashi-script secondary text and occasional astronomical diagrams with Hebrew labels.
>
> COMPOSITOR ERRORS: The 1743 Jessnitz print has documented compositor errors (see Georg Alter, *Aleph* 11.1, 2011). Proper names — especially transliterated Greek, Latin, and Arabic astronomer names — are frequently garbled in transmission. When a name is unrecognizable, attempt identification from context (epoch, field of work, associated discoveries) and flag with `[?]` if uncertain.
>
> SCAN COMPLETENESS: Some pages are missing from this particular scan. If you encounter a page-number jump or content discontinuity, note it as a scan gap rather than a textual anomaly.
>
> Identify named persons in brackets. Note cited Jewish sources in brackets.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- 18th-century typeface with degraded ink in places.
- Some pages missing from this scan; cross-reference with `nechmad_venaim_20763` for gaps.
- Compositor errors documented by Georg Alter — astronomer names frequently garbled.
- Some astronomical terms are transliterations of Latin/Greek names in Hebrew letters — attempt identification.
