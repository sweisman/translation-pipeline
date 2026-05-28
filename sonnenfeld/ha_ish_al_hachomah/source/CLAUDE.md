# Ha-Ish Al HaChomah (Part 1) — HebrewBooks ID 50062

## Book Metadata
- **Title**: Ha-Ish Al HaChomah (האיש על החומה, "The Man on the Wall")
- **Author**: R. Shlomo Zalman Sonnenfeld (שלמה זלמן בן יוסף חיים זוננפלד)
- **Subject**: Biography of R. Yosef Chaim Sonnenfeld (1848–1932), rabbi of the Edah HaChareidis in Jerusalem
- **Source**: HebrewBooks.org ID 50062
- **Language**: Modern Hebrew (printed)

## Context
A 20th-century Hebrew biography of a major early-Mandate Jerusalem rabbinic figure. Modern Hebrew print should be the easiest scan in the corpus to read. Of interest for the corpus as a window onto Ottoman and Mandate-era Jerusalem rabbinic life; references the same kinds of communal institutions and halakhic disputes that later figures in the broader project also engage.

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating *Ha-Ish Al HaChomah* (האיש על החומה, "The Man on the Wall"), a Hebrew biography of R. Yosef Chaim Sonnenfeld, the rabbi of the Edah HaChareidis in Jerusalem. Author: R. Shlomo Zalman Sonnenfeld. The scan is from HebrewBooks.org (ID 50062). Modern Hebrew print — should be significantly cleaner than the historical texts in this pipeline.
>
> CONTENT TYPE: Biographical/hagiographic. Contains historical narratives, personal anecdotes, rabbinic teachings, halakhic discussions, and accounts of communal affairs in Ottoman and Mandate-era Jerusalem.
>
> PERSONS: Identify named persons in brackets with relevant context (dates, titles, communal roles) where known.
>
> PLACES: Identify neighborhoods, institutions, and landmarks in Jerusalem and elsewhere in brackets where helpful.
>
> RABBINIC SOURCES: Where the text cites Talmudic, halakhic, or other rabbinic sources, note the reference in brackets.
>
> LETTERS AND DOCUMENTS: If the text reproduces letters, proclamations, or official documents, preserve their structure and mark each block clearly.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- Modern Hebrew print — the easiest scan in the corpus to read.
- Many proper names of rabbinical figures from 19th–20th century Jerusalem, some well-known, some obscure. Identify where possible.
- May contain Yiddish phrases or Ashkenazi Hebrew pronunciations transliterated into the text.
- Halakhic discussions reference technical terminology from *Shulchan Aruch* and responsa literature.
