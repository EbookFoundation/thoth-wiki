A Work is a unit of publication with at least one unique identifier.

The **Works** page will display the Works all users have access to. The following information is displayed:

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
An edition of a particular work usually encompasses all copies of the work that
contain the same content, and (most often) which have been produced by the same
publisher. Publisher identification of a specified or distinct edition may be due
to changes in content (addition, revision, or removal of content) or may identify
products produced for a specific market. It is important to note that some editions,
such as second, abridged, or annotated editions, may be new works entirely; others
may contain the same content but be classified as a different edition, such as a
large print edition. (BISG, _Revised Best Practices for Book Metadata_, 93)

Numbered editions: Please use "1" for the initial edition of a work, even if other editions are not planned.
**Named editions: [ONIX list 21?]**

## Publication Date

The date of publication in the format `dd/mm/yyyy`.

## Place of Publication

The place of publication. 

## Cover URL

URL referring to the cover image.

## Cover Caption

Caption referring to the cover image.

## DOI

[[Digital Object Identifier|DOI]] of the Work. 

## LCCN

The [[Library of Congress Catalog Number|LCCN]] of the Work.

## OCLC Number

The [[OCLC Number]] of the Work

## Internal Reference

The reference to the Work used by the Publisher internally.

## Width
Measurement perpendicular to the spine of the book.

## Height
Measurement along the spine of the book.

## Units

Select the unit of **Width** and **Height** from the dropdown list:
* mm
* cm
* in

## Page Count

Total number of pages. In most cases, unnumbered pages (e.g., endpapers) should be omitted from this count.
(Unnumbered pages that are part of plate sections/inserts are part of the book’s content and
should be counted.) Books that have pages numbered in both roman and Arabic numerals
(and no inserts) should have a Page Count that reflects the sum of the highest number of the
roman-numbered pages plus the highest number of the Arabic-numbered pages. _This value_
_is therefore **not necessarily** the total number of pages bound into the book – there may for_
_example be blank leaves at the back_. The sole exception to this is the case of a book with no
numbered pages; in such a case the value given for Page Count should be the total number
of all pages in the book.

For multi-volume books sold under a single Product Identifier, enter the total for all the
volumes combined in the product record for the multi-volume product. If the individual
volumes are sold separately, each of their product records should carry a Page Count for only
the volume in question. 

**Example**

Using _The Chicago Manual of Style_, 14th edition as an example, one sees that the front
matter is numbered in roman numerals up to page ix. The main body of the work has pages
numbered in Arabic numerals up to page 921. The book also contains five unnumbered
pages at its end and both a front and a back flyleaf. For the purposes of these best practices
guidelines, the Page Count sent out for this book should be 930 (the sum of the highest
number of the roman-numbered pages, 9, plus the highest number of the Arabic-numbered
pages, 921). (BISG, _Revised Best Practices for Book Metadata_, 104)


## Page Breakdown

Breakdown of **Total number of pages** in frontmatter, main, and backmatter.

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

## Copyright Holder

Copyright holder of the work.

## Landing Page

URL of the web page of the work.

## Short Abstract

Short abstract of the work.

## Long Abstract

Long abstract of the work.

## General Note

Note about the work.

## Table of Content

Table of content of the work.

## Contributions

Use the searchbar to find a [[Contributor|Thoth_Contributor]]. The **Contributor's Given Name**, **Contributor's Family Name**, and **Contributor's Full Name** have been imported from the Contributor record.

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

### Institution
The institution of the contributor at the moment of contribution.

### Biography
The biography of the contributor at the moment of contribution.

### Main
Select whether the contribution is main contribution from the dropdown list. Main contributions are represented on the [[Catalogue|Thoth_Catalogue]] page.

### Contribution Ordinal
Integer determining the order in which contributions are listed.

## Publications

[[Publications|Thoth_Publications]] are separate instances of a single work. Click **Add Publication** to add a new publication. Click **View** to view any Publication record and add a price.

### Publication Type

Select the publication type from the dropdown list:
* Paperback
* Hardback
* PDF
* HTML
* XML
* Epub
* Mobi

### ISBN
The [[ISBN]] of the publication.

### URL
The URL of the publication, for example a link to a repository such as [[OAPEN]] or [[JSTOR]].

## Languages

Click **Add Language** to add a new language.

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

Although optional, and not a substitute for controlled subject schema such as the BISAC and
BIC systems, keywords can be transmitted in ONIX and provide an additional data point for
search results and for data analysis via search engine algorithms.

For fiction, important keywords might include character names, locations, genre words.
For non-fiction, key personal names and terms of art from the subject matter. You need not
include words already used within the BISAC, BIC or Thema subject schemes.

Additional information about keywords can be found in the [BISG Best Practices for Keywords
in Metadata](https://www.bisg.org/best-practices-keywords-metadata). [BISG, _Revised Best Practices for Book Metadata_, 110]

[[BIC]], [[BISAC]], and [[LCC]] are all legacy classifications that are no longer properly maintained and are copyright protected. Only [[Thema]] is consistently maintained, has the widest collection of categories, and is open. 

### Subject Ordinal

Integer determining the order codes or keywords.

## Issues

Use the searchbar to find a [[Series|Thoth_Series]] belonging under the [[Imprint|Thoth_Imprints]] under which the Work is published.

### Issue Ordinal

The number of the Work in the Series.

## Funding

Use the searchbar to find a [[Funder|Thoth_Funders]]

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