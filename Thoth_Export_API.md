The Thoth Metadata Export API allows third parties to query the Thoth database and extract records in a variety of metadata formats. The API currently allows three types of queries, into formats, specifications, and platforms. 

**Formats** are general metadata formats such as [[ONIX 3.0]] or [[KBART]]. **Specifications** are specific flavors of these formats tailered to the specifications of different **Platforms** such as [[OAPEN]] and [[Project Muse]].

There are two functionalities that may directly useful for publishers keeping their metadata records in Thoth.

# Get a publisher's metadata record

Under the menu item **Get a publisher's metadata record** you can generate a stable URL that will always point to a file containing the publisher's metadata record in a specified specification of a format.

In order to generate this link, fill in two parameters:
* **specification_id**: this parameter refers to the format specification in which the metadata record is expressed. To select a specification_id, click **TRY** under **List supported specifications** and copy the value between quote marks listed after `id`, for example, `onix_3.0::project_muse`.
* **publisher_id**: this is the unique ID of the publisher. To find the publisher_id, enter the **Admin** section of Thoth, go to the list of [[Publishers|Thoth_Publishers]], and copy the **ID**. For example, punctum books has the unique id `9c41b13c-cecc-4f6a-a151-be4682915ef5`.

After filling in both parameters, click **TRY**. With ONIX records, there will be an error message `Response Status: (CORS or Network Issue)` but do not panic. This error is caused by the fact that the query doesn't return text, but a file. Click on the tab **CURL** and copy the URL from there. Pasting this URL in your browser window should download the pertinent metadata file.

# Get a work's metadata record

The same procedure as getting a publisher's metadata record. Instead of **publisher_id**, you'll need a **work_id**. To find the work_id, enter the **Admin** section of Thoth, go to the list of [[Works|Thoth_Works]], and copy the **ID**. For example, *A Boy Asleep under the Sun* has the unique id `5402ea62-7a1b-48b4-b5fb-7b114c04bc27`.

Alternatively, you may obtain a work_id from the [[GraphQL API|Thoth_GraphQL_API]].

# Supplement: Per-Publisher MARC records

These MARC record files can be used by libraries to integrate a publisher's whole catalogue of books into their library management systems. _Please note that other formats are also available, and the export API's endpoint can also be used to directly pull relevant records from Thoth into your respective Library Management System.

### MARC21record

* Mattering Press: [Mattering Press' books](https://export.thoth.pub/specifications/marc21record%3A%3Athoth/publisher/17d701c1-307e-4228-83ca-d8e90d7b87a6)
* meson press: [meson press books](https://export.thoth.pub/specifications/marc21record%3A%3Athoth/publisher/f0ae98da-c433-45b8-af3f-5c709ad0221b)
* White Horse Press: [White Horse Press' books](https://export.thoth.pub/specifications/marc21record%3A%3Athoth/publisher/ba67afbb-2b43-4ef8-b1cc-d7333706d54e)
* Open Book Publishers: [OBP books](https://export.thoth.pub/specifications/marc21record%3A%3Athoth/publisher/85fd969a-a16c-480b-b641-cb9adf979c3b)
* punctum books: [punctum books](https://export.thoth.pub/specifications/marc21record%3A%3Athoth/publisher/9c41b13c-cecc-4f6a-a151-be4682915ef5)
* African Minds: [African Minds' books](https://export.thoth.pub/specifications/marc21record%3A%3Athoth/publisher/b61217e4-3134-4bfe-8695-30e047ed3f57)
* mediastudies.press: [mediastudies.press' books](https://export.thoth.pub/specifications/marc21record%3A%3Athoth/publisher/4ab3bec2-c491-46d4-8731-47a5d9b33cc5)

