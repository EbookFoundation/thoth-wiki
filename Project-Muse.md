[Issue 102](https://github.com/thoth-pub/thoth/issues/102)

### Progress: 
ONIX metadata output can be generated from Thoth

[Project Muse](https://muse.jhu.edu/) is an online scholarly library managed by Johns Hopkins University focused on the humanities and social sciences. 

* Preferred metadata format: [[ONIX 3.0]]
* Other supported formats: [[XLSX]], [[ONIX 2.1]]
* File transfer: via uploader tool
* Cover file: [[JPEG]], [[GIF]], [[PNG]]
* Content files: [[PDF]], [[EPUB]]
* Chapter support: Yes

For metadata uploads in [[XLSX]] there is a [proprietary template](https://about.muse.jhu.edu/media/uploads/metadata_submission_template.xls). They also provided a [sample ONIX 3.0 file](https://cloud.copim.ac.uk/s/tWfeyRH7bi9reHa).

Project MUSE exposes a [[KBART]] [file](https://about.muse.jhu.edu/lib/metadata?format=kbart&content=book&no_auth=1&collection_ids=726) of its OA holdings

## Metadata Requirements

Regardless of format, the following fields are required for a metadata feed to successfully load into our system:

* eISBN
* Title
* Subtitle [if applicable]
* [At least 1] BISAC or BIC subject code(s)
* [At least 1] Contributor
* Contributor Role
* Contributor Statement
* Digital List Price
* Print Publication Date

## Preparing and Submitting Book PDFs

* Format the book PDF according to [these instructions](https://cloud.copim.ac.uk/s/gm2GdExdtDeX453), making sure that all fonts are fully embedded and that you have not subset the fonts. (Fonts that are not fully embedded are incompatible with our search engine and will be undiscoverable.)
* Name the book PDF with the book's eISBN.
* Bookmark each section of the ebook PDF, including the Cover, Front Matter, TOC, Chapters, and Back Matter.
* Prepare the cover image file (JPEG, GIF, or PNG) for submission with the ebook PDF and name it with the same eISBN as the book PDF. (Do not submit the cover as a PDF. It will overwrite your book PDF.)
* Submit the book PDF and the cover image file using the Project MUSE book uploader.

## Preparing and Submitting Book EPUB Files

Project MUSE accepts EPUB 3 files, which are converted to HTML 5 and served to users via web browsers. In order for your EPUB to be compatible with this process, please follow [these instructions](https://cloud.copim.ac.uk/s/fGNorHxEafjFb2G). Our system will use this data to automatically generate the web TOC when the book launches on Project MUSE.

Once the EPUB 3 file has been formatted correctly, name the file after the book’s ISBN-13 (ie. 9780000000000.epub). This allows it to be easily matched with the corresponding metadata in our database.

Submit the EPUB, along with the cover JPEG and PDF, using the Project MUSE book uploader or via your established DAM vendor channel.

For more information on submitting Open Access files and metadata, [please refer to these detailed instructions](https://about.muse.jhu.edu/pub/docs/oa-books-instructions).

