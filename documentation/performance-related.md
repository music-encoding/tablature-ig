# Performance-related notations

## Techniques
### Slides

Slides are to be encoded with the `<gliss>` element. The element has a tablature specific attribute `@slide` with possible values `legato` and `shift`. `@show.dirmark` indicates whether the `sl.` direction should be shown.

`@slide.to` and `@slide.from` attributes can take values `upwards` and `downwards` for slides with only one note (e.g., with only `@startid`).

### Legato techniques: hammer on & pull off 

Hammer on and pull off are notated in a similar way – a slur over notes on the same course. Additional letters (H and P respectively) may optionally indicate which is involved, but this can be deduced from the direction – `hammer on` is up the finger board, `pull off` is down.

`<slur>` indicates the set of notes covered (see guidelines option 2 for meaning 'performance technique'), using `@startid` and `@endid`. `@show.dirmark` indicates whether letters are present. For more complex cases, the element can contain `<dirMark>` subelements whose text content indicates the letters used and whose startid *must* give the first note of the gesture.


### Pitch inflection: bends and vibrato arm techniques 

Much of the core semantics of bends can be provided by `<bend>`. Currently, notes participating in a bend have explicit pitch. This is not the case in guitar tablature bends, where displacement from non-bent pitch must be specified.

Because bends can be both upwards and downwards in pitch (the latter achieved using the vibrato arm), and because both follow the same principle (pitch displacement in either upward or downward direction), we introduce the `<pitchInflection>` element.

All notes that participate in a bend (apart from the first) must have `@inflection.startid` to point to the first (pitched) note that is included in the bend gesture. Those subsequent notes must not provide differing `@tab.course` or `@tab.fret` information.

Bend displacements (`@dis`) are specified in number of semitones, and the textual content of the element indicates how the bend is specified in the source. Negative displacements indicate vibrato arm bends.

The simplest bends involve two explicit notes:
#### Two-note, whole-tone bend
```xml
    <tabGrp dur="16">
      <note tab.course="2" tab.fret="14" xml:id="note1" />
    </tabGrp>
    <tabGrp dur="16">
      <note xml:id="note2" inflection.startid="#note1"/>
    </tabGrp>
    <tie startid="#note1" endid="#note2" />
    <pitchInflection startid="#note1" endid="#note2" dis="2">Full</pitchInflection>
```
Grace-note bends can be shown with `@startid` and no `@endid`:
#### Quick, unmeasured bend
```xml
    <tabGrp dur="16">
      <note tab.course="2" tab.fret="14" xml:id="note1" />
    </tabGrp>
    <pitchInflection startid="#note1" dis="2">1</pitchInflection>
```
Prebends use another new attribute `@prebend`:
#### Simple prebend
```xml
    <tabGrp dur="16">
      <note tab.course="2" tab.fret="14" xml:id="note1" />
    </tabGrp>
    <pitchInflection startid="#note1" dis="1" prebend="true">1/2</pitchInflection>
```
A release may involve an explicit (parenthetical) repeat of the fret symbol. `@show.fret` may be provided on `<pitchInflection>`, which then refers back to the original fret symbol, or text content may be included if a different symbol is required. In the case of a multi-note bend, the notes after the first must refer to the initial note of the bend using `@pitchInflection.startid`.

#### Two-note, whole-tone bend
```xml
    <tabGrp dur="16">
      <note tab.course="2" tab.fret="14" xml:id="note1" />
    </tabGrp>
    <tabGrp dur="16">
      <note xml:id="note2" pitchInflection.startid="#note1"/>
    </tabGrp>
    <tabGrp dur="16">
      <note xml:id="note3" pitchInflection.startid="#note1"/>
    </tabGrp>
    <tie startid="#note1" endid="#note2" />
    <tie startid="#note2" endid="#note3" />
    <pitchInflection startid="#note1" endid="#note2" dis="2">Full</pitchInflection>
    <pitchInflection startid="#note2" endid="#note3" dis="0" show.fret="true" show.fret.enclose="paren"/>
```
TODO: add vibrato arm examples (downward pitch inflections)

### Miscellaneous performance techniques

#### Vibrato

We distinguish between vibrato using the left hand or the (guitar) vibrato arm. We introduce a new element `<vibrato>`, which will be a regular control event plus an extra attribute `@wide=true`. The method of generating the vibrato is specified through an attribute `@technique`, containing a semi-open list of techniques to choose from. The proposed values for this list are:

* left-hand
* vibrato-arm
* bend-neck

#### Muted/muffled strings

Strings muted with the left hand (to achieve a percussive effect) can be indicated by means of the attribute `@tab.muted`. 

### Arpeggios, trills, tremolo picking, volume swells

We can use the existing elements `<arpeg>`, `<trill>`, `<btrem>`, and `<dynam>` for arpeggios, trills, tremolo picking, and volume swells, respectively.  

#### Various 

We can use `<dir>`, which needs a new attribute `@technique`, which itself will contain a semi-open list of techniques to choose from. The proposed values for this list are:

* palm-muting
* let-ring
* tap-fing
* tap-pick
* rake
* feedback

#### TODO
* pick slide

### TODO: harmonics, various performance

## TODO Fingerings
