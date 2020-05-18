## MEI Customisations for Transforming Musicology

Contains customisations of [MEI](http://music-encoding.org/home) used
in the
[Transforming Musicology](http://www.transforming-musicology.org/)
project.

Currently these comprise just:

`instruments`

Allows describing `<perfRes>` instruments in more detail. Adds some
playing technique marking elements.

`frettab`

Allows marking up of tablatures for fretted string instruments.

### Using Roma with the ODDs

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

In order
to compile these into a schema file (XSD, RNG, etc.) you need to use
the 7.17.0 release (or later) of the
[TEI stylesheets](https://github.com/TEIC/Stylesheets). The build
process goes something like:

    $ git clone https://github.com/TEIC/Roma.git
    $ ln -s Roma/roma2.sh /path/to/bin/roma   # e.g. /usr/local/bin
    $ git clone https://github.com/TEIC/Stylesheets.git tei-xsl
    $ cd tei-xsl && make
    $ git clone https://github.com/music-encoding/music-encoding.git mei
    $ roma --xsl=/path/to/tei-xsl/ --localsource=/path/to/mei/source/driver.xml /absolute/path/to/mei-tmus/schemata/mei-frettab.odd
