# Astronomiae Instauratae Progymnasmata — Internet Archive

## Book Metadata
- **Title**: Astronomiae Instauratae Progymnasmata ("Introductory Exercises Toward the Restoration of Astronomy")
- **Author**: Tycho Brahe (1546–1601)
- **Editor/Appendix**: Johannes Kepler (1571–1630) — prepared the book for publication after Brahe's death and wrote the appendix on pp. 817–822.
- **Edition**: Frankfurt, 1610 (typesetting begun at Uraniborg, completed in Prague). Publisher: Gottfried Tampach, Frankfurt.
- **Source**: Internet Archive (https://archive.org/details/bub_gb_CVOItHLenPEC) — National Central Library of Rome copy, 927 scanned pages. Alternate scan from University of Seville: https://archive.org/details/A021051 (887 pages, 400 PPI but smudged in early pages).
- **Pages**: [16] + 822 + [12] (~850+ scanned pages)
- **Structure**: Part I of a projected multi-volume work on recent astronomical phenomena. Covers solar and lunar restitution, the fixed stars (Brahe's pre-telescopic catalog), and an extensive treatment of the nova of 1572. Part II was *De mundi aetherei recentioribus phaenomenis* (Uraniborg, 1588). Part III was never written.
- **Language**: Latin (Roman and italic type; woodcut illustrations; title page in two colors red/black)
- **Physical features**: Woodcut initials, printed marginalia, astronomical diagrams, star catalogs, observational tables

## Context
Brahe's principal scientific work — the definitive statement of his observational program and the foundation of all subsequent Tychonic astronomy. Solar and lunar theories, the catalog of fixed stars (most precise pre-telescopic catalog), detailed analysis of the nova of 1572 (which proved that change occurs in the celestial realm, contradicting Aristotle), and observational methods.

Kepler inherited the manuscript after Brahe's death in Prague (October 1601) and shepherded it to publication. The appendix on pp. 817–822 is Kepler's own contribution. David Gans visited Brahe's observatory at Benátky during the period when this work was being finalized (1600–1601); the observations and methods described here are what Gans witnessed firsthand. Longomontanus's *Astronomia Danica* (1640) is the systematization of the program laid out in this book.

## Subagent Task Prompt
The generic Latin-translation rules and the required batch-report format live in `.claude/agents/latin-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating Tycho Brahe's *Astronomiae Instauratae Progymnasmata* (Frankfurt, 1610), his principal scientific work, prepared for publication posthumously by Kepler. Latin, Roman and italic type, printed marginalia, woodcut initials, title page in two colors.
>
> Coverage: solar restitution, lunar theory, fixed stars (including Brahe's star catalog — the most precise pre-telescopic catalog), and an extensive treatment of the nova of 1572. Kepler's appendix occupies pp. 817–822 — when you reach those pages, note clearly that authorship shifts from Brahe to Kepler.
>
> The 16 preliminary pages contain a title page, dedication, privilege, and prefatory material. Translate all and identify each element. Note the two-color (red/black) printing of the title page.
>
> Brahe's star catalog is a centerpiece. Reproduce in full per the agent's table rules — every star name (Latin and/or Arabic), constellation assignment, ecliptic coordinates, and magnitude. Do not summarize or abbreviate. The nova-of-1572 sections include parallax measurements and geometric arguments with labeled diagrams critical to the scientific argument.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`latin-translator`

## Known Challenges
- Large work (~850 scanned pages → ~210+ batches at 4 pages each). Plan the run across multiple sessions per the project pacing rule.
- Star-catalog batches are table-heavy and benefit from extra attention to numerical accuracy.
- Brahe's Latin is technical and precise. His observational narratives (especially the nova sections) mix technical measurement with historical narrative.
- Marginalia are integral — cross-references, source citations, and summaries of the main argument live there.
- The 1610 printing was completed posthumously. Some sections may show editorial seams between Brahe's manuscript and Kepler's editorial work — note any shifts in voice or style.
- Woodcut diagrams of celestial positions, instrument schematics, and geometric proofs are frequent. Describe all labeled elements.
