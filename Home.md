<img src="https://punctumbooks.com/punctum/wp-content/uploads/2020/09/thoth-logo-latin.png" alt="Thoth" height="300" align="right"/>

The following wiki lists all output formats, platforms, and other stakeholders that relate to the development of [[open]] source metadata management system Thoth. Those wikis marked with an asterisk (*) are identified in the [WP5 Scoping Report](https://copim.pubpub.org/pub/wp5-scoping-report-building-open-dissemination-system/) and are indexed as an issue in the [Thoth Project](https://github.com/thoth-pub/thoth/projects).

The transfer protocols and file specifications listed in this wiki are those which have current or future support by Thoth. Any updates are welcome at wp5@copim.ac.uk.

# Data and Metadata Formats

## Data Formats

Data formats are the formats in which the textual content of an [[object]] are commonly digitally encoded. The Thoth project is agnostic as to which data format is used.

* [[AZW3]]
* [[EPUB]]
* [[HTML]]
* [[KFX]]
* [[MOBI]]
* [[PDF]]
* [[XML]]

## Metadata Formats

Metadata formats are the formats in which the [[metadata]] of an [[object]] are stored. Metadata formats have been developed both as part of software packages or as consortial standards. Different stakeholders in the [[scholcomm pipeline]] use different metadata format for different purposes. Moreover, different stakeholders maintain different subsets of the metadata potentially contained in specific formats. Thoth aims for a holistic approach, being able to export as many formats in as many flavors as possible. 

* [[BIBFRAME 2.0]]*
* [[CreDiT]]*
* [[CSV]]*
* [[KBART]]*
* [[JSON]]
* [[MAB2]]
* [[MARC 21]]
* [[MARCXML]]*
* [[ONIX 2.1]]*
* [[ONIX 3.0]]*
* [[RDF]]
* [[XLSX]]
* [[WikiData]]

`NOTE: **SKOS**, is a W3C recommendation designed for representation of thesauri, classification schemes, taxonomies, subject-heading systems, or any other type of structured controlled vocabulary. part of the Semantic Web family of standards built upon RDF and RDFS, and its main objective is to enable easy publication and use of such vocabularies as linked data. [...] built upon RDF and RDFS, and its main objective is to enable easy publication and use of such vocabularies as linked data. (Toby added a short note to the RDF entry, not sure if this should get its own Wiki page?)`

### Citations and Bibliographies

* [[BibTeX]]*
* [[CSL]]
* [[ENL]]
* [[ENW]]
* [[RefMan]]
* [[RIS]]

## Persistent Identifiers

Persistent identifiers allow the unique identification of an [[object]] such as a book or chapter, institution, project, or [[maker]].

### Object Identifiers
* [[DOI]]
* [[ISBN]]

#### DOI Registration Agencies
* [[CrossRef]]*
* [[DataCite]]
* [[EZID]]

#### ISBN Registration Agencies

* [[Bowker]] (USA)
* [List of National Agencies](https://en.wikipedia.org/wiki/International_Standard_Book_Number#How_ISBNs_are_issued) (Wikipedia)

### Institution Identifiers

There are several databases of institution identifiers. The largest is GRID (98,598 records), which is freely downloadable. Funder Registry (21,242 records) is run by Crossref, which provides Crossref funder IDs. A community-led option is ROR, whose database is correlated with GRID, Wikidata, and ISNI.

* [[Funder Registry]]*
* [[GRID]]
* [[ISNI]]
* [[ROR]]*
* [[Wikidata]]
   * [[Scholia]]

### Project Identifiers
* [[RAiD]]*

### Maker Identifiers
* [[ORCiD]]*
* [[ISNI]]*

### Subject Identifiers
* [[BIC]]
* [[BISAG]]
* [[Bowker]]
* [[KDP]]
* [[LOC]]
* [[Thema]]

# Content Platforms and Distributors

The following categorization in **Content Platforms and Distributors** and **Catalogs and Indices** has been adapted from Michael Clarke and Laura Ricci's draft report [*OA Books Supply Chain Mapping*](https://drive.google.com/file/d/1iCu5OlT1cFDyq6r6yBC6orgjoEMJthor/view).

## Content Platforms

### Ebook Aggregators

| Name                            | Governance    | Membership    | OA | non-OA | Ingest      |
| :---                            | :---          | :---          |:---|:---    |:---         |
| [[EBSCO ebooks]]*               | Commercial    | Y             | Y  | Y      | Push        |
| [[JSTOR]]*                      | Non-Profit    | Y             | Y  | Y      | Push        |
| [[Project MUSE]]*               | Non-Profit    | Y             | Y  | Y      | Push        |
| [[ProQuest Ebook Central]]      | Commercial    | Y             | Y  | Y      | Push        |

### OA Platforms and Repositories

| Name                            | Governance    | Membership    | OA | non-OA | Ingest      |
| :---                            | :---          | :---          |:---|:---    |:---         |
| [[Érudit]]                      | Non-Profit    | ?             | Y  | Y      | ?           |
| [[Finna.fi]]                    | Non-Profit    | ?             | Y  | Y      | ?           |
| [[Hathi Trust Digital Library]] | Non-Profit    | ?             | Y  | N      | Push        |
| [[Internet Archive]]*           | Non-Profit    | N             | Y  | Y      | Push        |
| [[OAPEN]]*                      | Non-Profit    | Y             | Y  | N      | Push        |
| [[Open Bookshelf]] (DPLA)       | Non-Profit    | ?             | Y  | Y      | ?           |
| [[Open Edition]]                | Non-Profit    | ?             | Y  | Y      | ?           |
| [[Open Library]]                | Non-Profit    | Y             | Y  | Y      | Push        |
| [[Project Gutenberg]]           | Non-Profit    | N             | Y  | N      | Push        |
| [[Verdensbiblioteket]]          | Non-Profit    | N             | Y  | N      | ?        |
| [[Wikibooks]]                   | Non-Profit    | N             | Y  | N      | ?        |
| [[Wikisource]]                  | Non-Profit    | N             | Y  | N      | ?        |

### Shadow Libraries

| Name                            | Governance    | Membership    | OA | non-OA | Ingest      |
| :---                            | :---          | :---          |:---|:---    |:---         |
| [[Aaaaarg.fail]]*               | Shadow        | N             | Y  | Y      | Push        |
| [[Library Genesis]]*            | Shadow        | N             | Y  | Y      | Push        |
| [[Memory of the World]]*        | Shadow        | N             | Y  | Y      | Push        |

### National Libraries

Check teh [List of National and State Libraries](https://en.wikipedia.org/wiki/List_of_national_and_state_libraries) (Wiki)

* [[British Library]]*
* [[Library of Congress]]*
* [[National Library of France]]
* [[National Library of Germany]]
* [[National Library of Scotland]]
* [[National Library of Spain]]
* [[National Library of Sweden]]

### GLAM libraries

* [[Europeana]]
* [[Digital Public Library of America]] (DPLA)

### Consumer Ebook Platforms

* [[Google Play Books]]*
* [[Kindle]]
* [[Kobo]]
* [[Nook]]

## Ebook Distributors 

Ebook distributors differ from Digital Libraries in the sense that they do not claim to offer a scholarly function, be that to research institutions or to the general public. Distributors repackage and normalize ebook metadata. Most ebook distributors operate some form of monetization scheme, which may not be hospitable to OA books.

* [[Axiell]]
* [[Open Edition]] 
* [[Open Research Library]]
* [[OverDrive]]*
* [[RNIB Bookshare]]
* [[StreetLib]]
* [[Unglue.it]]

# Catalogs and Indices

Platforms that aggregate and host metadata, promoting discovery of particular titles. 

## Library Management Systems

Catalog management systems for individual libraries.

* [[ExLibris]] Alma (ProQuest)
* [[Folio]]
* [[Worldshare]] (OCLC)

## Knowledge Bases

Library-agnostic, global content indices.

* [[Alma's Central Knowledge Base]] (ProQuest)
* [[BDSLive]]* 
* [[ProQuest 360 Core]] 
* [[WorldCat KnowledgeBase]] (OCLC)

## Third-party Content Indices 

* [[DOAB]]*    
* [[Unpaywall]]

## DOI Registries

* [[Crossref]]

## Publication Database Search Engines

Search engines built on top of publication databases tailored toward researches. See [Jeroen Bosman's excellent Scholarly search engine comparison](https://tinyurl.com/searchenginecomparison) for useful information regarding availability of publication types, etc. See also the [recent comparative study](https://arxiv.org/abs/2005.10732) by Visser, Van Eck, and Waltman. 

* [[BASE]] (Bielefeld Academic Search Engine)
* [[Dimensions]]
* [[FatCat]] (Internet Archive)
* [[IEEE Xplore]]
* [[Internet Scholar Archive]] (Internet Archive)
* [[Lens]]
* [[LexisNexis]]
* [[Library Hub Discover]]* (Jisc)
* [[MathSciNet]]
* [[OpenAIRE Research Graph]]
* [[Open Research Knowledge graph]]
* [[OpenTexts.World]] 
* [[Orion Search]]
* [[PubMed]]
* [[ResearchGraph]]
* [[ScienceOpen]]
* [[SciFinder]]
* [[Scopus]] (RELX)
* [[S2ORC - Semantic Scholar Open Research Corpus]]
* [[Summon]] (ProQuest)
* [[Web of Science]] (Clarivate)
* [[WorldCat Discovery]]* (OCLC)

## Web-scale Search Engines

* [[Google Scholar]]
* [[Microsoft Academic]]
* [[Semantic Scholar]]

# Bibliographic Reference Management Platforms

All currently available bibliographic management platforms support import from [[BibTeX]] and [[RIS]]. Overall, these appear to be the two major formats. An excellent overview of every single platform is provided on the [OpenOffice wiki](https://wiki.openoffice.org/wiki/Bibliographic/Software_and_Standards_Information).

| Name             | Target User   | Type        | [[BibTeX]] | [[RIS]] |
| :---             | :---          | :---        | :---       | :---    |
| [[BibDesk]]      | Individual    | Open Source | [Y](https://bibdesk.sourceforge.io/manual/BibDeskHelp_16.html) | [Y](https://bibdesk.sourceforge.io/manual/BibDeskHelp_6.html) | 
| [[Bibliographix]]| Individual    | Open Source | [Y](http://mybibliographix.de/wp/datenimport/) | [Y](http://mybibliographix.de/wp/datenimport/) |
| [[Biblioscape]]  | Individual    | Commercial  | Y | Y |
| [[Bibus]]        | Individual    | Open Source | ? | ? |
| [[Citavi]]       | Individual    | Commercial  | [Y](https://www1.citavi.com/sub/manual5/en/index.html?importing_a_bibtex_file.html) | [Y](https://www1.citavi.com/sub/manual5/en/index.html?importing_a_ris_file.html)|
| [[EndNote]]      | Individual    | Commercial  | ? | [Y](https://support.clarivate.com/Endnote/s/article/EndNote-Importing-RIS-files-and-associating-them-with-EndNote?language=en_US)| 
| [[Mendeley]]     | Individual    | Commercial  | [Y](https://guides.libraries.psu.edu/mendeley/add)| [Y](https://guides.libraries.psu.edu/mendeley/add)|
| [[Papers]]       | Individual    | Commercial  | [Y](https://support.papersapp.com/support/solutions/articles/30000026491-how-do-i-import-from-another-reference-manager-endnote-mendeley-zotero-refworks-reference-manager-) | Y |
| [[RefWorks]]     | Individual    | Commercial  | ? | [Y](https://knowledge.exlibrisgroup.com/RefWorks/Legacy_RefWorks/03Get_References/020Converting_from_Other_Bibliographic_Management_Programs) |
| [[Zotero]]*      | Individual    | Open Source | [Y](https://www.zotero.org/support/kb/importing_standardized_formats)| [Y](https://www.zotero.org/support/kb/importing_standardized_formats)|



# Publishing Platforms

Publishing platforms allow authors, editors, and publishers to collaborate in a digital, in-browser environment, with a potential to radically transform publishing production pipelines.

* [[Fulcrum]]
* [[Editoria]]

# Print Book Distributors

There are basically only two main print book distributors available to OA publishers who wish to use print-on-demand for their hardcopy publications, [[Amazon KDP]] and [[Ingram Lightning Source]]. Both require the manual input of metadata upload of print-ready PDF files without apparent batch or automated upload options. 

# OER

Open Educational Resources (OER) focus mainly on textbooks rather than scholarly publications. 

## Digital OER Libraries

| Name                            | Governance    | Membership    | OA | non-OA | Ingest      |
| :---                            | :---          | :---          |:---|:---    |:---         |
| [[BCcampus OpenEd]]             | Public        | N             | Y  | N      | Push |
| [[Merlot]]                      | Public        | Y             | Y  | N      | Push | 
| [[OER Commons]]                 | Non-Profit    | Y             | Y  | N      | Push |
| [[Open Textbook Library]]       | Non-Profit    | N             | Y  | N      | Push | 

## OER Citation Indexes/Discovery Platforms

* [[OASIS]]
* [[Mason OER Metafinder]]
* [[OERWorldmap]]

# Archiving Platforms

* [[Internet Archive – Wayback Machine]]
* [[LOCKSS]] & [[CLOCKSS]]
* [[Portico]]
* [[Zenodo]]
