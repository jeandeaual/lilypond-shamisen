# Shamisen notation for LilyPond

This is a work in progress, but should be adequate for most pieces.
Contributions, bug reports, and suggestions are very welcome.

## Prerequisites

The font *IPAexGothic* is required to annotate uchi, hajiki, etc. and must be
installed and available. This is available to download from the website of the
[Information-technology Promotion Agency](https://ipafont.ipa.go.jp/node26#en)
in Japan ([ipaexg00301.zip](https://oscdl.ipa.go.jp/IPAexfont/ipaexg00301.zip))
or by installing the [fonts-ipaexfont](apt:fonts-ipaexfont) package on Ubuntu.

## Usage

The default staff size is quite small. 24 is recommended. Set this before
including `shamisen.ly`:

    #(set-global-staff-size 24)

Include shamisen support:

    \include "shamisen.ly"

Depending on your system, the default font will not support Japanese. If you
want to use Japanese in the title or metre, you will need to change it:

    \paper{
      #(define fonts
        (set-global-fonts
         #:roman "IPAexGothic"
         #:factor (/ staff-height pt 20)
        ))
    }

Create a tab staff, set the tuning, tell it to use shamisen notation, and
insert notes as usual:

    \score {
      \new TabStaff {
        \set TabStaff.stringTunings = #niagariTuning
        \shamisenNotation
        \time 2/4

        % notes

      }
    }

### Predefined tunings

- `honchoushiTuning` (C F C')
- `niagariTuning` (C G C')
- `sansagariTuning` (C F B♭')

### String selection

The default behaviour of LilyPond is to place notes on the lowest position
(i.e. the highest string) possible. This can be overridden in the normal way:

    c'\2 % play on the middle string

### Annotations

These extend the normal LilyPond annotations to add:

- `\hajiki` left-hand pluck ハ
- `\sukui` upstroke ス
- `\uchi` hammer-on ウ
- `\oshi` oshibachi/suberi ⅃
- `\keshi` mute ケ

Example:

    g \hajiki

### Fingering indications

This can be achieved in the normal way, but for convenience Roman numerals for
Ⅰ, Ⅱ, Ⅲ are defined as `\first`, `\second`, `\third` etc.:

    f16^\third

### Underlines for note lengths

These are entered as notes in the normal way:

    c4 % -> 0
    c8 % -> 0 with single underline
    c8. % -> 0 with single underline and dot
    c16 % -> 0 with double underline
    c32 % -> 0 with triple underline

### Dot rests

These are entered as rests in the normal way:

    r4 % -> dot
    r8 % -> dot with single underline
    % etc.

### 4300 phrases and similar

The `\trtr { ... }` (*t*su*r*u*t*a*r*a) function squashes the spacing of the
notes within the braces:

    \trtr { c'16\2^\third bes \hajiki g \hajiki g }

## Limitations

### Half notes

Some scores use a small square box to distinguish half notes from quarter notes.
This is not implemented.

### Tsurutara spacing

Spacing is removed from between the notes and added afterwards. Then the phrase
is the last thing in a bar, the spacing is pushed to the next bar.

## Implementation notes

Underlining of notes is implemented as a different stencil for the note stem.

The non-semitonal numbering of positions is achieved by a lookup function.

Hajiki, sukui, etc. are normal annotations, using text markup.

## Bonus

Also included is a small Ruby program that can convert a simple LilyPond-like
language based on tablature into notes, to assist in transcribing existing
works. See sakurasakura.txt for an example of how this works.
