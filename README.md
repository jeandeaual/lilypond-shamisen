# Shamisen notation for LilyPond

This is a work in progress, but should be adequate for most pieces.

## Features

* underlining of 8th. 16th, 32nd notes
* kana annotations for `\hajiki`, `\sukui`, `\uchi`
* fingering indications `^\first`, `^\second`, `^\third`
* dot rests (with underlines)
* predefined tunings:
  - `honchoushiTuning` (c f c')
  - `niagariTuning` (c g c')
  - `sansagariTuning` (c f bf')

## Missing

* half-note length indicators - these can probably be inferred from the bar length

## Implementation notes

Underlining of notes is implemented as a different stencil for the note stem.

The non-semitonal numbering of positions is achieved by a lookup function.

Hajiki, sukui, and uchi are normal annotations, using text markup.

## Bonus

Also included is a small Ruby program that can convert a simple LilyPond-like
language based on tablature into notes, to assist in transcribing existing
works. See sakurasakura.txt for an example of how this works.
