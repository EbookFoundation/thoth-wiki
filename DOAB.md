[Issue 47](https://github.com/thoth-pub/thoth/issues/47) ONIX 3.0 output for OAPEN is also compliant with DOAB requirements.

The [DOAB](https://www.doabooks.org/) (Directory of Open Access Books) is a discovery service for Open Access monographs, a joint project of [[OAPEN]], OpenEdition, CNRS and Aix-Marseille Université.

* Preferred metadata format: through [custom form](https://www.doabooks.org/doabAdmin?func=books) with the following [fields](https://www.doabooks.org/docs/doabUploadFieldDescription.xlsx)
* Other supported formats: [[XLSX]], [[ONIX 3.0]], [[ONIX 2.1]]
* File transfer: Browser
* Cover file: URL
* Content files: URL
* Chapter support: No

DOAB upload requirements are provided on their [website](https://www.doabooks.org/doab?func=forPublishers&uiLanguage=en) and in a list of [required metadata](https://www.doabooks.org/docs/doabMetadataApril2012.pdf)

![DOAB Metadata Upload Form](https://punctumbooks.com/punctum/wp-content/uploads/2020/10/Screenshot-2020-10-15-at-14.52.08.png)

OA books in the [[OAPEN]] repository are automatically indexed in the [[DOAB]] provided they are published under a free to share license. [[DOAB]] in turn feeds into [[Library Hub Discover]].

## Ingest

DOAB would prefer to ingest data from Thoth via an [[OAI-PMH]] feed. Upon metadata retrieval the book will typically be live on DOAB within 5 working days.