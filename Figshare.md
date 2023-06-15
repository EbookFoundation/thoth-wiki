[Figshare](https://figshare.com/) is a paid service underpinning many institutional repositories.

It has a well-documented [public API](https://docs.figshare.com/) which account holders can use to interact with their repository (as an alternative to the GUI). This facilitates the automation of archiving and preservation tasks, such as uploading content files and adding metadata.

## An in-depth look at the Figshare API: notes for repository users and developers

_This text was originally compiled in early 2022. Some aspects of the API may have changed since then._

This is a compilation of notes made during initial attempts to connect Thoth to the Figshare API, testing against the Loughborough University Figshare repository with the aim of making a proof-of-concept deposit. While Thoth-specific, these notes go into a lot of technical detail about the Figshare API, covering many points that should assist others aiming to interact with it.

A more general overview can be found in this [COPIM blogpost](https://copim.pubpub.org/pub/experimenting-with-repository-workflows-for-archiving-automated-ingest/release/1). The Thoth-specific Rust code described here was later superseded by the Python-based [Thoth Dissemination Service](https://github.com/thoth-pub/thoth-dissemination/).

### Summary

The Figshare API works in a similar way to the two Thoth APIs (the GraphQL API for database data and the Export API for metadata file output). Submitting any data to the Figshare API usually involves sending a POST request with a JSON body to a specific HTTP endpoint. The Thoth user interface (web app) sends similar requests to the Thoth APIs, so it should be possible to re-use this logic to interact with the Figshare API.

The full API can be explored at <https://docs.figshare.com/swagger.json> as well as via the documentation link. Specifications of the various field objects etc are also listed under <https://docs.figshare.com/#description_presenters>. Some pointers and examples of how to use the API (including very simple requests that can be made in-browser on real data) can be found at <https://help.figshare.com/article/how-to-use-the-figshare-api>.

### Initial research (synthesis of documentation)

#### Figshare structure

* Deposit requests must contain an Authorization header containing a token related to a user account (OAuth 2.0).
* Figshare content is either 'private' or 'public'. New content can only be created as 'private'. Making a public deposit is therefore a two-stage process: 1) create the content, 2) publish it.
  * 'Publishing' content creates a duplicate version of the private content under a separate URL. The private version persists after publication.
  * Public content cannot be updated directly: first the private version must be updated, then it must be re-published.
* The basic unit of Figshare content is the 'article'. This can come in many types, such as Monograph, Dataset, Figure, Chapter.
* Multiple articles can be grouped together under a 'collection' or 'project'.
* Initial creation of an article is metadata-only (<https://docs.figshare.com/#private_article_create>). Once the article is created, files can be uploaded to it (<https://docs.figshare.com/#private_article_upload_initiate>).

#### Authorization

Steps to obtain Authorization tokens are listed here: <https://docs.figshare.com/#figshare_documentation_oauth>

* Log in to Figshare user account and "register" the "application" (in our case, Thoth).
* On registration, receive "client ID" and "secret".
* Send a request to the authorization endpoint, containing the client ID, with `response_type` set to `code`.
* The response to the request will contain an authorisation code (as one of the query parameters to the redirect URL).
* Send a request to the token endpoint, containing the client ID, the secret, and the code.
* The response to the request will contain an access token, which can be included in the Authorization header of relevant requests.

Alternatively, a user can obtain a personal access token directly from the Figshare interface, which can be included in Authorization request headers in the same way.

#### Article details

* Articles are a good representative template for what metadata can be included in Figshare content, and how to format it.
* Articles are created by sending a POST request (with an Authorization header) to the HTTP endpoint `https://api.figshare.com/v2/account/articles`, with a JSON body containing details of the article (<https://docs.figshare.com/#description_presenters_articlecreate>).
* A successful request will prompt a response with a JSON body containing the newly-created article's ID and its full URL (in the format `/account/articles/{article_id}`).
* The only mandatory property to be submitted in the request JSON is the article's "title".
  * However, before an article can be published, several other properties also need to be supplied (this is only(?) indicated in the GUI):
    * "authors": array of author details objects, each of which can contain multiple fields. Note only a maximum of 10 authors can be added on initial article creation; others must be added separately (via the `authors` endpoint).
    * "categories": array of numeric category IDs, which will appear (as their text equivalents) as a clickable list on the article page
    * "defined_type": this appears to be how the article type, e.g. Monograph, Dataset, is specified. However, on article creation, a text keyword is requested (from a limited list which excludes e.g. Monograph), but on article search, a numeric ID is requested (from a longer list, including e.g. 15 - Chapter, 25 - Monograph).
    * "tags": array of free text keywords, which will appear as a list of clickable search items on the article page (synonymous with separate property "keywords" - values submitted as "keywords" will be stored/returned as "tags")
    * "description": free text description (can contain HTML)
    * "license": numeric licence ID, which will appear as a clickable icon on the article page
* Other optional properties include:
  * "funding"/"funding_list": text denoting a grant number or funding authority, or array of numeric ID/string pairs, representing existing(?) Figshare funding objects (which are linked to the [Dimensions.ai](https://www.dimensions.ai/) database)
  * "timeline": an array of date details objects, which will appear as a list under the 'History' heading on the article page
* A number of further properties are listed as 'not applicable to regular users':
  * For institutions: "doi" and "handle" (can only be used if the institution has the appropriate settings)
  * For publishers: "resource_doi" and "resource_title" (described as the 'publisher article DOI' and 'publisher article title')
    * Difference between "doi" and "resource_doi" is unclear; perhaps "doi" is the Figshare-assigned DOI and "resource_doi" is the canonical work DOI (which Thoth records).

#### Property specifications

* Categories: the full list of public categories, with their numeric IDs and text equivalents, can be found by testing the endpoint under <https://docs.figshare.com/#categories_list>. We could consider creating a mapping to automatically convert Thoth subjects to Figshare categories (which are taken from the [Australian Fields of Research](https://www.arc.gov.au/grants/grant-application/classification-codes-rfcd-seo-and-anzsic-codes) classification system); however, there are prohibitively many (of both).
  * Loughborough frequently use "unspecified" because of this issue.
* Authors: objects can contain the fields "id", "name", "first_name", "last_name", "email" and/or "orcid_id" (<https://docs.figshare.com/#description_presenters_author>). "id" represents a Figshare ID and all other fields will be overridden with Figshare author details if included.
* License: the full list of public licences, with their numeric IDs, can be found by testing the endpoint under <https://docs.figshare.com/#licenses_list>. Only 7 are supported: CC-BY 4.0, CC0, MIT, GPL, GPL 2.0+, GPL 3.0+, and Apache 2.0. Further licences can be added to an institutional account and then viewed at <https://docs.figshare.com/#private_licenses_list> (they will then be assigned private numeric IDs).
* Timeline: objects can contain the fields "firstOnline", "publisherPublication" and/or "publisherAcceptance" (<https://docs.figshare.com/#description_presenters_timeline>). Field values are dates in YYYY-MM-DD format.

#### File upload

The 'Figshare upload service API' is apparently distinct from the 'Figshare API', and seems to be less well defined. There are instructions on how to upload files, with examples, at <https://docs.figshare.com/#upload_files>:

1. Calculate the MD5 hash of the file to be uploaded.
2. Submit a POST request to the `articles/{article_id}/files` endpoint, with a JSON body containing this hash ("md5"), the file "name", and the file "size".

* Alternatively, supply the "link" to an existing file hosted elsewhere - but this will not upload a copy of the file to Figshare, so is not suitable for our purposes.

3. Receive a response to the request containing a newly created URL for the file, which will contain the file ID.
4. Submit a GET request to the file URL (of the form `articles/{article_id}/files/{file_id}`) to receive a response containing an "upload_url" and "upload_token" (<https://docs.figshare.com/#description_presenters_privatefile>).
5. Submit a GET request to the upload URL (of the form `upload/{token}` - we have moved to the upload service API) to receive a response detailing how many parts the file needs to be split into for upload, and the start/end offsets of these parts (<https://docs.figshare.com/#description_presenters_uploadinfo>).
6. Split the file into the required parts.
7. For each part, submit a PUT request, with the binary file data as the body, to the `upload/{token}/{part_number}` endpoint.
8. Confirm completion of the upload by submitting a POST request to the `articles/{article_id}/files/{file_id}` endpoint (moving back to the standard Figshare API).

Note that the instructions/examples mostly assume that the file to be uploaded is stored locally (although there is also an example for submitting files directly from AWS S3, if the AWS key/secret are known). Thoth stores links to publication files, but does not store the files themselves. Automatic upload would therefore probably require downloading a copy of the relevant file and then re-uploading the copy to Figshare.

* As encountered in [previous manual testing](https://copim.pubpub.org/pub/experimenting-with-repository-workflows-for-archiving-manual-ingest/release/1), some of the files linked in Thoth are not publicly accessible/downloadable, e.g. OBP publications link to public PDF and XML files but paywalled EPUB and MOBI files. This would need to be worked around somehow.
* Meanwhile, not all files associated with a work are linked in Thoth. For example, the previous testing investigated uploading works which have several audio/image file resources, none of which are listed within Thoth, but were added manually to the book pages on the OBP website. We may want to extend Thoth to track 'additional resources' provided with a work.

#### Projects/Collections

* A 'collection' can be defined with most of the same properties as an 'article', e.g. authors, categories, etc. It can also take an "articles" property, containing an array of IDs of existing articles.
* A 'project' has a more limited set of properties, only covering title, description, funding.
* Once a project is created, a new article can be created and associated with it in a single step (<https://docs.figshare.com/#private_project_articles_create>). The creation request is the same as for basic article creation, but the endpoint path contains the project ID.
  * This cannot be done for collections: articles must be created separately and then added to the collection.

#### Other useful methods

* <https://docs.figshare.com/#private_article_embargo_update>: set an embargo on an article (used in previous manual testing to upload paywalled content such as EPUB and MOBI book versions)
* <https://docs.figshare.com/#private_article_publish>: make a private article public. Note that this doesn't convert the existing article, but creates a new public copy of the private article. Future changes to the public article must be made by amending the private article and then repeating the `publish` request (public articles can't be amended directly).
* <https://docs.figshare.com/#custom_fields>: allows custom object properties to be defined (as can also be done via the API) - this could be used for storing e.g. external links.
* <https://docs.figshare.com/#private_article_resource>: allows "resources" (links) to be added to articles - intended use unclear but could be another way of linking to unhosted "Additional Resources".

### Practical investigation (coding-based)

#### Work done

* Proof of concept: add simple user-activated triggers within Thoth Work page to submit Work metadata to Figshare in private Article format, and to upload files (currently only example data) to the Article.
  * Further work extended this to investigate submission of Work metadata in Project format, with Publications added as related Articles.
* Currently: all work on [a standalone GitHub branch](https://github.com/thoth-pub/thoth/tree/feature/289_figshare_api). All logic within [a single file](https://github.com/thoth-pub/thoth/blob/feature/289_figshare_api/thoth-app/src/component/figshare.rs) in the Thoth app (browser-based user interface component of Thoth).
  * Comments within the code form a complement to this summary, noting relevant in-depth details of the Figshare API discovered in the course of developing the logic.
  * Version at time of writing: [commit ddb9445](https://github.com/thoth-pub/thoth/commit/ddb944509d0f34e32f2c346520d02d3b0b919140).
* The command-line tool [curl](https://curl.se/) was also used ad hoc to send HTTP requests to the Figshare API and examine the responses received, by way of testing and experimentation.
* Ad-hoc testing was also done via the interactive in-browser endpoints at the documentation link (<https://docs.figshare.com/>). As we were using a test instance of the API rather than the live instance, it was necessary to replace "figshare" in the URL with "figsh", i.e. <https://docs.figsh.com/>.
* Outcomes:
  * Successfully connected to many of the documented Figshare endpoints and uploaded data
  * Uncovered quirks of Figshare API not fully noted in documentation
  * Created working open-source example [Rust](https://www.rust-lang.org/) code paths for interacting with Figshare API - starting point for future development (either by us or by others)

#### Not yet implemented

* Full Work = Project and Publication = Article logic
* Handling of multi-part files, including logic to check all parts succeeded before marking upload as 'completed'
* Publishing private Article, and verifying that publication succeeded (e.g. no missing mandatory fields)
* Full error handling, reporting errors (/successes) to user, user-friendly display/interface
* Submission of category metadata (requires translation between Thoth representation and Figshare ID)
* Fix bug in file upload: MD5 is calculated accurately but submitted incorrectly (formatted as JSON instead of binary)
* See also TODO comments in code

#### Technical considerations (Figshare)

When submitting metadata and files, we are constrained by the record structure and properties offered by Figshare, which do not always overlap well with Thoth metadata representations.

* Thoth stores a richer set of metadata than is accepted by Figshare as defined (i.e. robustly searchable/connected) property fields.
  * This could be mitigated by uploading a full metadata file in a standard format (e.g. XML) in parallel with filling out Figshare property fields. This would make the preservation more robust while maintaining its discoverability.
  * Figshare also allows the creation of "custom fields" (on Articles/Collections/Projects), so another option would be to use these to enhance a repository's template to match the Thoth metadata representation. Not clear how useful this would be, e.g. how discoverable these fields are.
* Thoth objects and Figshare objects need to be identifiably linked, e.g. to check whether an existing Figshare record exists for a Thoth Work and can be updated (and avoid creating duplicate Figshare records), and to allow viewers of Figshare to find the full Thoth metadata if desired.
  * Each Figshare object is given an ID on creation (which forms the basis of its URL), which could potentially be stored in Thoth, but it is unclear where it would be appropriate to do this.
    * There are currently no appropriate fields on the Thoth Work.
    * Thoth Publications allow storing URLs to externally hosted versions of content (e.g. at OAPEN, Project MUSE, etc), and so it would be appropriate to add URLs linking to Figshare uploads here.
      * We are also considering a mechanism for automatically distributing content to external hosts and then storing the URLs created, which would tie in with the desired Figshare process.
      * However, this would not be the right level at which to store Figshare IDs/URLs relating to the Work as an umbrella.
      * These fields might also only be filled out once a content file was uploaded, in which case they would not give any information about whether a work-in-progress Figshare record without any files existed for the Work/Publication.
  * Each Thoth object (e.g. Work) also has an ID which relates predictably to its URL(s), but it is unclear where these should be stored in Figshare.
    * Note that Thoth object IDs are only guaranteed unique per Thoth instance. If other users installed the Thoth software and created their own separate metadata databases, then linked them to Figshare, there is an outside chance that the same ID could be assigned to different Works stored under different Thoth instances.
    * Figshare has a search function which allows searching directly on some properties, as well as generically across "all metadata fields", so this could be used to retrieve a Figshare record based on a Thoth metadata value.
      * "resource_doi" is directly searchable, but not all Thoth Works might have a DOI at point of record creation.
      * Other directly searchable properties (e.g. "title") are not guaranteed unique within Thoth.
      * We could attempt to repurpose an existing directly searchable Figshare property to store the Thoth Work ID. Possibilities include "doi", "handle" and "resource_title", but it is not clear how they are intended to be used, or whether it would be valid to repurpose them. (In particular, "doi" presumably represents the Figshare-assigned DOI, and should be formatted appropriately, and might be automatically overwritten.)
      * The solution chosen was to store the Thoth Work ID in a "custom field". This appears to be reliably retrieved using the "all metadata fields" Figshare search.
* The previous manual testing created a Project/Collection as the equivalent of a Thoth Work, and individual Articles as the equivalent of child Thoth Publications (e.g. PDF version, XML version, etc.). The coding work created a single Article as the equivalent of a Thoth Work, as a representative example (many Article properties and API endpoints are similar to those of Projects/Collections). The original structure is preferable, but raises some considerations:
  * Collections, and especially Projects, offer fewer Figshare-defined property fields than Articles. If we view the Collection/Project as the entry point for the Work, and Articles as merely containers for the Publication files, the metadata stored will be less rich.
    * This could be overcome by storing all available metadata on the Articles as well.
  * Files can only be uploaded to Articles, not Collections/Projects - if we wanted to upload any files relating to the Work as a whole rather than individual Publications (e.g. a full metadata file), it is unclear where these should be stored.

Note that Figshare provide:

* skeleton client programs in a number of programming languages (e.g. <https://docs.figshare.com/clients/python.zip> - linked in the "Other" tab under any endpoint example)
* example scripts in Python/Bash for file upload (<https://docs.figshare.com/#upload_files_example_upload_on_figshare>)
* a plugin for automating file upload via GitHub (<https://github.com/figshare/github-upload-action>)
* a (recently introduced) GUI tool for Institutional Administrators to upload batch metadata and links to files via CSV (<https://help.figshare.com/article/administrative-batch-management>).

Work done to connect with the Figshare API via Thoth partially replicates these resources, but in the Rust programming language (not offered in the Figshare client set), and integrated with the Thoth user interface. It is also free and open source, whereas the Figshare source code is not transparently hosted (e.g. on GitHub). However, the Figshare resources provide an ample basis for developers to create their own connections to the API.

#### Figshare API behaviour

##### Endpoints/objects

The API [documentation](https://docs.figshare.com) is reasonably comprehensive, and the [Swagger version](https://docs.figshare.com/swagger.json) provides a useful quick reference. It documents all available endpoints (paths), the HTTP methods which can be used on them, the parameters (if any) which need to be submitted, the responses which may be returned, and the objects (definitions) which may be referenced in them, e.g. as request or response bodies.

* The Swagger version only covers the main Figshare API, not the upload API.

The documentation is worth becoming familiar with, but it omits some details (e.g. mandatory vs optional vs defaulting fields, error vs warning vs silent failure behaviour), and the API structure is not always intuitive. Some pointers:

* Some objects have multiple varying representations, and it is not always clear which is needed when. The object used when creating a record may be different from the object returned when viewing it. This can lead to confusion when trying to construct queries.
  * For example, authors can be represented by the [Author](https://docs.figshare.com/#description_presenters_author) object, the [AuthorComplete](https://docs.figshare.com/#description_presenters_authorcomplete) object and the [AuthorsCreator](https://docs.figshare.com/#description_presenters_authorscreator), all of which have different sets of fields. The AuthorsCreator object also appears to be used for the "authors" child property of the [ArticleCreate](https://docs.figshare.com/#description_presenters_articlecreate) object, although it is not labelled as such in the documentation.
  * A similar issue is observed with field names: e.g. when [searching for authors](https://docs.figshare.com/#private_authors_search), filtering on ORCIDs requires an "orcid" field, but the returned responses will include "orcid_id" fields.
* Meanwhile, some objects which are differently named turn out to have the same representation.
  * ArticleCreate and ArticleUpdate objects appear to have identical sets of fields, so the same JSON body can be used both for creating a new article and for updating an existing article.
  * The same is true of CollectionCreate/CollectionUpdate and - with the exception of the "group_id" attribute - ProjectCreate/ProjectUpdate.
* Some conceptually similar requests result in slightly different responses.
  * For example, creating an article returns a [LocationWarnings](https://docs.figshare.com/#description_presenters_locationwarnings) success response, updating an article returns a [LocationWarningsUpdate](https://docs.figshare.com/#description_presenters_locationwarningsupdate) success response, and publishing the article returns a [Location](https://docs.figshare.com/#description_presenters_location) success response. These all include a "location" field, but vary in whether they also include "warnings" or "entity_id" fields.
  * Many failed requests return an [ErrorMessage](https://docs.figshare.com/#description_presenters_errormessage) response with fields "code" and "message", so code which calls the API must be able to handle both types of response body structure.
    * Response body type should be predictable from the HTTP status code (e.g. 200 for success, 400 for error).
* Some optional fields will be left empty if omitted on submission, while others will be automatically set to defaults.
  * For example, when creating/updating an article, if "license" is omitted, it will default to 1, if "defined_type" is omitted, it will default to 11 (online resource), and if "authors" is omitted, it will default to a list containing the logged-in user as the single item. All other optional fields appear to be left as empty/null.
  * This has implications for e.g. checking whether a private article's record is complete before publishing it - although we may not have supplied values for mandatory public article fields such as "license" or "defined_type", they will always be non-empty (and may not be accurate).
* In some cases, an error will be raised if an incorrect field name is submitted, but in other cases, it will be silently ignored.
  * For example, when submitting an AuthorsCreator object, erroneously including a "full_name" field (instead of "name") will result in failure with the message "Invalid params: authors (Invalid 'full_name' field received)" (irrespective of whether other valid fields are also included).
  * However, when submitting a [TimelineUpdate](https://docs.figshare.com/#description_presenters_timelineupdate) object, erroneously including a "publisher_publication" field as the only field (instead of "publisherPublication") will return a success response but not have any effect.
  * Likewise, when [searching for authors](https://docs.figshare.com/#private_authors_search), erroneously including an "orcid_id" field as the only field (instead of "orcid") will return a success response containing all authors, not filtered by "orcid_id" (i.e. the same behaviour as if no parameters had been submitted).
* Similarly, incorrect field types may not always be well handled.
  * The AuthorsCreator "id" field needs to be an integer type, but if it is erroneously submitted as a string, a success response will be returned, but the "id" will be interpreted as empty (clearing any existing author on a replace request).
    * Note that this only seems to occur with valid ID values converted to strings; submitting a string of alphabetic characters, or a string of numeric characters which does not correspond to a known Figshare author ID, will instead fail with the error "Constraint error: Invalid id supplied for User entity".
  * However, erroneously submitting a "license" value as a string instead of an integer will fail with the error message "license: '[value]' is not of type 'integer'".
* When [updating an article](https://docs.figshare.com/#private_article_update), only the fields which are included are updated, i.e. omitting existing fields does not clear them.
  * For most field types, including the field but leaving it empty will clear existing field values. This is probably what we want as the final Figshare record ought to match the final Thoth record (e.g. values erroneously entered at an earlier point should be corrected if subsequently removed), although it raises a meta-question around preservation of the history of the metadata record!
* The documentation for obtaining the [list of available custom fields](https://docs.figshare.com/#custom_fields_list) implies that including a "group_id" value is mandatory, however, it can be omitted and it will default to the group of which the user is a member (this is clearer in the Swagger documentation).
* When [updating an article](https://docs.figshare.com/#private_article_update), a success response should contain a LocationWarningsUpdate body. This is received successfully in curl, but no body is received when submitting the request via the browser app. The response received by the app does contain `Content-Type` and `Content-Length` headers which correspond to the expected body. All other tested response bodies were received correctly in the browser app, so it is unclear what the issue is here.

##### Authorization

All work was carried out using a personal access token obtained directly from the Figshare interface. We also registered Thoth as an application with a view to implementing the OAuth2 workflow, but this was blocked while waiting for a support ticket response.

* Testing this workflow may require a user to log in with their personal Figshare credentials, which would be inconvenient as the tester does not have a Figshare account.
* Figshare support suggested that behaviour might be different on the test instance than on the main instance: specifically, that it may be necessary to include a username and password in the URL when contacting the authorization endpoint (in the format `https://[username]:[password]@[instance].figsh.com/account/applications/authorize`). This is yet to be tested.
* Note that the OAuth2 workflow is only required if we wish to embed a Figshare login into Thoth, so that each Thoth user can submit items to Figshare using their own personal Figshare account. We may decide that a better approach is to have a specific "Thoth" account in Figshare to which all user submissions are attributed. If so, using the "Thoth" account's personal access token for all API interactions would be the correct authorization method.

##### Article properties

Author:

* Submitting an "author" object without including a Figshare author ID (optional) automatically creates a new Figshare record for that author and assigns them a new Figshare author ID.
  * This is the case even if e.g. the author name matches an existing Figshare author record (and note anyway that names are not unique or unchanging identifiers).
  * If the "orcid" or "email" field matches an existing Figshare author record, the submission is rejected with an error message indicating that orcids/emails must be unique across all authors.
* Thoth does not store authors' Figshare IDs, there are no plans to add this information, and we could not realistically expect to harvest many of them if we did.
  * Thoth does store ORCIDs and so does Figshare, but not all Thoth author ORCIDs are known (if they exist).
* There is therefore the risk that we will create many duplicate Figshare author records.
  * This is a known problem when submitting metadata to Figshare manually - cf Loughborough system where only main author's ID is included - so we might consider it not in scope here.
  * We could potentially mitigate this by storing the returned author ID within Thoth the first time a record is created, and then re-using it afterwards. However:
    * Thoth author data structure supports e.g. authors changing names between publications, which Figshare does not (using the Figshare author ID would overwrite any publication-specific name variant with the Figshare record version).
    * Adding such platform-specific logic is generally to be avoided as it could make Thoth overcomplicated/cluttered and harder to maintain.
* There is also the risk that submissions will fail if the author's ORCID is known and already stored within an existing Figshare author record.
* Storing the Thoth author ("Contributor") ID within Figshare would be a useful workaround as it could allow Figshare users to disambiguate duplicates and access the richer author metadata within Thoth (cf discussion of Thoth Work IDs above).
  * However, the "author" object only supports a limited number of fields, and it is not clear which (if any) would be appropriate for this.
  * For example, we can submit an "email" field, but there seems to be no way to retrieve it (perhaps it is Figshare-internal). Note also that it could cause failed submissions as with ORCIDs.
* It may be necessary to search Figshare for existing matching author records, and then include the Figshare ID if found, before submitting any author's details.
  * At minimum, this should be done for authors whose ORCID is known, to avoid failed submissions.
  * The downside is that this would overwrite the more granular Thoth author data with the version stored in Figshare, as discussed above.
  * The [Figshare author search endpoint](https://docs.figshare.com/#private_authors_search) appears to be unreliable, failing to return any results for known existing values of either "orcid" or "search_for". This may require a support ticket. It may be some kind of permissions issue, as most of the values searched related to authors created during the testing process.
* Figshare's ORCID validation appears to be stricter than Thoth's (Thoth uses the URL match pattern specified by [Wikidata](https://www.wikidata.org/wiki/Property:P496), but does not validate the final checksum character). If an ORCID has been entered into Thoth with an incorrect checksum character, submission of records connected to that author may fail with error "Invalid 'orcid' field received".

Defined type:

* The [documentation](https://docs.figshare.com/#description_presenters_articlecreate) for article creation (and updating) lists a smaller set of valid "defined_type" values than are actually accepted.
  * Most, if not all, of the "item_type" values listed in the [article search documentation](https://docs.figshare.com/#description_presenters_articlesearch) are also accepted as "defined_type"s (if submitted as lowercase strings, e.g. "chapter" for "15 - Chapter").

Resource DOI:

* Loughborough account appears to be configured to successfully accept "resource_doi"s.
* They must be submitted in the plain DOI format, i.e. without the leading "https://doi.org/" of the URL-formatted version.
  * The Thoth app uses the plain format, but the Thoth API supplies the URL format.
* Invalidly formatted DOIs return an "Invalid DOI format" error and the submission fails.
* To clear an already-submitted DOI value, or otherwise submit an empty DOI, use "" (the empty string) rather than any other null-type value.

Categories:

* As well as the internal Figshare ID allocated to each category ("id" field), there is a "source_id" field representing the category's ID within a specific external standard taxonomy (represented by "taxonomy_id").
  * [Examples in the documentation](https://docs.figshare.com/#private_article_categories_list) give "Anatomy" as ID 300204 within taxonomy 4.
  * There is no indication of which/how many taxonomies are available (300204 looks like an ANZSRC FoR number, but within ANZSRC FoR, this number represents "Agricultural management of nutrients" rather than "Anatomy").
  * For seemingly all the [public categories](https://docs.figshare.com/#categories_list), source_id is listed as "" and taxonomy_id as 10.

Timelines:

* Dates submitted in YYYY-MM-DD format (as supplied by the Thoth API) are successfully accepted, and returned as YYYY-MM-DDT00:00:00.
* It may not be possible to clear an already-submitted date value (as opposed to overwriting it with a new one).
  * Submitting "" does not raise any errors but also does not have any effect (tested on a "publisherPublication" child property which had already been given a value).
  * Submitting an empty "timeline" object (i.e. `"timeline": {}`) also raises no errors but has no effect.
    * `"timeline": {}` is the returned value for articles for which no timeline dates have yet been set.
  * Null-type values are not accepted (either for child properties or for the "timeline" object itself).

Licences:

* The [public licences list](https://docs.figshare.com/#licenses_list) is a subset of the [private licences list](https://docs.figshare.com/#private_licenses_list), so only the latter needs to be checked.
* The public licences lists differ slightly between the main Figshare instance and the Loughborough test instance. On the main instance, entry 1 is listed as "CC BY 4.0". On the test instance, "CC BY 4.0" is entry 50, and entry 1 is listed as "CC BY". The same URL is given for all three.
* Apart from 1 and 50 above, there are no URL clashes in the Loughborough test instance private licence list.
  * We can therefore select the appropriate Figshare licence number by checking the Thoth-stored licence URL against the Figshare list.
* The value of "license" defaults to 1 if not specified.
  * This could result in incorrect licence information being stored, therefore we should always submit a non-default value.
  * We may need to create a private licence with the value "unknown" to handle cases where the Thoth licence field is empty, or the Thoth-stored licence is not found in the Figshare list.
  * Alternatively, we could automatically create a new private licence every time a new Thoth-stored URL is encountered.
  * Currently, Thoth runs no checks on the licence field, other than ensuring it's a valid URL.
* The documentation does not specify how to create a new private licence via the API, or whether this is possible. Figshare support have confirmed that new private licences can only be added by them on request.
  * This may mean every institution with users connecting their Figshare accounts to Thoth will have to manually update their private licences list (to include the "unknown" value or handle each new unlisted licence) in order to avoid incorrect licence information being stored.
    * From their perspective as the partnering repository, Loughborough suggested a workflow where every new publisher was created as a new Figshare "Group", and all required licences were manually bulk-added to the Group at that point (with ad hoc update requests any time a work was added with an unlisted licence). We will need to bear this point of friction in mind when considering how any Thoth-based Figshare integration mechanism would scale to additional publishers/repositories.
* Submitting an invalid "license" value (e.g. 0) does not raise any errors or warnings, but the existing value is not updated.

Fundings:

* Only one of "funding" and "funding_list" can be submitted at a time (if both are provided, the submission fails with an error message stating that they are mutually exclusive).
* Submitting a "funding_list" but not a "funding" results in the "title" of the first item in the "funding_list" also being saved as the "funding" value (overwriting any existing value).
* And vice versa: submitting a "funding" but not a "funding_list" results in the "funding" value also being saved as the "title" of the first item in the "funding_list" (overwriting any existing value).
* "funding_list" "title" value is mandatory, and seemingly any string is accepted.
* Figshare funding structure is less rich than Thoth: Figshare only accepts a string representing a grant number/funding body (either the "funding" value or "funding_list" "title" value), while Thoth optionally stores any/all of grant number, program name, project name and project short name (as well as always storing the funding institution).
  * Not clear which of these should be used as the single Figshare value, or how to appropriately cycle through them if only some are provided.
  * On creation, "funding_list" items are returned with empty "grant_code" and "funder_name" fields, but it is not possible to submit values for these fields.
    * It may be that these are only valid for non-"user_created" fundings. Note the discussion above about Figshare integration with "Dimensions" funding database.
* Every created funding is assigned a new Figshare ID.
  * If a funding has the same value as a previously-created funding, the submission succeeds and a duplicate Figshare record is created (with a new ID).
* Existing "funding" values can be cleared by submitting an empty string ("").
  * This also appears to clear ALL existing "funding_list" values, not just the first one.
* Existing "funding_list" values can be cleared by overwriting the existing set with a new set, or by submitting an empty list ([]) to clear the whole list.

Custom fields:

* New custom fields can be created via the API, although this is a more involved process than for most other objects (<https://docs.figshare.com/#custom_fields> - not tested).
* Custom fields must be defined as specific to particular object types, e.g. Article, Project.

##### File upload

Some file-related actions are accessible from the main Figshare API under the endpoint `/account/articles/{article_id}/files`. These are largely [well-documented](https://docs.figshare.com/#private_article_files) and included in the Swagger version.

* Note that once a file upload has been [initiated](https://docs.figshare.com/#private_article_upload_initiate), there is no way to amend the submitted details, e.g. if an incorrect file "name" or "size" was provided (the endpoint does not support update methods such as `PUT`).
  * Files may be deleted at any point after initiation, so amendments can be done by deletion and recreation.
* The documentation does not list possible file "status" values (found at the [file details](https://docs.figshare.com/#private_article_file) endpoint), but some were found to be:
  * `created`: upload has been initiated but not yet marked as completed
    * Upload completion requests will only succeed if this is the file's current status - resubmitting upload completion requests will fail with a 503 error as the status should already have changed.
  * `available`: upload has successfully been marked completed
  * `ic_failure`: upload completion request was unsuccessful, e.g. the Figshare-calculated MD5 hash of the uploaded file did not match the initially-submitted MD5 hash.
* All well-formed upload completion requests receive a 202 "accepted for processing" response, whether or not the "processing" then succeeds. To confirm that an upload was successful, we must then check the file details endpoint again and confirm that the status has changed to `available`.

File data itself is handled by the Figshare upload API, which is less clearly documented. Some pointers:

* The upload API does not appear to require an authorization token. GET and PUT requests (i.e. both retrieving file details, including potentially sensitive information such as the filename, and submitting file data) succeed with no authentication checks.
  * This is a potential security concern, although a minor one.
    * To access a file's upload endpoint, we need its Figshare-generated randomly-patterned "upload_token" (a 32-character string composed of a combination of digits and the letters a-f), which would be difficult to guess.
    * Any unauthorised file data submissions would probably result in a failure at the upload completion stage, as the MD5 hash is very unlikely to match the initial submission.
* In testing, the upload API root URL (for the test instance) was found to be `https://fup1010100.figsh.com`; it is not clear whether this location is persistent or may change.
* The [documentation](https://docs.figshare.com/#upload_files_uploads_api) suggests that an initiated upload can be cancelled by user request or timeout (receiving the status `ABORTED`). However, it is not clear how the user can do this, or how long the timeout window is.
  * Uploads were still found to have status `PENDING` after remaining inactive for more than 24 hours after initiation.
  * After initiating and then deleting a file from the main endpoint, the file's upload URL was still found to be active with status `PENDING`.
    * It continued to accept file part submissions, even though there was no longer any way to mark the upload as complete, and its file details continued to reference the deleted file ID.
* An initiated upload will show the status `COMPLETED` through the upload API once all parts have been uploaded, even if it is found to have been unsuccessful when checking the main API (e.g. non-matching MD5s).
* File part upload:
  * The [documentation](https://docs.figshare.com/#upload_files_parts_api) does not specify what `Content-Type` header should be used in requests containing binary file part data.
    * The [bash script example](https://docs.figshare.com/#upload_files_example_upload_on_figshare) uses the curl option `--data=binary`, which appears to correspond to `application/x-www-form-urlencoded`, but this may not be a suitable option for large quantities of binary data.
  * Submitting a file Part changes its status from `PENDING` to `COMPLETE`.
    * Resubmitting a file Part when its status is already `COMPLETE` does not produce an error response. On inspection, it seems that the resubmitted data overwrites the previously-submitted data.

The Figshare [example Python upload script](https://docs.figshare.com/#upload_files_example_upload_on_figshare) (as mentioned above) was tested and found to work successfully with a large (multi-part) PDF book file stored locally. Only minor tweaks were required:

* Set appropriate `TOKEN`, `FILE_PATH` and `TITLE` values (replacing example defaults)
* Changed `BASE_URL` to lead to Figshare test instance instead of main instance
* Changed python2-style `print ''` statements to python3-style `print('')` statements
  * Script was run as python3, as running it as python2 failed to find the required external module `requests`. This was probably due to local settings and could have been resolved manually, but this was the easier solution.

File type considerations:

* Figshare accepts all uploads as binary data and streams the received data directly to storage as-is. This presumably means that any file type is accepted, although there may be limits on which formats Figshare is able to display/preview in addition to providing for direct download. It may also mean that corrupted data is not detected (if it was already corrupted before the upload process began).
* Figshare handles zip files reasonably well: files included within a zip file cannot be previewed within the user interface, but Figshare is able to display a tree of the zip file's contents, including all file names. This is acceptable for many purposes, e.g. checking whether all expected files are present/users deciding whether they want to go on to download the file.
  * OBP XML publications can be accessed via a direct link as a zip file, which contains separate XML files for each chapter (unlike e.g. the single-file PDF version). We could either attempt to unpack these and upload each XML file separately (matching the previous manual testing), or settle for uploading the single zip file as-is.

##### Projects

Following the initial work submitting Thoth Works in Figshare Article format, a brief investigation was carried out into submission of Thoth Works in Figshare Project format, with child Publications represented as child Articles. (A partially-working proof of concept was committed under [f3e0eda](https://github.com/thoth-pub/thoth/commit/f3e0edaef112ba1c1740ffa77addc52a90e62a3d) and then reverted.) Some findings are as follows:

* Basic Project/Articles creation was successful.
  * As noted, Projects have limited metadata, so this was mitigated by adding all available Work metadata to every Article object.
  * For identification purposes, an Article "custom field" was again used, this time to store the Thoth Publication ID. The Loughborough test instance does not currently have any Project "custom fields", but if one were set up, it could be used to store the Thoth Work ID.
  * To associate an Article with a Project, it must be created via the endpoint `/account/projects/{project_id}/articles`. It does not seem to be possible to associate an Article with a Project after it has already been created. There is no indication within an Article's metadata as to whether it is associated with a Project; this information is only stored under the Project.
  * The endpoint `/account/projects/{project_id}` does not display a Project's Articles; these must be retrieved separately from `/account/projects/{project_id}/articles` (note for comparison that retrieving an Article includes its Files).
  * Projects have a "collaborators" property, indicating which Figshare users are associated with the Figshare Project (as distinct from authorship of the Project materials themselves). On creation, the logged-in user is automatically set as the sole collaborator. Collaborators cannot be set directly on the Project; they can only be invited to it, or leave it.
* Updating existing Articles under Projects raises more points of consideration.
  * Note that Articles cannot be updated via the `/account/projects/{project_id}/articles/{article_id}` endpoint, only viewed. Updates must be done via `/account/articles/{article_id}` (the article_id is the same for both). This was tested successfully.
  * As a Project (Work) may have multiple Articles (Publications), care must be taken over workflow. This reflects a broader point which also has a bearing on e.g. file upload (with multiple files/multiple parts). It is sensible for code which interacts with an API to be "asynchronous", i.e. instead of pausing every time it sends a request and waiting until the response is returned (which may take some time), it continues working on other things and goes back to deal with the response when it arrives. However, if it has sent multiple similar requests in succession (e.g. to upload multiple file parts), it then needs a way to work out which response corresponds to which object (e.g. which file part), if further object-specific processing is needed.
    * The Thoth GraphQL API makes this quite easy as you can specify which object properties you want to receive in the response. However, the Figshare API responses are pre-defined, and do not always contain information which would be useful in this respect. For example, the response to a file part upload attempt only specifies "success" or "failure" - it does not indicate *which* file part was being uploaded.
    * The original code submitting a Work as an Article only needed to track a single object, and so this could be done by saving off its article_id and referring back to it when needed. However, this needs to be adapted if handling multiple Articles at once.
  * Not all Article properties are displayed at the `/account/projects/{project_id}/articles` endpoint; for example, "custom_fields" can only be retrieved via `/account/projects/{project_id}/articles/{article_id}`.
    * This is a drawback of relying on a custom field to store the publication_id mapping: we cannot obtain the publication_ids of all existing Articles in a single API call (for purposes of checking which already exist and which need to be created).
      * Custom fields also do not appear in article search responses.
    * Although the Swagger documentation specifies that only the ArticleComplete and ArticleCompletePrivate objects have the "resource_doi" property, in testing, the Article objects displayed at the `/account/projects/{project_id}/articles` endpoint appeared to show them. It may be that the property is only displayed if the institution's settings support it, and this is not easy to represent in the schema.
* We need to determine the workflow if the Publication corresponding to an existing Article is later deleted - i.e. whether we simply ensure that an Article exists for every Publication found, or instead ensure that the Project's Article list exactly matches the Work's Publication list. Again, this raises a broader point: the original code had no mechanism for deleting the corresponding Figshare record if a Thoth Work was deleted. We should consider how the requirement for an up-to-date record overlaps with the requirement for full preservation (see also the earlier discussion of clearing metadata fields if they were overwritten in Thoth after initial submission).
  * We have not yet determined at what point in a book's lifecycle we would submit it to Figshare - if we decide it would be a single one-off submission rather than a process of iterative updates, many of these concerns become moot.

#### Technical considerations (Thoth)

Work was based on the model of existing HTTP calls between the Thoth app and the Thoth GraphQL API (server retrieving metadata from central database). This resulted in some limitations:

* All Thoth API endpoints operate solely using JSON bodies: inbound HTTP requests contain a JSON body outlining the data fields which are being queried/submitted, and outbound HTTP responses contain a JSON body representing the data which was requested/updated.
  * Figshare API requires/produces a wider variety of HTTP calls. Some require a JSON body in the request but will return a plain text response. Some (e.g. file upload) require a request with a binary data body. Some responses contain success/error information in the JSON body, but others only indicate success/error via the HTTP status code (e.g. 200 OK, 401 Unauthorized).
  * The existing Thoth HTTP calls are made using a [Rust module](https://docs.rs/crate/yewtil/0.4.0/source/src/fetch/request.rs) which handles JSON bodies well but appears to have limited support for other patterns.
* Situating all the logic within the browser-based app made it challenging to retrieve files for onward upload to Figshare. The Thoth app does not currently have any file-related capabilities (with good reason):
  * Many Thoth records contain the direct links to e.g. PDF versions of the relevant publication which are publicly browsable and downloadable, and the initial assumption was that the new code could download files from these links and then send them onwards to Figshare. However, [web standards](https://web.dev/same-origin-policy/) mean that browser-based apps are limited in what resources they can retrieve via HTTP calls (a safety feature to avoid attacks from malicious apps). The Thoth app can retrieve data from the Thoth and Figshare APIs because these are public APIs which have given explicit permission for browser-based apps to interact with them. However, online publication files are usually not hosted at public APIs, so cannot be accessed from within the Thoth app.
    * As discussed above, it was suggested that we could upload full metadata files to Figshare to expand on the set of metadata fields supported by the Figshare interface. Potentially appropriate files (in e.g. ONIX and CSV formats) are created by the Thoth Export API (by taking data from the Thoth GraphQL API and reformatting it). However, unlike the Thoth GraphQL API, the Thoth Export API is not public and cannot be accessed by browser-based apps.
  * The Thoth app is written in Rust compiled to [WebAssembly](https://webassembly.org/), a format which does not allow the app to access the user's file system directly (a safety feature to avoid attacks from malicious apps). It would be possible to implement a standard file upload dialog box, through which the user could manually give the app permission to access a selected file and send it onwards to Figshare. However, this would require adding a JavaScript component and connecting it to the Rust code, which would be time-consuming.

A preferable long-term structure would be for the HTTP calls to the Figshare API/to online publication file links to be made within a separate server (non-browser-based), activated by requests being sent from the Thoth app (and/or, potentially, as a regular scheduled automatic process).

* Upcoming work on the main Thoth development path will include the creation of relevant new components, such as a generic service for automated retrieval/distribution of publication files (for which the Figshare file upload process could be a test case). Once this is in place, the prototype logic could be moved or recreated there.

We may also want to consider whether any long-term software-based solution would work best as an integrated component of Thoth (i.e. only available for publishers who are members of Thoth, and possibly only accessible via the Thoth app admin login), or as a standalone app/service (or both!).

* Metadata format used in Thoth app is based on JSON data retrieved from Thoth API. Current logic could potentially be adapted to work on any JSON data submitted in the same format as produced by the Thoth API (e.g. via CSV to JSON conversion).