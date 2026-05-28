# Nechmad ve-Na'im — HebrewBooks ID 20763

## Book Metadata
- **Title**: Nechmad ve-Na'im (נחמד ונעים)
- **Author**: David Gans (דוד בן שלמה גנז), 1541–1613
- **Edition**: Jessnitz, 1743 (first and only printed edition)
- **Source**: HebrewBooks.org ID 20763
- **Structure**: 12 sections (שער), 305 paragraphs (סימן)
- **Language**: Hebrew (square type, some Rashi script for secondary text)
- **Note**: This is a more complete scan than ID 14299. Prefer this scan for translation; use 14299 only to cross-check.

## Context
David Gans's Ptolemaic astronomical textbook, written by a member of the Maharal's Prague circle who personally visited Tycho Brahe at Benátky. Gans cites the Brahe corpus, Longomontanus, Yisraeli's *Yesod Olam*, and others. This work is the Hebrew-language hinge between the Latin Tychonic literature (Brahe, Longomontanus) and the medieval Jewish cosmological tradition (Yisraeli, Gersonides).

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating David Gans's *Nechmad ve-Na'im* (Jessnitz, 1743), a Ptolemaic astronomical textbook in Hebrew. The book has 12 sections (שער) and 305 paragraphs (סימן). Paragraph headers are marked with סימן followed by a Hebrew numeral. The scan (HebrewBooks ID 20763) is the more complete of the two available scans of this edition. 18th-century square Hebrew type, sometimes degraded; some Rashi-script secondary text; occasional astronomical diagrams with Hebrew labels.
>
> COMPOSITOR ERRORS: The 1743 Jessnitz print has documented compositor errors (see Georg Alter, *Aleph* 11.1, 2011). Proper names — especially transliterated Greek, Latin, and Arabic astronomer names — are frequently garbled in transmission. When a name is unrecognizable, attempt identification from context (epoch, field of work, associated discoveries) and flag with `[?]` if uncertain.
>
> Identify named persons in brackets. Note cited Jewish sources in brackets.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- 18th-century typeface with degraded ink in places.
- Compositor errors documented by Georg Alter — astronomer names frequently garbled.
- Some astronomical terms are transliterations of Latin/Greek names in Hebrew letters — attempt identification.
