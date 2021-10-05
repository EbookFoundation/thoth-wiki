[Issue 48](https://github.com/thoth-pub/thoth/issues/48) Issue Closed. ONIX output for OAPEN available.

[OAPEN](https://oapen.org/) is an online library and publication platform promoting and supporting the transition to open access for academic books by providing open infrastructure services to stakeholders in scholarly communication. 

* Preferred metadata format: [[ONIX 3.0]], encoded in UTF-8
* Other supported formats: [[DOCX]], [[XLSX]], [[CSV]], [[ONIX 2.1]]
* File transfer: through URL in [[ONIX 3.0]] spec
* Cover file: Extracted from content file
* Content files: [[PDF]], [[EPUB]]
* Chapter support: No

OAPEN provides guidelines for [uploading books and metadata](https://cloud.copim.ac.uk/s/C7KPbNDaLwJcfL5) and a [sample ONIX 3.0 file](https://cloud.copim.ac.uk/s/PjxsDr7TbjxGgPJ).

OAPEN provides multiple [metadata feeds](https://oapen.org/librarians/15635975-metadata), including [[MARCXML]], [[ONIX 3.0]], and [[CSV]].


## Ingest

OAPEN would prefer to ingest data from Thoth via an [[OAI-PMH]] feed. Upon metadata & file retrieval the book will typically be live on OAPEN within 5 working days.


## Embargo

OAPEN can support embargo periods for books (typically up to 3 months). The book page will be live, including description but the book file(s) cannot be accessed yet. Upon request and for special occasions only OAPEN can manually input a title and its metadata on an exact day to ensure it won't appear in any form online prior to the desired date.
