# Tzemach David — HebrewBooks ID 36906

## Book Metadata
- **Title**: Tzemach David (צמח דוד)
- **Author**: David Gans (דוד בן שלמה גנז), 1541–1613
- **Edition**: Warsaw, 1859 (originally Prague, 1592)
- **Source**: HebrewBooks.org ID 36906
- **Pages**: 230
- **Structure**: Part I — Jewish history from creation to 1592. Part II — world/gentile history from Julius Caesar to Emperor Rudolph.
- **Language**: Hebrew (square type)
- **Note**: This edition may contain a Part III (1592–1692, by R. David ben Moses of Reindorf, not by Gans) and possibly further supplements up to 1859. If encountered, note where Gans's original text ends and later additions begin, but translate everything.

## Context
Gans's Hebrew historical chronicle, written by the same author as *Nechmad ve-Na'im* and a member of the Maharal's Prague circle. Part II — Gans's deliberate decision to translate non-Jewish history into Hebrew, with a preface justifying secular study — is of particular scholarly interest. The chronicle format is brief: entries are dated and short, with dense sequences of names and events.

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating David Gans's *Tzemach David* (Warsaw, 1859 edition; originally Prague, 1592), a Hebrew historical chronicle. Part I covers Jewish history from creation to 1592 — biblical figures, prophets, Tannaim, Amoraim, Savoraim, Geonim, and later rabbis. Part II covers world/gentile history from Julius Caesar to Emperor Rudolph. Entries are chronological and generally brief.
>
> This edition may contain a Part III (covering 1592–1692, by R. David ben Moses of Reindorf, not by Gans) and possibly further supplements up to 1859. If encountered, note clearly where Gans's original text ends and later additions begin, but translate everything.
>
> Hebrew dates use the Jewish calendar (Anno Mundi). Preserve these and add CE equivalents in brackets where possible. Part II references many non-Jewish historical figures — names transliterated into Hebrew need identification in brackets.
>
> Gans's preface to Part II contains his justification for studying secular history — translate with particular care; it is of standalone scholarly interest.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- Chronicle format with dense sequences of dates, names, and brief entries.
- Hebrew dates use the Jewish calendar (Anno Mundi); add CE equivalents in brackets where possible.
- Part II references many non-Jewish historical figures — names may be transliterated into Hebrew and need identification.
- Gans's preface to Part II contains his justification for studying secular history — translate with care.
