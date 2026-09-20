# Requiem

**A record label whose artists will never tour again.**

An awareness page about the silencing of the wild — the measurable, ongoing loss of
natural soundscapes — built as a single self-contained `index.html`. No build step,
no framework, no dependencies, no audio or image assets.

Live idea: some species now exist only as a recording. The page treats that literally,
presenting extinction as a back catalogue you can press play on.

## The three things that make it work

**1. REQ-001 plays the gap.**
The Kauaʻi ʻōʻō sang in duets. In 1987 the last male was recorded singing his half,
leaving a pause for a female's answer that no longer existed. The player reproduces that
structure: his two-note phrase, then ~3.6 seconds where her reply belongs. Forest
ambience runs underneath the whole cycle, so the gap reads as a living forest with
nothing in it rather than digital silence. A call counter ticks up against a fixed
`Answers: 0`.

**2. The dawn chorus scrubber.**
Drag from 1970 to 2026 and the chorus thins out visually (24 dots) and audibly (voices
drop out of the generated mix). Scaled to the measured ~29% decline in North American
breeding birds. `1970` / `Today` buttons allow instant A/B, which is where the contrast
actually lands.

**3. "In your lifetime" + a personal share card.**
Enter a birth year and the page states how many birds have vanished since — and, if you
were born after 1987, that you have never heard a Kauaʻi ʻōʻō and never will. That result
is then rendered to a 1200×630 share card on a `<canvas>`, generated entirely in-browser
and downloadable as a PNG. Nothing is uploaded. Every visitor's card is different, which
is the point: it makes the statistic personal before it is shared.

**4. The run-out groove.**
After the last section the page does what a record does: it runs out. A tall sticky
section fades through four lines while a groove ring spirals inward to nothing, any
playing audio ramps to silence, and the tonearm lifts off the record.

## Everything else

- All audio is **synthesised in-browser** with the Web Audio API — oscillators, filtered
  noise, and a generated noise-impulse convolver for reverb. No audio files ship.
- Only one sound source plays at a time; audio stops itself when scrolled out of view.
- Scroll progress is rendered as a **turntable tonearm** tracking across a spinning record.
- Full `prefers-reduced-motion` support; real `<button>`/`<a>`/`<input>` semantics,
  `aria-expanded`/`aria-pressed`, a skip link, and a live region for the calculator.

## Honesty notes

This matters for an awareness project, so it is stated on the page too:

- **The audio is reconstruction, not archive.** Every sound is generated from published
  descriptions of how the originals sound. It is never presented as the real recording.
  The 1987 ʻōʻō tape is held by the Cornell Lab of Ornithology.
- **The lifetime figure is a straight-line estimate** from the measured 1970–present
  total, not a year-by-year measurement.
- Hero footage and stills are illustrative, not documentary records of the species named.

## Sources

- Rosenberg et al., *Science* (2019) — 2.9 billion birds / ~29% decline since 1970
- Morrison et al., *Nature Communications* (2021) — 25 years of quieting soundscapes
- Gordon et al., *Nature Communications* (2019) — coral reef acoustic enrichment
- Kauaʻi ʻōʻō: 1987 Cornell Lab recording; declared extinct by USFWS, October 2023
- Ivory-billed woodpecker: 1935 Cornell Lab Singer Tract recordings; last accepted
  sighting 1944; proposed extinct 2021, decision pending
- Okjökull: lost glacier status 2014; memorial plaque installed August 2019

## Before you publish

Fill in the placeholders in the Act section:
`[YOUR PLEDGE OR DONATE URL]`, `[YOUR SHARE LINK]`, `[PARTNER ORGANISATION]`.

## Running it

Open `index.html`. That's it — though the hero video loads from a remote URL, so it
needs a network connection to appear.
