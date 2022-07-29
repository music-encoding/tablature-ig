## Tablature Interest Group repository

Contains example materials, draft documentation and MEI customisations to support the work of the Interest Group.

The aim of the Interest Group is to develop MEI for the encoding of repertories that use tablature notations. This involves making recommendations for extension, addition and amendment to future versions of the MEI schema and guidelines, and supporting the development of software tools to process MEI containing tablature. We ultimately aim to include as many tablature forms as possible, but are initially focussing on those for the guitar and lute family of instruments.

### Examples

Examples have been chosen to test a broad range of the notation types that are currently 'in scope'. Images of the original sources used are accompanied by sample encodings.

### Documentation

Documentation covers areas discussed in IG meetings. It is not yet complete or stable.

### Schemata

Contains ODD customisations of the MEI schema for our recommendations. 
Originally, these were customisations from previous work on this as part of the [Transforming Musicology](https://github.com/TransformingMusicology) project.

Comprising of:

`instruments`

Allows describing `<perfRes>` instruments in more detail. Adds some
playing technique marking elements.

`frettab`

Allows marking up of tablatures for fretted string instruments.

#### Using Roma with the ODDs

The customisations are contained in two ODD files (plus one container
ODD file, `mei-frettab.odd`, that pulls in all of MEI plus the two new
modules). The `mei-frettab.odd` uses `<specGrpRef>` elements to
reference the two ODD files. The Roma tool requires that the `@target`
attribute of `<specGrpRef>` be an absolute URI so in the version
included in this repository the two elements use unresolvable
URIs. Before building you need to edit the `@target` attribute values
changing them to the absolute paths to the two files. E.g.:

    <specGrpRef target="file:///path/to/tmus-mei/schemata/instruments.odd#instruments" />
    <specGrpRef target="file:///path/to/tmus-mei/schemata/frettab.odd#frettab" />

In order to compile these into a schema file (XSD, RNG, etc.) you need to use
the 7.17.0 release (or later) of the
[TEI stylesheets](https://github.com/TEIC/Stylesheets).

Roma uses saxon, an XSLT processor, which must be installed, version >= 10.
[Saxon](http://saxon.sourceforge.net/).

Saxon does not handle XIncludes, one solution is to use xmllint as a preprocessor.  Other solutions are
discussed here [DocBook XSL](http://www.sagehill.net/docbookxsl/Xinclude.html).

The build process goes something like:

    $ git clone https://github.com/TEIC/Roma.git
    $ ln -s Roma/roma2.sh /path/to/bin/roma   # e.g. /usr/local/bin
    $
    $ git clone https://github.com/TEIC/Stylesheets.git tei-xsl
    $ cd tei-xsl
    $ make
    $ cd ..
    $
    $ git clone https://github.com/music-encoding/music-encoding.git mei
    $ # to specify version, e.g. v4.0.1, otherwise defaults to latest development version
    $ cd mei
    $ git checkout v4.0.1
    $ cd ..
    $
    $ xmllint --xinclude -o /path/to/mei/mei-source.xml /path/to/mei/source/mei-source-included.xml
    $ roma --xsl=/path/to/tei-xsl/ --localsource=/path/to/mei/source/mei-source-included.xml /absolute/path/to/mei-tmus/schemata/mei-frettab.odd

