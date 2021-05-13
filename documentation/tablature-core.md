# Tablature documentation
*EARLY DRAFT*
 * [Tuning and instrumental setup](#Tuning-and-instrumental-setup)
 * [Tablature types](#Tablature-types)
 * [Notes](#Notes)
   * [Fret/Course symbols](#Fret/course-symbols)
   * [Rhythm flags for lute tablatures](#Rhythm-flags-for-lute-tablatures)
## Tuning and instrumental setup
Guitar-like instruments can be described in terms of the number of
strings they have, but often the strings are grouped and notated as if those
groups were a single string. Examples include mandolins and 12-string guitars.
To make this distinction explicit, we use the *string* exclusively to refer to
physical strings. To refer to the notated version, which may consist of one or
more physical strings, we use the historical term, "*course*". Thus, both a
6-string and a 12-string guitar are 6-course instruments.

The course tuning for 6- and 12-string guitars are the same – so they can both
play from the same tablatures. Our tuning specification supports indicating
course tunings on their own, or string tunings as well.

In the simplest cases, the tuning can be named from a controlled list of tuning
types.
```xml
<tuning tuning.standard="guitar.drop.D"/>
```
or
```xml
<tuning tuning.standard="lute.renaissance.6"/>
```
If individual course tunings are to be named, `<tuning>` can take multiple
`<course>` elements as children. For example, a standard classical guitar
tuning could be specified like this:
```xml
<tuning>
  <course n="1" pname="e" oct="4"/>
  <course n="2" pname="b" oct="3"/>
  <course n="3" pname="g" oct="3"/>
  <course n="4" pname="d" oct="3"/>
  <course n="5" pname="a" oct="2"/>
  <course n="6" pname="e" oct="2"/>
</tuning>
```
Where the specific instrumental setup is important, the stringing of the
instrument can also be specified. The example is a common way to string
and tune a 6-course renaissance lute. The `course` pitch indicates how the
resulting note would normally be transcribed in score, and would often be
derived from the lowest sounding pitch.
```xml
<tuning>
  <course n="1" pname="g" oct="4">
    <string pname="g" oct="4"/>
  </course>
  <course n="2" pname="d" oct="4">
    <string pname="d" oct="4"/>
  </course>
  <course n="3" pname="a" oct="4">
    <string pname="a" oct="4"/>
    <string pname="a" oct="4"/>
  </course>
  <course n="4" pname="f" oct="3">
    <string pname="f" oct="3"/>
    <string pname="f" oct="4"/>
  </course>
  <course n="5" pname="c" oct="3">
    <string pname="c" oct="4"/>
    <string pname="c" oct="3"/>
  </course>
  <course n="6" pname="g" oct="2">
    <string pname="g" oct="3"/>
    <string pname="g" oct="2"/>
  </course>
</tuning>
```
In the (rare) cases where strings are indicated as being sounded separately
within a course, `@n` may be used on `<string>` to allow them to be
disambiguated.

The tuning declaration should be placed in the `<staffDef>` element.

## Tablature types
`@notationtype` in `<staffDef>` is used to specify the tablature type.
Permitted values are:
 * tab.lute.french
   * letters for frets
   * courses closest to the ground when playing are at the top of the stave
 * tab.lute.italian
   * numbers for frets
   * courses closest to the ground when playing are at the bottom of the stave
 * tab.lute.german
   * No staff lines, although vertical position may imply voicing
   * Symbols (based on letters) for combinations of fret *and* course
 * tab.guitar
   * numbers for frets
   * courses closest to the ground when playing are at the top of the stave

Organ and other instrumental tablatures would be expected to be added
as needed. The names ‘lute’ and ‘guitar’ in these are the names of the
notation, not the instrument – other instruments also use these notations.

**This replaces the existing `tab` value for this attribute (which
would probably map to `tab.guitar` here).**

A `<staffDef>` with both tuning and tablature type specified could look like this:
```xml
<staffDef lines="6" notationtype="tab.lute.italian">
  <tuning tuning.standard="lute.renaissance.6"/>
</staffDef>
```

## Notes
The primary rhythm and pitch information in guitar and lute tablature
is contained in vertically-aligned stacks of symbols. The main
components of these stacks are rhythm symbols, which indicate the inter-onset time between the current and the next stack, and fret/course symbols
which indicate what, if anything, should be sounded.

In ASCII tab, rhythmic indications are usually omitted. In lute
tablature, one rhythmic indicator or no rhythmic indicator (indicating that the duration is the same as that of the last rhythm indicator shown) can appear in each stack.
Some guitar tablatures support multiple rhythm signs.

We use `<tabGrp>` to indicate such a stack. It is chord-like in
behaviour, and normally takes `@dur.ges` to indicate what the
effective (minimum) duration of that stack is (that is, the inter-onset interval between this and the next stack, not the duration of members of the chord).

### Fret/course symbols
A `<note>` in lute and guitar tablature indicates (by different
means) the fret and course being sounded. From this, and given a
tuning, pitch can be calculated. We use `@tab.fret` and
`@tab.course` to indicate this information:
```xml
<note tab.course="2" tab.fret="3"/>
```
In normal cases, this will be enough, given the `@notationtype`. On
occasions where the symbol is not the expected one, it can be indicated using
the new element `<fretGlyph>`. Likely examples of this might be variant
German notation symbols or alternatives for frets above 9 in Italian tabs.

```xml
<note tab.course="6" tab.fret="0">
  <fretGlyph symbol="1" symbol.mod="strikethrough"/>
</note>
```

### Rhythm flags for lute tablatures
In lute tablatures, a rhythm indication may be present or absent in any
given `<tabGrp>`. This can be reflected using the `<tabDurSym>` element:
```xml
<tabGrp dur.ges="4">
  <tabDurSym/>
  <note tab.course="2" tab.fret="3">
  <note tab.course="3" tab.fret="0">
  <note tab.course="5" tab.fret="2">
</tabGrp>
```

Where the rhythm sign is absent, it is usually played as if
the previous indication had been repeated. Where there is no preceding
indication or the music requires a different interpretation of rhythm,
editorial markup should be used to add a tabDurSym (replaces **tabRhythm**).

Where a `<tabDurSym>` is the only element of `<tabGrp>`, the result has the
same effect as a rest in CMN.

Given the presence of a rhythm symbol, the form can be inferred from `@dur` or
`@dur.ges` (*which?*) on `<tabGrp>`. Where the editor wishes to specify the
form of the rhythm symbol, the following attributes can be used on `<tabDurSym>`:

att | description
---|---
 `symbol` | The duration symbol.
`head` | Indicates whether the rhythm sign has a note head and if so, what shape.
`flags` | The number of flags on the rhythm sign.
`flagDir` | Indicates the direction of the rhythm sign's flag(s) (used for *sesquialtera*). Legal values: left, Left pointing, right, Right pointing
`serif` | Indicates that the rhythm sign has a serif (short flag)
`serifDir` | Indicates the direction of the rhythm sign's serif when `@serif` is `true` Legal values: left, Left pointing, right, Right pointing,
`dots` | The number of dots on the rhythm sign (as in `<note>` in cmn)
