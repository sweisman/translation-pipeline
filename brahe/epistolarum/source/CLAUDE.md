# Epistolarum Astronomicarum Libri — Internet Archive / Library of Congress

## Book Metadata
- **Title**: Epistolarum Astronomicarum Libri ("Books of Astronomical Letters")
- **Author**: Tycho Brahe (1546–1601), with Landgrave Wilhelm IV of Hesse-Kassel (1532–1592) and Christoph Rothmann (fl. 16th c.)
- **Edition**: Uraniborg, 1596; reissued Nuremberg by Levinus Hulsius, 1601 (first gathering reset)
- **Source**: Internet Archive — search 1596 or 1601 edition. Also available via Library of Congress: https://www.loc.gov/item/85194824/
- **Pages**: [40] + 309 + [2] (~400 total with preliminaries)
- **Language**: Latin and German. German letters are followed by their Latin translations.
- **Structure**: Brahe's correspondence with Landgrave Wilhelm IV and Wilhelm's astronomer Christoph Rothmann. Subsequent volumes were planned but never published.

## Context
Brahe's astronomical correspondence — real-time arguments for his system against both Ptolemy and Copernicus, in debate with the competing observatory at Kassel. Rothmann was Brahe's most capable interlocutor and pushed back on specific technical points. The letters document:
- Brahe's arguments for the Tychonic system vs. Copernicus
- The "star size" argument: Brahe showed that if stars had the apparent widths he measured, Copernican distances would require stars to be absurdly immense — far larger than the Sun
- Competing observational programs at Uraniborg and Kassel
- Technical discussions of instruments, methods, and specific observations
- Rivalry and cooperation between the two observatories

David Gans mentions Brahe's "12 men, all of them learned and skilled in the science." These letters show those men at work, debating methods and results in real time.

## Subagent Task Prompt
The generic Latin-translation rules and the required batch-report format live in `.claude/agents/latin-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating Tycho Brahe's *Epistolarum Astronomicarum Libri* (Uraniborg, 1596 / Nuremberg, 1601), his published astronomical correspondence with Landgrave Wilhelm IV of Hesse-Kassel and Christoph Rothmann. Bilingual: letters appear in both German and Latin.
>
> BILINGUAL TEXT: Translate from the Latin. When a German original precedes its Latin translation, note `[German original precedes]` and translate from the Latin. If significant differences between the German and Latin are visible, note them.
>
> LETTER STRUCTURE: Each letter has a sender, recipient, and date. Preserve these headers exactly. Mark each letter boundary clearly with a horizontal rule or labeled heading so the collation pipeline can index by letter as well as by page.
>
> Identify named persons, places, and instruments in brackets. Translate all prefatory material, dedications, and privileges.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`latin-translator`

## Known Challenges
- Bilingual Latin/German. The German is 16th-century Kanzleideutsch, significantly different from modern German. Translate from the Latin when both are available.
- Epistolary Latin is less formal than treatise Latin — colloquialisms, personal asides, and incomplete thoughts are normal.
- Numerous errors in pagination were noted in the original printing; an errata page exists at the end.
- The letters contain references to specific observations, instruments, and celestial events that should be identified where possible.
- Rothmann's letters argue against Brahe on specific points — the back-and-forth *is* the substance. Preserve the argumentative structure clearly.
- Some letters reference drawings or tables that may have been enclosed with the original correspondence but not reproduced in the printed edition — note these references.
