# Astronomia Danica — Internet Archive

## Book Metadata
- **Title**: Astronomia Danica
- **Author**: Christen Sørensen Longomontanus (1562–1647)
- **Edition**: Amsterdam, 1640 (published by Joan and Cornelis Blaeu). This is the revised and expanded second edition; the first edition was published in 1622.
- **Source**: Internet Archive (https://archive.org/details/astronomiadanica00long)
- **Pages**: 532 scanned pages. The original collation suggests [12] preliminary + 459 main + 44 appendix + [trailing blanks]. Note: in the actual Internet Archive copy used here, the appendix on new stars and comets follows immediately after the main text's blank verso (PDF p. 477) — no separate index/errata leaves are present. Pre-collation descriptions citing "[7] pages of index/errata" do not match this copy.
- **Structure**: Main text runs to 459 numbered pages. A 44-page appendix has its own title page and separate pagination starting from 1. Preliminary matter is the standard 12 pages (title page, dedication, privilege, table of contents, commendatory verses). The appendix dedication is dated 1621 — preserved unchanged from the 1622 first edition; flag with a footnote, not as a translation anomaly.
- **Language**: Latin (Roman type with printed marginalia; woodcut initials)
- **Scan quality**: 400 PPI, ABBYY OCR already applied (but translation should work from images, not OCR text)

## Context
Longomontanus was Tycho Brahe's longest-serving assistant (1589–1600) and the principal systematizer of the Tychonic cosmological model. After Brahe's death in 1601, Longomontanus held the chair of mathematics at the University of Copenhagen and devoted the rest of his career to refining and publishing Brahe's system. *Astronomia Danica* is the definitive technical statement of the Tychonic system — the same system David Gans encountered during his visits to Brahe's observatory and which forms the background cosmology of *Nechmad ve-Na'im*.

The book covers: the structure of the cosmos (Tychonic: Earth stationary, Sun orbiting Earth, planets orbiting Sun), solar theory, lunar theory, eclipses, planetary theory, fixed stars, and precession. Practical computation tables are interleaved throughout. The 44-page appendix covers the new stars of 1572 and 1604 and the comets of 1607 (Halley's) and 1618, with both astronomical and astrological treatment.

## Subagent Task Prompt
The generic Latin-translation rules and the required batch-report format live in `.claude/agents/latin-translator.md`. Use this work-specific prompt as the task context (the agent inherits everything else):

> Translating Christen Sørensen Longomontanus's *Astronomia Danica* (Amsterdam, 1640), the definitive technical exposition of the Tychonic astronomical system. Latin, Roman type, printed marginalia, woodcut initials. Internet Archive scan at 400 PPI.
>
> The text covers the full range of positional astronomy as understood in the Tychonic framework: cosmological structure, solar and lunar theory, eclipses, planetary motions, fixed stars, precession. It includes astronomical tables, geometric diagrams, and computational examples. Marginalia (printed by the author, not later annotations) are integral to the argument — translate them per the agent's rule 2.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`. End with the structured batch report from the agent definition.

## Subagent
`latin-translator`

## Known Challenges
- 17th-century Latin with specialized astronomical vocabulary. Longomontanus's prose is technically dense.
- Marginalia are integral to the text — they often summarize or cross-reference the main argument. Do not skip them.
- The 44-page appendix has separate pagination — note the transition clearly. The dedication is dated 1621 (preserved from the 1622 first edition); not a translation anomaly.
- Astronomical tables are integral to the work and should be reproduced in full, not summarized. Some are large (e.g., the 30-row prosthaphaeresis canons of Venus, Mercury, Saturn, Jupiter, Mars) and span multiple batch pages — the collation step handles boundaries.
- Geometric diagrams with labeled points (A, B, C…) are frequent. Describe the figure and list all labeled points and their roles. The nocturnal volvelle in Liber II Cap. 5 (PDF p. 108) has ~20 small peripheral star-name labels and required multiple passes during the original run.
- The scan is high resolution (400 PPI) but the book is 384 years old — some pages may have bleed-through, foxing, or tight binding margins, particularly in the dense inner-planet reflexion tables (Cap. 24 of Liber II Theoricorum, PDF pp. 452 and 472).
- Longomontanus occasionally references Brahe's unpublished observations. Note these when encountered.
- Compositor errors are common: stale/premature running headers across chapter boundaries (verified in batches 18, 27, 36, 51, 95), digit-swaps (Cap. 12/21), Arabic/Roman numeral inconsistencies (Cap. 11 in Arabic on pp. 357–360 while the rest of the book uses Roman), and table-cell impossibles. Transcribe verbatim per agent rules 7–9; the reconciliation stage triages them.
