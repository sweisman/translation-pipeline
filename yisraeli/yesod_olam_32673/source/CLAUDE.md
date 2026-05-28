# Yesod Olam Part I — HebrewBooks ID 32673

## Book Metadata
- **Title**: Yesod Olam (יסוד עולם, "The Foundation of the World") — Part I (*Sectio Prior*)
- **Author**: R. Isaac ben Joseph Yisraeli (יצחק בן יוסף הישראלי), active first half of 14th century, Toledo
- **Edition**: Berlin, 1846 (edited by Beer Goldberg and Aryeh Leib Rosenkranz, with introduction by David Cassel). Critical second edition; the first edition was Berlin, 1777 (edited by R. Baruch Schick of Shklov).
- **Source**: HebrewBooks.org ID 32673 (192 pages)
- **Structure**: Books 1–3 of five total:
  - Book 1 (מאמר ראשון): Mathematical introduction — geometry, trigonometry, foundational concepts.
  - Book 2 (מאמר שני): Structure of the universe — geocentric cosmological model, celestial spheres, distances.
  - Book 3 (מאמר שלישי): Geography and astronomy — time differences, motions of sun and moon, solstices, eclipses.
- **Language**: Hebrew with German epitome translation on facing/adjacent pages.

## Context
The primary medieval Jewish astronomical work that David Gans cites extensively in *Nechmad ve-Na'im*. Part I contains the cosmological content most relevant to the broader corpus:
- The "14,000 years" world-axis figure (cited by Gans in Chapter 58 for his shell-velocity calculation)
- The 6,000-parsa Earth circumference (Pesachim 94a; used by Gans for parsa calibration)
- The date-line problem (Book 2 Chapter 17 — the solution Gans later describes as broken by the discovery of the New World)
- The epistemic boundary: "we can know something only about the inner part of this highest sphere; what happens on the outer surface and beyond it is inaccessible to the human inquiring mind"

Yisraeli was a student of the Rosh (R. Asher ben Yechiel) in Toledo and wrote this work at his teacher's request. R. Moses Isserles (Gans's teacher in Cracow) wrote extensive glosses on it.

## Subagent Task Prompt
The generic Hebrew-translation rules and the required batch-report format live in `.claude/agents/hebrew-translator.md`. Use the following work-specific orientation as the task context for each batch:

> Translating Part I of R. Isaac ben Joseph Yisraeli's *Yesod Olam* (Berlin, 1846), a medieval Hebrew astronomical treatise. Coverage: mathematical foundations (geometry, trigonometry), the structure of the universe (geocentric model, celestial spheres, distances), and geography/astronomy (time, solar and lunar motion, eclipses). The edition includes Hebrew text and a German epitome translation.
>
> DUAL TEXT: Hebrew and German on facing or adjacent pages. Translate from the Hebrew. Where the German translation is visible, note any significant divergences between the German translator's rendering and your own.
>
> MATHEMATICAL CONTENT: Book 1 contains geometric and trigonometric proofs. Describe all diagrams and preserve mathematical relationships precisely.
>
> CELESTIAL DISTANCES: Book 2 contains the cosmological distance calculations that Gans cites in *Nechmad ve-Na'im*. These are of particular importance — translate with maximum precision and flag any ambiguous numerals.
>
> ISSERLES GLOSSES: R. Isserles' glosses may appear — if present, translate and mark as `[Gloss: Isserles]`.
>
> The introduction by David Cassel is in German — translate it as well.
>
> Translate this batch (PDF pages X–Y). Source: `…/source/batch_NN.pdf`. Output: `…/translation/batch_NN.md`.

## Subagent
`hebrew-translator`

## Known Challenges
- Contains technical mathematical terminology (geometry, trigonometry) in medieval Hebrew.
- Astronomical distance calculations use parsa and other units; handle carefully and convert to modern units where helpful.
- The Berlin edition's German translation provides a useful cross-check but may itself contain errors.
- R. Isserles' glosses may appear — translate and mark as `[Gloss: Isserles]`.
