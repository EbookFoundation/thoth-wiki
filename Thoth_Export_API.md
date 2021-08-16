The Thoth Metadata Export API allows third parties to query the Thoth database and extract records in a variety of metadata formats. The API currently allows three types of queries, into formats, specifications, and platforms. 

**Formats** are general metadata formats such as [[ONIX 3.0]] or [[KBART]]. **Specifications** are specific flavors of these formats tailered to the specifications of different **Platforms** such as [[OAPEN]] and [[Project Muse]].

There are two functionalities that may directly useful for publishers keeping their metadata records in Thoth.

# Get a publisher's metadata record

Under the menu item **Get a publisher's metadata record** you can generate a stable URL that will always point to a file containing the publisher's metadata record in a specified specification of a format.

In order to generate this link, fill in two parameters:
* **specification_id**: this parameter refers to the format specification in which the metadata record is expressed. To select a specification_id, click **TRY** under *List supported specifications** and copy the value between quote marks listed after `id`, for example, `onix_3.0::project_muse`.
* **publisher_id**: this is the unique ID of the publisher. To find the publisher_id, enter the **Admin** section of Thoth, go to the list of [[publisher|Thoth_Publishers]], and copy the **ID**. For example, punctum books has the unique id `9c41b13c-cecc-4f6a-a151-be4682915ef5`.

After filling in both parameters, click **TRY**. There will be an error message `Response State: Not Found:404` but do not panic. This error is caused by the fact that the query doesn't return text, but a file. Click on the tab **CURL** and copy the URL from there. Pasting this URL in your browser window should download the pertinent metadata file.

# Get a work's metadata record





# Thoth Metadata Export API

## List of supported formats

Click **Try** to get list.

specs 1-1 match output formats on catalog page

Schema/example give the syntax of the response

## Describe a metadata format

Take id from List above, paste, press **Try**, gives yuo the specs of only that format.

## List supported specifications

lists the specifications of the formats listed above.

## Get a publisher's metadata record

ID: comes from Thoth, this is a stable link!! Copy the link from under CURL.
