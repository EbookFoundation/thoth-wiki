<img src="https://punctumbooks.com/punctum/wp-content/uploads/2020/09/thoth-logo-latin.png" alt="Thoth" height="300" align="right"/>

The following wiki lists all output formats, platforms, and other stakeholders that relate to the development of [[open]] source metadata management system Thoth. Those wikis marked with an asterisk (*) are identified in the [WP5 Scoping Report](https://copim.pubpub.org/pub/wp5-scoping-report-building-open-dissemination-system/) and are indexed as an issue in the [Thoth Project](https://github.com/thoth-pub/thoth/projects).

The transfer protocols and file specifications listed in this wiki are those which have current or future support by Thoth. Any updates are welcome at wp5@copim.ac.uk.

## Data Formats

Data formats are the formats in which the textual content of an [[object]] are commonly digitally encoded. The Thoth project is agnostic as to which data format is used.

* [[AZW3]]
* [[EPUB]]
* [[HTML]]
* [[JSON]]
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
* [[MAB2]]
* [[MARC 21]]
* [[MARCXML]]*
* [[ONIX 2.1]]*
* [[ONIX 3.0]]*
* [[RDF]]
* [[XLSX]]

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

* [[Bowker]]

### Institution Identifiers
* [[Funder Registry]]*
* [[GRID]]
* [[ROR]]*

### Project Identifiers
* [[RAiD]]*

### Maker Identifiers
* [[ORCiD]]*
* [[ISNI]]*

## Libraries

### Digital Libraries

Digital libraries acquire and maintain collections of digital objects. The table below summarizes the available platforms, also providing information on their governance structure; membership fees; type of ingest; what they provide; whether they feature OA and/or non-OA content; and whether ingest happens via push (active upload by publisher) or through the exposition of the metadata of the object to a scraper.

| Name                            | Governance    | Membership Fee| In     | Out      | OA | non-OA | Ingest      |
|---------------------------------|---------------|---------------|--------|----------|----|--------|-------------|
| [[Aaaaarg.fail]]*               | Pirate        | N             | Bk     | Bk       | Y  | Y      | Push        |
| [[EBSCO ebooks]]*               | Commercial    | Y             | Bk     | Bk       | Y  | Y      | Push        |
| [[Hathi Trust Digital Library]] | Non-Profit    | ?             | Bk     | Bk       | Y  | N      | Push        |
| [[Internet Archive]]*           | Non-Profit    | N             | Bk     | Bk       | Y  | Y      | Push        |
| [[JSTOR]]*                      | Non-Profit    | Y             | Bk     | Bk/Ch    | Y  | Y      | Push        |
| [[Library Genesis]]*            | Pirate        | N             | Bk     | Bk       | Y  | Y      | Push        |
| [[Memory of the World]]*        | Pirate        | N             | Bk     | Bk       | Y  | Y      | Push        |
| [[OAPEN]]*                      | Non-Profit    | Y             | Bk     | Bk       | Y  | N      | Push        |
| [[Open Research Library]]       | Commercial    | N             | Bk     | Bk       | Y  | N      | Expose      |
| [[Project MUSE]]*               | Non-Profit    | Y             | Bk     | Bk/Ch    | Y  | Y      | Push        |


### National Libraries

* [[British Library]]*
* [[Library of Congress]]*


## Catalog Management Platforms

| Name             | Target User   | Type        | [[BibTeX]] | [[RIS]] |
| :---             | :---          | :---        | :---       | :---    |
| [[BibDesk]]      | Individual    | Open Source | [Y](https://bibdesk.sourceforge.io/manual/BibDeskHelp_16.html) | [Y](https://bibdesk.sourceforge.io/manual/BibDeskHelp_6.html) | 
| [[Bibliographix]]| Individual    | Open Source | | |
| [[Biblioscape]]  | Individual    | Commercial  | Y | Y |
| [[Bibus]]        | Individual    | Open Source | | |
| [[Citavi]]       | Individual    | Commercial  | [Y](https://www1.citavi.com/sub/manual5/en/index.html?importing_a_bibtex_file.html) | [Y](https://www1.citavi.com/sub/manual5/en/index.html?importing_a_ris_file.html)|
| [[EndNote]]      | Individual    | Commercial  | N | [Y](https://support.clarivate.com/Endnote/s/article/EndNote-Importing-RIS-files-and-associating-them-with-EndNote?language=en_US)| 
| [[Folio]]        | Institutional | Commercial  | | |
| [[Mendeley]]     | Individual    | Commercial  | [Y](https://guides.libraries.psu.edu/mendeley/add)| [Y](https://guides.libraries.psu.edu/mendeley/add)|
| [[Papers]]       | Individual    | Commercial  | [Y](https://support.papersapp.com/support/solutions/articles/30000026491-how-do-i-import-from-another-reference-manager-endnote-mendeley-zotero-refworks-reference-manager-) | Y |
| [[RefWorks]]     | Individual    | Commercial  | | [Y](https://knowledge.exlibrisgroup.com/RefWorks/Legacy_RefWorks/03Get_References/020Converting_from_Other_Bibliographic_Management_Programs) |
| [[Zotero]]*      | Individual    | Open Source | [Y](https://www.zotero.org/support/kb/importing_standardized_formats)| [Y](https://www.zotero.org/support/kb/importing_standardized_formats)|

## Metadata Aggregators

Metadata aggregators ingest metadata from publishers and expose these to libraries to aid them in the process of acquisition and collection building, as well as retailers.

| Name                            | Governance    | Membership Fee| In       | Out      | OA | non-OA | Ingest      |
|---------------------------------|---------------|---------------|----------|----------|----|--------|-------------|
| [[BDSLive]]*                    | Commercial    |               | Bk/(Ch?) | Bk/(Ch?) | Y  | Y      | Push        |
| [[DOAB]]*                       | Non-Profit    | N?            | Bk       | Bk       | Y  | N      | Push/Expose |
| [[ProQuest 360 Core]]           | Commercial    |               | Bk/(Ch?) | Bk/(Ch?) | Y  | Y      | Push        |



## Citation Indexes/Discovery Platforms

Citation Indexes and Discovery Platforms are  search engines built on top of specific publication databases tailored toward researches. 

* [[ExLibris]] (ProQuest)
* [[Google Scholar]]
* [[IEEE Xplore]]
* [[LexisNexis]]
* [[Library Hub Discover]]* (Jisc)
* [[MathSciNet]]
* [[OpenTexts.World]] 
* [[PubMed]]
* [[ScienceOpen]]
* [[SciFinder]]
* [[Scopus]] (RELX)
* [[Summon]]
* [[Web of Science]] (Clarivate)
* [[WorldCat Discovery]]* (OCLC)

The discovery platform of EBSCO is linked to its [[EBSCO ebooks]] service.

## Publishing Platforms

* [[Fulcrum]]
* [[Editoria]]

## Print Book Distributors

* [[Amazon KDP]]*
* [[Ingram Lightning Source]]



## Ebook Distributors

* [[Axiell]]
* [[Google Books]]*
* [[Google Play Books]]
* [[Open Edition Books]]
* [[OverDrive]]*
* [[RNIB Bookshare]]
* [[StreetLib]]
* [[Unglue.it]]
* [[Worldreader]]

## OER

* [[Open Textbooks]]
* [[BC Open Textbooks Collections]]
* [[OER Commons]]
* [[Orange Grove Open Textbooks]]
* [[Merlot]]

## Archiving Platforms

* [[Internet Archive – Wayback Machine]]
* [[LOCKSS]]
* [[Portico]]
* [[Zenodo]]

---

`@vincent - just leaving these here as I'm not sure where to put them [Toby]`

## OER Meta Search engines

 - Openly Available Sources Integrated Search (OASIS) - https://oasis.geneseo.edu/
 - Mason OER Metafinder - https://mom.gmu.edu/
