A Work is a unit of publication with at least one unique identifier.

The **Works** page will display the Works the current user has access to. The following information is displayed:

| Column Name  | Content      |
| :---         | :---          | 
| ID           | Unique primary key ([[UUID]])    | 
| Title      | [Title](#title-mandatory) |
| Type    | [Type](#work-type-mandatory) |
| Contributors  | List of comma-separated contributors|
| DOI | [DOI](#doi) |
| Publisher | [Publisher](#imprint-mandatory) |
| UpdatedAt | Date/time of most recent update |

Clicking on any record allows you to edit it. Save the record by clicking **Save**.

# Work Type (Mandatory)

Select the type of the work from the dropdown list:
* Book Chapter
* Monograph
* Edited Book
* Textbook
* Journal Issue
* Book Set

Not all fields are available for all Work Types. Non-available fields are greyed out.

# Work Status (Mandatory)

Select the status of the work from the dropdown list:
* Unspecified
* Cancelled
* Forthcoming
* Postponed Indefinitely
* Active
* No Longer Our Product
* Out of Stock Indefinitely
* Out of Print
* Inactive
* Unknown
* Remaindered
* Withdrawn from Sale
* Recalled

# Imprint (Mandatory)

Select the [[Imprint|Thoth_Imprints]] from the dropdown list.

## Title (Mandatory)

The title of the Work.

## Subtitle

The subtitle of the Work.

## Edition
> An edition of a particular work usually encompasses all copies of the work that contain the same content, and (most often) which have been produced by the same publisher. Publisher identification of a specified or distinct edition may be due to changes in content (addition, revision, or removal of content) or may identify products produced for a specific market. It is important to note that some editions, such as second, abridged, or annotated editions, may be new works entirely; others may contain the same content but be classified as a different edition, such as a large print edition. 

(BISG, _Revised Best Practices for Book Metadata_, 93)

👀 Numbered editions: Please use "1" for the initial edition of a Work, even if subsequent editions are not planned.
**Named editions: [ONIX list 21?]**

## Publication Date

The date of publication in the format `dd/mm/yyyy`.

## Place of Publication

The place of publication. 

## Cover URL

URL of the cover image.

## Cover Caption

Caption referring to the cover image.

## DOI

[[Digital Object Identifier|DOI]] of the Work. 

## LCCN

The [[Library of Congress Control Number|LCCN]] of the Work. _Only provide this if you already happen to have the information at hand. Not a requirement. Relevant primarily for US publishers._

## OCLC Number

The [[OCLC Number]] of the Work. _Only provide this if you already happen to have the information at hand. Not a requirement. Relevant primarily for US publishers._

## Internal Reference

A reference to the Work used by the Publisher internally.

## Page Count

Total number of pages. In most cases, unnumbered pages (e.g., endpapers) should be omitted from this count. (Unnumbered pages that are part of plate sections/inserts are part of the book’s content and should be counted.) Books that have pages numbered in both roman and Arabic numerals (and no inserts) should have a Page Count that reflects the sum of the highest number of the roman-numbered pages plus the highest number of the Arabic-numbered pages. _This value_ is therefore **not necessarily** the total number of pages bound into the book – there may for example be blank leaves at the back_. The sole exception to this is the case of a book with no numbered pages; in such a case the value given for Page Count should be the total number of all pages in the book.

For multi-volume books sold under a single Product Identifier, enter the total for all the volumes combined in the product record for the multi-volume product. If the individual volumes are sold separately, each of their product records should carry a Page Count for only the volume in question. 

**Example**

> Using _The Chicago Manual of Style_, 14th edition as an example, one sees that the front matter is numbered in roman numerals up to page ix. The main body of the work has pages numbered in Arabic numerals up to page 921. The book also contains five unnumbered pages at its end and both a front and a back flyleaf. For the purposes of these best practices guidelines, the Page Count sent out for this book should be 930 (the sum of the highest number of the roman-numbered pages, 9, plus the highest number of the Arabic-numbered pages, 921). 

(BISG, _Revised Best Practices for Book Metadata_, 104)


## Page Breakdown

Breakdown of **Total number of pages** in frontmatter, main, and backmatter.

## First Page

Only relevant for the Work type **Book Chapter**: First page of the chapter.

## Last Page

Only relevant for the Work type **Book Chapter**: Last page of the chapter.

## Image Count

Total number of images.

## Table Count

Total number of tables.

## Audio Count

Total number of audio fragments.

## Video Count

Total number of video fragments.

## License (Mandatory)

URL of the pertinent [[Creative Commons]] license.

## Copyright Holder (Mandatory)

Copyright holder of the work.

## Landing Page

URL of the web page of the work.

## Long Abstract

Abstract of the work. **Where a work has only one abstract, it should be entered here, and Short Abstract can be left blank.** Long Abstract is output in metadata formats, and Short Abstract is not.

## Short Abstract

Short abstract of the work. Where a work has two different versions of the abstract, the truncated version should be entered here. Otherwise, it can be left blank. This field is not output in metadata formats; where relevant, Long Abstract is used instead.

## General Note

A general-purpose field used to include information that does not have a specific designated field. In MARC records, it corresponds to field 500.

Examples of general notes: "Previous edition: 2017.", "Links to additional resources are available from the publisher's website.", "Please note that in this book the mathematical formulas are encoded in MathML.".

## Bibliography Note

Indicates that the work contains a bibliography or other similar information. In MARC records, it corresponds to field 504.

An example of a bibliography note is: "Includes bibliography (pages 289-321) and index.".

## Table of Content

Table of content of the work.

## Related Works

This section allows the addition of a related Work, such as a Book Chapter to an Edited book. Start by searching for an existing Related Work, and if it does not exist in that list, create a new entry.

### Relation Type
Select the Relation Type from the dropdown list:
* Replaces
* Has Translation 
* Has Part
* Has Child
* Is Replaced By
* Is Translation Of
* Is Part Of 
* Is Child Of

Relation Types are symmetrical. The converse Relation Type is added to the selected Related Work.

### Relation Ordinal

Integer determining the order in which Related Works are listed, start with `1`.

## Contributions

Use the searchbar to find a [[Contributor|Thoth_Contributors]]. The **Contributor's Given Name**, **Contributor's Family Name**, and **Contributor's Full Name** have been imported from the Contributor record.

### Contribution Type
Select the contribution type from the dropdown list:
* Author
* Editor
* Translator
* Photographer
* Illustrator
* Music Editor
* Foreword by
* Introduction by
* Afterward by
* Preface by

In case the Work is an Edited Book, **do _not_ add chapter contributors as Authors**. Chapter contributors are to be recorded on the individual chapter level via the chapters listed under Related Works.

### Biography
The biography of the contributor at the moment of contribution.

### Main
Select `Yes` or `No` from the dropdown list to indicate whether the contribution is a main contribution to the Work. Main contributions are listed as such on the [[Catalogue|Thoth_Catalogue]] page. 

To provide good practice examples, in the case of a Monograph, one would mark the Main Author(s) of that monograph with `Yes`, while contributions such as prefaces, forewords, introductions, would be marked with `No`. 

With Edited Collections, the Editors of said collection would be listed on the book-level entry and marked with `Yes`, while contributions such as prefaces, introductions, concludions would be recorded on the chapter level via Related Works, and marked with `No`. Contributions by authors of full chapters will be recorded on the chapter level via Related Works, and marked with `Yes`. 

### Contribution Ordinal

Integer determining the order in which contributions are listed, start with `1`.

Once a Contribution has been entered, you can also add one or more Institutional Affiliations per Contribution. As with Funders (see below) Affiliations are drawn from the [[Institutions|Thoth_Institutions]] table. Search for the Institution affiliated with the Contribution, to which you can also add a Position and Affiliation Ordinal, which determines the order in which the affiliations are listed.


### Institution
The [[Institution|Thoth_Institutions]] affiliated with the contributor at the moment of contribution. Search for the institution in the search bar and select it. In the rare case of an institution not being listed, it is best to keep the field empty (no additional free text input available). _Optional_: Check with the Thoth development team (via info@thoth.pub) to see if an update of the underlying ROR database might be necessary, or if there are other ways for them to include the missing institution in the list.

#### Position
Optionally, add the position of the Contributor at the Institution at the moment of contribution (free text input). 
Examples: "Associate Professor", "Researcher in the Social Systems department", etc. 

#### Affiliation Ordinal
Integer determining the order in which affiliations are listed, start with `1`.

By cicking `Edit`, contributor details can be edited.

By clicking `Remove`, contributions can be removed.


## Publications

[[Publications|Thoth_Publications]] are separate instances of a single work. Click **Add Publication** to add a new publication. Click **View** to view any Publication record, and add a price.

### Publication Type

Select the publication type from the dropdown list:
* Paperback
* Hardback
* PDF
* HTML
* XML
* Epub
* Mobi
* AZW3
* DOCX
* FictionBook

### ISBN
The [[ISBN]] of the publication. Only ISBN-13s are accepted.

### Width (only for Paperback and Hardback)
Measurement perpendicular to the spine of the book. Automatically converted from in to mm or vice versa if the conversion box is ticked.

### Height (only for Paperback and Hardback)
Measurement along the spine of the book. Automatically converted from in to mm or vice versa if the conversion box is ticked.

### Depth (only for Paperback and Hardback)
Measurement of the thickness of the spine of the book. Automatically converted from in to mm or vice versa if the conversion box is ticked.

### Weight (only for Paperback and Hardback)
Weight of the book. Automatically converted from oz to g or vice versa if the conversion box is ticked.

By cicking `Edit`, publication details can be edited.

By clicking `View`, Locations and Prices can be added via the [[Publications|Thoth_Publications]] page.

By clicking `Remove`, publications can be removed.

## Languages

Click `Add Language` to add a new language.

### Language Code

Select the language code from a dropdown list. See [ISO 639-3](https://iso639-3.sil.org/code_tables/639/data) for full list of language codes.

### Language Relation
Select the language relation from a dropdown list.
* Original
* Translated from
* Translated into

### Main
Select whether the language is the main language of the work from a dropdown list.

## Subjects

Click **Add Subject** to add a new subject.

### Subject Type

Select the subject type from a dropdown list:
* [[BIC]]
* [[BISAC]]
* [[Thema]]
* [[LCC]]
* Custom
* Keyword

### Subject Code

In case of [[BIC]], [[BISAC]], [[Thema]], [[LCC]], and Custom, add the appropriate subject code. 

Keywords are words or phrases that describe content. In the context of structured metadata,
keywords are not necessarily part of a controlled vocabulary of subject terms (such as
BISAC Subject Headings, Thema or BIC Subject Classifications, or Library of Congress
Subject Headings); instead, they are words or phrases assigned by the metadata creator in
anticipation of ways in which the end user might search for content.

Although optional, and not a substitute for a controlled subject schema such as the BISAC and
Thema systems, keywords can be transmitted in ONIX and provide an additional data point for
search results and for data analysis via search engine algorithms.

For fiction, important keywords might include character names, locations, genre words.
For non-fiction, key personal names and terms of art from the subject matter. You need not
include words already used within the BISAC, BIC or Thema subject schemes.

Additional information about keywords can be found in the [BISG Best Practices for Keywords
in Metadata](https://www.bisg.org/best-practices-keywords-metadata). [BISG, _Revised Best Practices for Book Metadata_, 110]

👀 Note: [[BIC]], [[BISAC]], and [[LCC]] are all legacy classifications that are no longer properly maintained and are copyright protected. Only [[Thema]] is consistently maintained, has the widest collection of categories, and is open. **Hence, Thoth recommends focusing on [[Thema]] and [[BISAC]] classifications.** 

[[LCC]] will be generated by the Library of Congress, and [[BIC]] is [to become obsolete](https://bic.org.uk/press-releases/bic-announces-date-for-bic-standard-subject-categories-scheme-end-of-life/) as of Feb 2024. There also is a [BISAC-to-Thema translator](https://bisactothema.biblioshare.org/) available, courtesy to the [Booknet Canada](https://www.booknetcanada.ca/blog/2014/4/24/introducing-bncs-bisac-to-thema-translator.html).

### Subject Ordinal

Integer determining the order codes or keywords.

## Issues

Use the searchbar to find a [[Series|Thoth_Series]] belonging under the [[Imprint|Thoth_Imprints]] under which the Work is published.

### Issue Ordinal

The number of the Work in the Series.

## Funding

Use the searchbar to find a funding [[Institution|Thoth_Institutions]]

### Program

The name of the funding program.

### Project Name

The name of the project.

### Project Short Name

The short name of the project.

### Grant Number

The grant number of the project.

### Jurisdiction

The jurisdiction of the project.
