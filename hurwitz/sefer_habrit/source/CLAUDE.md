# Sefer HaBrit HaShalem — HebrewBooks ID 43670

## Book Metadata
- **Title**: Sefer HaBrit HaShalem (ספר הברית השלם)
- **Author**: R. Pinchas Eliyahu Hurwitz (הורביץ, פינחס אליהו בן מאיר), 1765–1821
- **Edition**: Expanded "HaShalem" edition (19th century; first published Brünn, 1797)
- **Source**: HebrewBooks.org ID 43670
- **Pages**: 596
- **Structure**: Part I (מאמר ראשון) — natural sciences: astronomy, physics, geography, chemistry, biology, medicine. Part II (מאמר שני) — metaphysics, ethics, the soul, prophecy, and Kabbalah. Each part divided into sections and chapters.
- **Language**: Hebrew (19th-century square type, generally cleaner than the Gans scans; some Rashi script)
- **Sections of particular interest**: Part I, Section 3, Chapters 3–4 (astronomy, cosmology, extraterrestrial life). Flag these when reached.

## Context
A late-Enlightenment Hebrew encyclopedia of science and Kabbalah, drawing on European scientific literature (often through intermediate Hebrew translations) and integrating it with Lurianic kabbalistic frameworks. Hurwitz's chapters on extraterrestrial life are notable as one of the earliest Jewish treatments of the topic. The expanded "HaShalem" edition adds ~350 entries to the 1797 first edition.

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating R. Pinchas Eliyahu Hurwitz's *Sefer HaBrit HaShalem* (ספר הברית השלם), an encyclopedic work of science and Kabbalah first published in 1797. Part I (מאמר ראשון) covers natural sciences — astronomy, physics, geography, chemistry, biology, medicine. Part II (מאמר שני) covers metaphysics, ethics, the soul, prophecy, and Kabbalah. Each part is divided into sections and chapters. The scan (HebrewBooks ID 43670, 596 pages) is 19th-century square Hebrew, generally cleaner than the Gans scans, with some Rashi script.
>
> KABBALISTIC TERMINOLOGY: Preserve references to the four Kabbalistic worlds (Atzilut, Beriah, Yetzirah, Asiyah) in transliteration with translation in brackets on first occurrence.
>
> SCIENTIFIC TERMINOLOGY: Mixes scientific terminology (often borrowed from European languages, sometimes Latinized in Hebrew letters) with Kabbalistic terminology. Identify the European source term in brackets where recognizable.
>
> SECTIONS OF PARTICULAR INTEREST: Part I, Section 3, Chapters 3–4 cover astronomy, cosmology, and extraterrestrial life — flag these when reached.
>
> EXPANDED EDITION: This is the "HaShalem" edition with ~350 additions over the 1797 Brünn first edition. References to events post-1797 are normal authorial additions, not errors.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- Mixes scientific terminology (often borrowed from European languages) with Kabbalistic terminology.
- References to the four Kabbalistic worlds should be preserved in transliteration with translation in brackets on first occurrence.
- The astronomy and extraterrestrial life passages (Part I, Section 3, Chapters 3–4) are of particular interest — flag these when reached.

### Hurwitz-specific print conventions
- Chapters often use incipit-word headings ("פרק י"ב הנה" / "פרק י"ג ועתה") — the opening word functions as the chapter title.
- Discourses may reach 30+ chapters, so most chapter numerals are two letters (כ"ה, ל"ב, etc.). Two-letter numerals are normal, not anomalous.
- Running headers on verso pages sometimes lag body headings or persist from the prior section — agent rule 10 already handles this (trust body headings, report both verbatim).
