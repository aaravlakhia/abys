# Requiem

**A record label whose artists will never tour again.**

An awareness page about the silencing of the wild — the measurable, ongoing loss of
natural soundscapes — built as a single self-contained `index.html`. No build step,
no framework, no dependencies, no audio or image assets.

Live idea: some species now exist only as a recording. The page treats that literally,
presenting extinction as a back catalogue you can press play on.

## Scope

The catalogue spans the animal kingdom, not just birds — seven tracks across
**birds, mammals (cetaceans), amphibians, invertebrates and the cryosphere**, each with
its own synthesised voice and a filter to browse by class:

| # | Track | Class | Status |
|---|---|---|---|
| REQ-001 | Kauaʻi ʻōʻō | Aves | Extinct 2023 |
| REQ-002 | Ivory-billed woodpecker | Aves | Presumed extinct |
| REQ-003 | Baiji (Yangtze river dolphin) | Mammalia | Functionally extinct 2006 |
| REQ-004 | Rabbs' fringe-limbed treefrog | Amphibia | Extinct 2016 |
| REQ-005 | Okjökull | Cryosphere | Gone 2014 |
| REQ-006 | The flying insects | Insecta | Collapsing (−75% biomass) |
| REQ-007 | **Vaquita** | Mammalia | **~10 left — still savable** |

REQ-007 is deliberately last. It is the only track on the label that is not finished,
and the page turns on that fact.

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

## The 3D motion system

The hero's entrance animation is the language for the entire page, extended into real 3D:

- **Masked line reveals.** Every section title uses the same double-wrapped mask as the
  headline, but the inner span rotates up out of it in 3D (`rotateX(-64deg)` → flat),
  staggered line by line.
- **Depth reveals.** Everything that scrolls in arrives from `translateZ(-120px)
  rotateX(-11deg)` rather than a flat slide, so content rises *out of* the page.
- **Cursor tilt.** Player cards, action cards and the calculator hold a live tilt under
  the pointer (rAF-throttled, `hover: hover` only).
- **The chorus has depth.** Living voices sit forward at `translateZ(+18px)`; dead ones
  fall back to `-30px`. As you drag toward 2026 the chorus literally recedes from you.
- **Every section is set inside the opening frame.** The hero's own poster is the deep
  ground of each section, pushed to `translateZ(-620px)` and thrown far out of focus, so
  the whole page sits in the same meadow the film opens on.
- **A record with real thickness.** Twelve faces stacked in Z, a fine groove pattern, a
  warm centre label, a spindle hole, and a specular sweep that counter-rotates so the
  light reads as fixed in the room while the disc turns under it. One per section, each
  at a different size, height and tilt.
- **A readability scrim** sits between that ground and the content. Measured contrast of
  body copy over the composited background runs 6.7:1 to 15.7:1 against a 4.5:1 floor.
- **The background field is pinned to the viewport.** Each section's 3D stage is a
  `position: sticky` viewport-height layer holding ~30 dust motes at staggered
  `translateZ`. This matters: stretched over a full section (~5500px) the same field put
  one or two motes on screen at a time and read as no background at all. The sections use
  `overflow: clip` rather than `hidden`, since `hidden` would become the sticky scrollport
  and kill the pin.
- **The run-out groove is a tunnel** — six concentric rings at staggered depths flying
  past the viewer as the needle runs in.

Every transform carries its own `perspective()` so depth never depends on an ancestor's
stacking context, and the whole system is neutralised under `prefers-reduced-motion`.

## Case files

Every track flips. A **Case file** button rotates the player card 180° in 3D to reveal
the species' last known range (approximate coordinates), what killed it, when it was last
confirmed, and a "what it would have taken" line. Faces turned away from the viewer are
pulled out of the tab order, focus moves with the flip, and audio stops rather than
playing from a hidden face.

Two of those lines are the reason the section exists: the Singer Tract case file reads
*"Conservationists asked the lumber company directly. It refused."* The vaquita's reads
*"This one is not a mystery. It is enforcement."*

## Design review

Reviewed against the [ui-ux-pro-max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
guideline set. Findings it surfaced, and what changed:

| Finding | Fix |
|---|---|
| Transform performance — never animate `width` | Scroll progress bar moved to `transform: scaleX()` |
| `reduce-reflows` / 16 ms frame budget | Three independent scroll listeners collapsed into one rAF-throttled pass |
| `focus-not-obscured` (WCAG 2.2 AA) — sticky UI must not hide the focused control | `scroll-padding-top: 88px` on `html` |
| `web-target-size` (WCAG 2.2 AA) — 24×24 CSS px minimum | Mini-nav logo was 69×18 and the "Act" link 20 px wide; both now clear 24×44 |
| `image-dimension` / CLS | Hero image carries explicit `width`/`height` |
| `tap-delay` | `touch-action: manipulation` on interactive elements |
| Motion sensitivity — parallax must not be forced | Every 3D effect neutralised under `prefers-reduced-motion` |

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

- WWF *Living Planet Index* (2024) — 73% average decline in monitored wildlife populations
- Rosenberg et al., *Science* (2019) — 2.9 billion birds / ~29% decline since 1970
- Hallmann et al., *PLOS ONE* (2017) — >75% loss of flying insect biomass over 27 years
- Baiji: 2006 Yangtze survey recorded no detections; declared functionally extinct
- Rabbs' fringe-limbed treefrog: last known individual died in Atlanta, 2016
- Vaquita: ~10 remain; census is acoustic, clicks ~139 kHz (pitched down on this page)
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
