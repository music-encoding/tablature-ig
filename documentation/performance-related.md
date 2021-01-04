# Performance-related notations

## Slides
Slides are techniques in which notes are sounded by means of a position change (i.e., moving the LH up or down the fretboard). There are four main types of slide:
* Legato slide: given two notes on the same string, the target note is sounded by moving the LH finger from the position of the start note, once that has been sounded, to the position of the target note without releasing pressure on the string and without picking/plucking that target note. It is notated by means of a diagonal line (upward or downward, depending on the slide direction) between the notes involved, combined with a slur over them; the abbreviation 'sl.' may be used to indicate the slide. The legato slide has a defined start and target note.
* Shift slide (portamento): similar to the legato slide, the main difference being that the target note now _is_ picked/plucked. It is notated by means of a diagonal line (upward or downward, depending on the slide direction) between the notes involved; the abbreviation 'sl.' may be used to indicate the slide. The potamento slide has a defined start and target note.
* Slide-to: a single-note slide where the note is the target note; there is no defined start of the slide, and the length of the slide is interpreted. It is notated by means of a diagonal line (or a grace note with a legato slide) to the left of the note. The direction of the diagonal line determines whether to slide from below (ascending) or from above (descending).
* Slide-from: a single-note slide where the note is the start note; there is no defined target of the slide, and the length of the slide is interpreted. It is notated by means of a diagonal line to the right of the note. The direction of the diagonal line determines whether to slide up (ascending) or down (descending).

### Elements and attributes
* Slides are to be encoded using the existing `<gliss>`. 
* `<gliss>` has a tablature-specific attribute `@slide`, with possible values 'legato' and 'shift'.
* `@startid` and `@endid` are used to indicate the start and target note.
* Both the slide-to and the slide-from have no `@endid`.
* In case of a slide-to or slide-from, `@slide.to` and `@slide.from` can take values 'upwards' and downwards' to indicate the slide direction.
* @show.dirmark indicates whether the 'sl.' abbreviation is shown.

### Examples:
* Legato slide/shift slide
```xml
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='12' xml:id='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='14' xml:id='n_2'/>`
`</tabGrp>` 
`<gliss startid='n_1' endid='n_2' slide='legato' show.dirmark='true'/>` (use `@slide=shift'` for shift slide)
```

* Slide-to
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='12' xml:id='n_1'/>`
`</tabGrp>`
`<gliss startid='n_1' slide.to='upwards' show.dirmark='true'/>` (slide from below; use `@slide.to='downwards'` for slide from above)

* Slide-from
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='12' xml:id='n_1'/>`
`</tabGrp>`
`<gliss startid='n_1' slide.from='upwards' show.dirmark='true'/>` (slide up; use `@slide.from='downwards'` for slide down)

## Legato techniques: hammer-on, pull-off, and tap
Legato techniques are techniques in which a note is sounded without picking/plucking it. There are two main types of legato techniques:
* Hammer-on: given two notes on the same string, the second note is sounded by 'hammering' a LH finger onto the fretboard. It is notated by means of a slur over the notes involved; the letter 'H' may be used to indicate the hammer-on, but this can be deduced from the direction (up the fretboard). A special case is the single-note hammer-on (sometimes also called 'left-hand tap'): a single note is sounded by hammering a LH finger directly onto the fretboard.
* Pull-off: given two notes on the same string, the second the note is sounded by 'pulling' a LH finger off the fretboard. It is notated by means of a slur over the notes involved; the letter 'P' may be used to indicate the pull-off, but this can be deduced from the direction (down the fretboard).

Strictly speaking, the tap is not a legato technique (it applies to a single note), but since it is commonly included in legato slurs, it should be mentioned here. More on the tap is found under Ornaments and effects below.
* Tap: the note is sounded by hammering a RH finger onto the fretboard. It is generally notated by means of the letter 'T' over the note involved. The tapped note is often the first note of a pull-off.

Hammer-ons, pull-offs, or a mix of them are often combined into longer 'slurs', of which only the first note is picked/plucked. Taps, as well as legato slides, are frequently included into these.

### Elements and attributes
* Slides are to be encoded using `<slur>`, which indicates the set of notes covered (see guidelines option 2 for meaning 'performance technique'). TODO what does the thing between parentheses mean?
* `@startid` and `@endid` are used to indicate the first and final note of the slur.
* A single-note hammer-on has no `@endid`.
* `@show.dirmark` indicates whether the letters 'H' and 'P' are shown. For more complex cases, the element can contain `<dirMark>` subelements whose text content indicates the letters used, and whose startid *must* give the first note of the gesture.
* Taps are encoded using `<dir>` with `@technique='tap-fing'` (or `@technique='tap-pick'` when using the pick to tap); by means of a textual value, the symbol to display (generally 'T') can be decided. See Ornaments and effects below.

### Examples
* Hammer-on/pull-off (for pull-of, reverse `n_1` and `n_2`) 
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='12' xml:id='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='14' xml:id='n_2'/>`
`</tabGrp>`
`<slur startid='n_1' endid='n_2' show.dirmark='true'/>`

* Single-note hammer-on
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='12' xml:id='n_1'/>`
`</tabGrp>`
`<slur startid='n_1' show.dirmark='true'/>`

* Slur combining hammer-on, pull-off, legato slide, and tap.
`<tabGrp dur='16'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='12' xml:id='n_1'/>`
`</tabGrp>`
`<tabGrp dur='16'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='14' xml:id='n_2'/>`
`</tabGrp>`
`<tabGrp dur='16'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='15' xml:id='n_3'/>`
`</tabGrp>`
`<tabGrp dur='16'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='17' xml:id='n_4'/>`
`</tabGrp>`
`<tabGrp dur='16'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='15' xml:id='n_5'/>`
`</tabGrp>`
`<tabGrp dur='16'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='14' xml:id='n_6'/>`
`</tabGrp>`
`<tabGrp dur='16'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note tab.course='3' tab.fret='12' xml:id='n_7'/>`
`</tabGrp>`
`<slur startid='n_1' endid='n_7' show.dirmark='true'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<gliss startid='n_2' endid='n_3' slide='legato' show.dirmark='true'/>`
&nbsp;&nbsp;&nbsp;&nbsp;`<dir technique='tap-fing' startid='n_4'>T</dir>`
&nbsp;&nbsp;&nbsp;&nbsp;`<gliss startid='n_5' endid='n_6' slide='legato' show.dirmark='true'/>`
`</slur>`

## Pitch inflection: bends
Bends raise the pitch; the target pitch lies above the start (notated) pitch. The pitch displacement is measured in semitones ('1' for a semitone, '2' (or 'Full') for a whole tone, '0.5' for a quarter tone, etc.). Bends may consist of up to three components:
* Bend: the note is lowered to the target pitch. A bend is rendered as an upward arrow with the pitch displacement written above it; its shape depends on the type of bend. There are three types of bend:
    * Bend: gradual, i.e., has a notated duration.    
    * Unmeasured (grace note) bend: almost immediate, i.e., has no notated duration (other than the grace note).
    * Pre-bend: immediate, i.e., the note is bent before it is picked/plucked.
* Hold: the note is held at the target pitch, and may be picked/plucked again. During a hold, other techniques (e.g., vibrato, tapping, bending, ...) may be applied. A hold is rendered as a dashed line to the right of the bend arrow head.
* Release: the note is released to the start pitch, and may be picked/plucked again. A release is rendered as a downward arrow (with the pitch displacement written above it only if the start pitch is not reached by that displacement); its shape depends on the type of release. There are three types of release:
    * Release (cf. bend): gradual, i.e., has a notated duration.
    * Unmeasured (grace note) release (cf. unmeasured bend): almost immediate, i.e., has no notated duration (other than the grace note).
    * Pre-release (cf. pre-bend): immediate, i.e., the note is released at the target pitch.

It must be noted that:
* A hold is inferred and needs not be specified. A hold is only rendered if the held note is not followed by a pre-release, i.e., if the held note is not the last note in the bend gesture. 
* A release only needs to be specified if it is not a pre-release, i.e., if it is not immediate. 
* All of the above can be applied to a unison bend: a bend where two notes are picked/plucked simultaneously: the start note (i.e., the note that is bent), and (on the adjacent higher string) a note that has the same pitch as the target note.

In total, there are four basic combinations (where a bend can be a bend, an unmeasured bend, or a pre-bend; and a release can be a release or an unmeasured release):

* Bend and pre-release. 
* Bend, hold, and pre-release -- NB: in order for this to differ from bend and pre-release, the held note must be repeated at least once.
* Bend and release. 
* Bend, hold, and release. 

### Elements and attributes
* Much of the core semantics of bends can be provided by `<bend>`. Currently, notes participating in a bend have explicit pitch. This is not the case in guitar tablature bends, where displacement from non-bent pitch must be specified. Because bends can be both upwards and downwards in pitch (the latter achieved using the vibrato arm, and called 'dives' -- see below), and because both follow the same principle (pitch displacement in either upward or downward direction), the <pitchInflection> element is introduced.
* Unmeasured bends, prebends, and unmeasured releases have no `@endid` on `<pitchInflection>`. Similarly, in the CMN above the tablature staff, unmeasured bends, prebends, and unmeasured releases are always specified over a single note, while bends and releases are always specified over two notes. 
* Prebends use `@prebend='true'` on `<pitchInflection>`.
* The pitch displacement is encoded using `@dis` on `<pitchInflection>`, and is specified in number of semitones; the textual content of the attribute indicates how the bend is specified in the source (`Full`, `1/2`, `1 1/2`, etc.). A release is indicated by `@dis='0'`. Negative values for the displacement indicate a vibrato arm dive.  
* All notes but the first in a bend gesture: 
    * Must have a `@pitchInflection.startid` on `<note>` to point to the first (pitched) note in the bend gesture.
    * Must not provide differing `@tab.course` or `@tab.fret` information on `<note>` -- and, in fact, may leave this out altogether if the note is not re-picked/plucked (which is implied by `@tie`). If the note is re-picked/plucked, this information must be provided.
* Multi-note bends may involve an explicit (parenthetical) repeat of the fret symbol, e.g., if the note in question is the first after a barline, or if another technique (e.g., vibrato) is applied from that point. This is encoded using `@show.fret='true'` (and `@show.fret.enclose='paren'`) on `<pitchInflection>`; the former refers back to the original fret symbol of the first note in the bend gesture. Alternatively, textual content may be included if a different symbol is required. 

### Examples
#### Bend and pre-release
* Bend (ex. 1)
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' endid='n_2 dis='2'>Full</pitchInflection>`
* Unmeasured bend (ex. 2a)/pre-bend (ex. 3)
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' dis='1'>1/2</pitchInflection>` (add `@prebend='true'` in case of pre-bend)
* Unmeasured bend, crossing bar (2b)
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' dis='1' show.fret='true' show.fret.enclose='paren'>1/2</pitchInflection>` TODO: `@show.fret` and `@show.fret.enclose` apply to `n_2`, which is not in this `<pitchInflection>`. Is this clear anyway? 

#### Bend, hold, and pre-release
* Bend (ex. 4)
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_3' tab.course='3' tab.fret='12' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' endid='n_2 dis='2'>Full</pitchInflection>`
* Unmeasured bend (ex. 5)/pre-bend (ex. 6)
`<tabGrp dur='4' dots='1'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tab.course='3' tab.fret='12' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' dis='2'>Full</pitchInflection>` (add `@prebend='true'` in case of pre-bend)

#### Bend and release
* Bend and release (ex. 7)
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='m' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_3' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' endid='n_2' dis='2'>Full</pitchInflection>`
`<pitchInflection startid='n_2' endid='n_3' dis='0'/>`
* Bend and unmeasured release (ex. 8)
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' endid='n_2' dis='2'>Full</pitchInflection>`
`<pitchInflection startid='n_2' dis='0'/>`
* Unmeasured bend and release (ex. 9)/pre-bend and release (ex. 11)
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' dis='2'>Full</pitchInflection>` (add `@prebend='true'` in case of pre-bend)
`<pitchInflection startid='n_1' endid='n_2' dis='0'/>`
* Unmeasured bend and unmeasured release (ex. 10)/pre-bend and unmeasured release (ex. 12)
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' dis='2'>Full</pitchInflection>` (add `@prebend='true'` in case of pre-bend)
`<pitchInflection startid='n_2' dis='0'/>` 

#### Bend, hold, and release
* Bend, hold, and release (ex. 13)
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='m' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_3' tie='m' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_4' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' endid='n_2' dis='2'>Full</pitchInflection>`
`<pitchInflection startid='n_3' endid='n_4' dis='0'/>`

* Bend, hold, and unmeasured release (ex. 14)
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='m' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_3' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' endid='n_2' dis='2'>Full</pitchInflection>`
`<pitchInflection startid='n_3' dis='0'/>`

* Unmeasured bend, hold, and release (ex. 15)/pre-bend, hold, and release (ex. 17)
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='m' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_3' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' dis='2'>Full</pitchInflection>` (add `@prebend='true'` in case of pre-bend)
`<pitchInflection startid='n_2' endid='n_3' dis='0'/>`

* Unmeasured bend, hold, and unmeasured release (ex. 16)/pre-bend, hold, and unmeasured release (ex. 18)
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='4'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' dis='2'>Full</pitchInflection>` (add `@prebend='true'` in case of pre-bend)
`<pitchInflection startid='n_2' dis='0'/>`

## Pitch inflection: vibrato bar dives
Vibrato bar dives lower the pitch by depressing the vibrato bar; the target pitch lies below the start (notated) pitch. The pitch displacement is measured in semitones ('1' for a semitone, '2' (_not_ 'Full'!) for a whole tone, '0.5' for a quarter tone, etc.). Vibrato bar dives may consist of up to three components, and, as they are essentially the opposite of bends, can be deconstructed similar to them (as shown above). There are a few minor differences:
* The three components are called now _dive_, _hold_, and _release_, where the three types of dive are called _dive_, _unmeasured dive_, and _pre-dive_.
* A dive is rendered as a downward diagonal line with the pitch displacement written above it; its shape (slope) depends on the type of dive.
* A release is rendered as an upward diagonal line (with the pitch displacement written above it only if the start pitch is not reached by that displacement); its shape (slope) depends on the type of release.
* There is a special `@dis` value to indicate that the vibrato bar is depressed so far that the strings are rendered slack: `slack`.
* There can be no defined target pitch for a dive (cf. slide-from above); also, there can be no defined start pitch for a pre-dive (cf. slide-to). In these cases, no pitch displacement is provided.

Again, it must be noted that:
* A hold is inferred and needs not be specified. A hold is only rendered if the held note is not followed by a pre-release, i.e., if the held note is not the last note in the bend gesture. 
* A release only needs to be specified if it is not a pre-release, i.e., if it is not immediate.

And also that:
* Usage beyond dive (+ hold) (+ return) is fairly rare; common combinations are:
    * Scoop: a pre-dive followed by an unmeasured release (the bar is depressed before the note is picked, the note is picked, and the bar is then returned almost immediately). A scoop is sometimes indicated with a slur-like symbol to the left of the note; usually no pitch displacement is provided.
    * Dip: an unmeasured dive + unmeasured release (the bar is depressed almost immediately and returned almost immediately); this can be applied at the time of or after picking the note. A dip is indicated with an inverted V shape (the downward and upward diagonal lines going with the unmeasured dive and release, connected at the bottom) above the note, with the pitch displacement written above it.
    * Vibrato (indicated by 'w/ bar').
* Sometimes, the vibrato bar is used to raise the pitch -- this technique can be seen as an emulation of a bend.

The same four basic combinations as listed for bends above apply for vibrato dives. 

### Elements and attributes
The points on elements and attributes, as also listed for bends above, apply for vibrato bar dives. Additionally, to make the distinction with a bend more clear (apart from the negative value for `@dis`), `@vibrato-bar='true'` is added to `<pitchInflection>`. TODO attribute name

### Examples
* Dive, hold, and release (ex. 19)
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_1' tab.course='3' tab.fret='12' tie='i'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_2' tie='m' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_3' tie='m' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<tabGrp dur='8'>`
&nbsp;&nbsp;&nbsp;&nbsp;`<note xml:id='n_4' tie='t' pitchInflection.startid='n_1'/>`
`</tabGrp>`
`<pitchInflection startid='n_1' endid='n_2' dis='-2' vibrato-bar='true'>Full</pitchInflection>`
`<pitchInflection startid='n_3' endid='n_4' dis='0' vibrato-bar='true'/>`

## Miscellaneous performance techniques
### Harmonics
#### Natural harmonic
TODO

#### Artificial harmonic
TODO

#### Tap harmonic
TODO

#### Harp harmonic
TODO

### Ornamental and effect techniques
A fair share of these techniques can be encoded using existing elements (and attributes), but for some, new ones are introduced.

#### Vibrato
A new element `<vibrato>` is introduced, which will be a regular control event, and which can have an attribute `@wide`, to be set to `true` in case of a wide vibrato. A distinction can be made between vibrato using the left hand or using the vibrato bar. The method of generating the vibrato is specified through an attribute `@technique`, for which there is a semi-open list of techniques to choose from. The proposed values for this list are:
* `left-hand`
* `vibrato-bar`
* `bend-neck`

#### Pick slide
Pick slides, where the edge of the pick is slid across one of the wound strings to create a non-pitched, scraping effect (indicated with an X in the tablature, as for muted/muffled strings), are a special form of slide-froms, and can therefore be encoded using the existing element `<gliss>`. A pick slide requires the addition of the attribute `@pick-slide='true'` on `<gliss>`.

#### Palm muting, let ring, tap, rake, feedback
These techniques can be specified by means of the existing element `<dir>`, on which an attribute `@technique`, which itself contains a semi-open list of the techniques to choose from, is used. The proposed values for this list are:
* `palm-muting`
* `let-ring`
* `tap-fing`
* `tap-pick`
* `rake`
* `feedback`

#### Arpeggio, trill, tremolo picking, volume swell
For these techniques, the existing elements `<arpeg>`, `<trill>`, `<btrem>`, and `<dynam>`, respectively, are used.

#### Muted/muffled strings
The attribute `@tab.muted`, to be placed on `<note>`, is introduced to indicate strings muted with the left hand (to achieve a percussive effect).

## Fingerings and performance instructions
### Left hand
* Fingering
* Bar (barré)

### Right hand
* Fingering
* Downstroke
* Upstroke

### Miscellaneous (shorthand) notation
* Rhythm slashes
* Rhythm slashes (single notes)
* Chord names