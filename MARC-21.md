MARC21 is the main metadata record file format used within institutional libraries. It is partially compatible with [[MARCXML]]. MARC21 ought to be phased out, but considering the enormous amounts of often idiosyncratic records in every single library this seems unlikely in the future.

[MARC21 specifications](https://www.loc.gov/marc/) are maintained by the Library of Congress.

"marc exchange" is apparently "[the ISO 2709 standard](https://github.com/tvirolai/marclojure)", and 
"MARC21" is apparently "[an instance of the ISO 2709 standard](https://en.wikipedia.org/wiki/ISO_2709)", and 
".mrc" is apparently a "[binary MARC file](https://librarycarpentry.org/lc-marcedit/aio/index.html)", and the examples of it in the rust crate do indeed look like marc exchange/marc 21
(whereas ".mrk" is a "[mnemonic MARC text file](https://librarycarpentry.org/lc-marcedit/aio/index.html)", which is more or less the ".mrc" version broken up into lines for ease of reading)

Conversion toolkit to/from MARCXML: https://www.loc.gov/standards/marcxml/