# De Mundi Aetherei Recentioribus Phaenomenis — Internet Archive

## Book Metadata
- **Title**: De Mundi Aetherei Recentioribus Phaenomenis Liber Secundus ("On Recent Phenomena in the Celestial World, Book Two")
- **Author**: Tycho Brahe (1546–1601)
- **Edition**: Originally printed at Uraniborg, 1588; reissued Prague, 1603 with new title page and dedication by Tengnagel
- **Source**: Internet Archive (https://archive.org/details/bub_gb_2f-EqKxRN34C) — Google Books scan
- **Pages**: [16] + 465 + [2] pages
- **Language**: Latin (Roman type with woodcut diagrams of cometary paths and planetary systems)

## Context
Part II of Brahe's projected three-volume series on recent celestial phenomena (Part I is the *Progymnasmata*; Part III was never written). It covers the Great Comet of 1577 and contains Brahe's formal presentation of the Tychonic geoheliocentric system — the model in which Earth is stationary, the Sun orbits Earth, and the planets orbit the Sun. This is THE text where Brahe lays out the cosmological architecture that David Gans encountered at Benátky and that Longomontanus later systematized in *Astronomia Danica*. Chapter 6 contains the famous diagram of the Tychonic system and the arguments for it against both Ptolemy and Copernicus.

## Subagent Task Prompt
The generic Latin-translation rules and the required batch-report format live in `.claude/agents/latin-translator.md`. Use the following work-specific orientation as the task context for each batch (the agent inherits everything else):

> Translating Tycho Brahe's *De Mundi Aetherei Recentioribus Phaenomenis Liber Secundus* (Uraniborg, 1588 / Prague, 1603), his treatise on the comet of 1577 and his geoheliocentric cosmological system. Latin, Roman type, woodcut diagrams.
>
> Chapter 6 is the centerpiece — Brahe's formal presentation of his planetary system. Translate with particular care; describe every diagram in this chapter in full detail.
>
> The 1603 reissue has a new title page and dedication by Franciscus Gansneb Tengnagel (Brahe's son-in-law). Translate all preliminary matter and identify each element (title page, Tengnagel dedication, original Brahe preface, etc.).
>
> The book contains detailed positional observations of the comet of 1577. Reproduce observational tables in full per the agent's table rules.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`latin-translator`

## Known Challenges
- The 1588 printing was done on Brahe's private press at Uraniborg; the 1603 reissue has a new title page and preliminary matter but the body text is from the original sheets. Print quality may vary across the volume.
- Chapter 8 contains Brahe's arguments against Copernicus — directly relevant to the Gans corpus and worth careful translation.
- Diagrams of cometary paths include labeled geometric points — describe all labeled elements.
- The scan is a Google Books digitization and may have occasional quality issues (finger shadows, skewed pages).
