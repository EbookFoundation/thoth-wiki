Welcome to Thoth! This manual is meant to help publishers who are using Thoth to create, manage, and disseminate title metadata. The manual is a work in progress.

# Metadata Fields

## publisher

## imprint

## work_type

## work_status

## title

## subtitle

## edition
An edition of a particular work usually encompasses all copies of the work that
contain the same content, and (most often) which have been produced by the same
publisher. Publisher identification of a specified or distinct edition may be due
to changes in content (addition, revision, or removal of content) or may identify
products produced for a specific market. It is important to note that some editions,
such as second, abridged, or annotated editions, may be new works entirely; others
may contain the same content but be classified as a different edition, such as a
large print edition. [[BISG, _Revised Best Practices for Book Metadata_, 93]

Numbered editions: Please use "1" for the initial edition of a work, even if other editions are not planned.
**Named editions: [ONIX list 21?]**

## doi

## publication_date

## publication_place

## license

## copyright_holder

## landing_page

## width
Measurement perpendicular to the spine, in millimeters.

## height
Measurement along the spine, in millimeters.

## page_count
In most cases, unnumbered pages (e.g., endpapers) should be omitted from this count.
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
pages, 921). [BISG, _Revised Best Practices for Book Metadata_, 104]

## page_breakdown

## image_count

## table_count

## audio_count

## video_count

## lccn

## oclc

## short_abstract

## long_abstract

## general_note

## toc

## cover_url

## cover_caption

## contributions [...]

## publications [...]

## series [...]

## language [...]

## BIC [code]

## THEMA [code]

## BISAC [code]

## LCC [code]

## custom_categories [...]

## keywords [...]

## funding [...]

