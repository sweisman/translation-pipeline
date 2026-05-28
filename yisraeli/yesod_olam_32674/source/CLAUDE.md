# Yesod Olam Part II — HebrewBooks ID 32674

## Book Metadata
- **Title**: Yesod Olam (יסוד עולם, "The Foundation of the World") — Part II (*Sectio Altera*)
- **Author**: R. Isaac ben Joseph Yisraeli (יצחק בן יוסף הישראלי), active first half of 14th century, Toledo
- **Edition**: Berlin, 1848 (edited by Beer Goldberg and Aryeh Leib Rosenkranz). Critical second edition; first edition was Berlin, 1777 (edited by R. Baruch Schick of Shklov).
- **Source**: HebrewBooks.org ID 32674
- **Structure**: Books 4–5 of five total:
  - Book 4 (מאמר רביעי): Calendar calculations — principles of the Jewish calendar, intercalation, new moon determination, tekufot (solstices/equinoxes), leap years.
  - Book 5 (מאמר חמישי): Astronomical tables (50+ tables with explanatory chapters) and a historical survey based on *Sefer HaKabbalah* of R. Avraham ibn Daud.
- **Language**: Hebrew with German epitome translation on facing/adjacent pages.

## Context
The practical application of the cosmological framework established in Part I. The calendar computations use the same astronomical parameters (mean lunar month of 29d 12h 793ch, solar year of Rabbi Adda) that Gans discusses in *Nechmad ve-Na'im* and that the Jewish calendar still uses today. The astronomical tables are the computational output of Yisraeli's cosmological model.

The historical survey in Book 5 traces the transmission of astronomical knowledge through Jewish history — the same lineage Gans later recounts in the epilogue of *Nechmad ve-Na'im*.

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating Part II of R. Isaac ben Joseph Yisraeli's *Yesod Olam* (Berlin, 1848), a medieval Hebrew astronomical treatise. Coverage: calendar calculations (Jewish calendar principles, intercalation, new moon, tekufot, leap years) and astronomical tables with a historical survey. The edition includes Hebrew text and a German epitome translation.
>
> DUAL TEXT: Hebrew and German on facing or adjacent pages. Translate from the Hebrew. Where the German translation is visible, note any significant divergences between the German translator's rendering and your own.
>
> CALENDAR COMPUTATIONS: Book 4 contains calendar arithmetic. Preserve all numerical values exactly, including chalakim (1/1080 of an hour) and regaim (1/76 of a chelek) fractions per the agent's rule 13. These are the same values discussed by Gans in *Nechmad ve-Na'im*.
>
> ASTRONOMICAL TABLES: Book 5 contains 50+ tables — the most table-heavy section in the entire corpus. Reproduce per the agent's table rules.
>
> ISSERLES GLOSSES: R. Isserles' glosses may appear — if present, translate and mark as `[Gloss: Isserles]`.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- Dense calendar arithmetic with chalakim and regaim fractions — must be preserved exactly.
- 50+ astronomical tables. If accuracy drops at 4 pages, consider 2-page batches for table-dense stretches (this is a workflow override; coordinate with the user).
- The historical survey (Book 5, latter portion) contains many proper names from Jewish and general history — these need identification in brackets.
- R. Isserles' glosses may appear — translate and mark as `[Gloss: Isserles]`.
- The Berlin edition's German translation provides a useful cross-check but may itself contain errors.
