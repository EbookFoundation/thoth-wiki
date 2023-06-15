SWORD is a standardised web protocol by which repository users' computers (clients) can "talk to" online repositories (servers). Variants of it are used by many archiving and repository services, such as [EPrints](https://github.com/thoth-pub/thoth/wiki/EPrints) and [DSpace](https://github.com/thoth-pub/thoth/wiki/DSpace).

Interaction with a SWORD-based repository is done using HTTP calls (similarly to interaction with the [Figshare](https://github.com/thoth-pub/thoth/wiki/Figshare) API, or the Thoth APIs). The SWORD protocol describes the structure that these HTTP calls should take. There is some flexibility within the protocol, so individual repository services are free to implement certain aspects of it in different ways, or not at all.

## Main details

The basic elements of the protocol are standard for an HTTP API: clients can e.g. GET from or POST to specific URLs in order to read or write repository files. When writing data, the body of the HTTP request contains the content to be written (perhaps a book file, or perhaps its accompanying metadata). Specific headers in the HTTP request indicate to the server how the request should be processed, e.g. the format of the content being submitted. The protocol also determines the format in which the server will return HTTP responses.

A major change occurred in the move from SWORD version 2.0 to SWORD version 3.0. Version 2.0 was based on the Atom Publishing Protocol, in which HTTP request/response bodies are formatted as XML. Version 3.0 drops Atom in favour of a JSON-based format. Some repositories, such as those based on the default EPrints configuration, still use version 2.0. When determining how to prioritise SWORD work, we should review the balance of repositories using v2.0 vs v3.0, as we may decide it is worth focusing on integration with one to the exclusion of the other.

Our main focus will be the submission of metadata, as we want to ensure this is structured correctly and as rich as possible. In both v2.0 and v3.0, the available default metadata categories are based on the Dublin Core schema. This overlaps well with the Thoth schema and is commonly used elsewhere (e.g. DOAB). Note servers can optionally be configured to also accept other metadata formats, such as MODS XML.

Accepted data file types may vary by server, but in v3.0, as a minimum they must include binary, zip, and the [SWORD implementation of BagIt](https://github.com/swordapp/swordv3/blob/master/docs/SWORDBagIt.json). Specifications for v2.0 are less clear, but suggest that all of the above types are potentially supported, with only zip being mandatory.

## SWORD client libraries

The SWORD project makes available a number of open-source resources for easily implementing integrations with the protocol. These include fully-featured Python client libraries for both [version 2.0](https://github.com/swordapp/python-client-sword2) and [version 3.0](https://github.com/swordapp/sword3-client.py), although (unsurprisingly) no Rust libraries. These libraries provide Python methods which abstract out the specifics of the protocol, allowing the programmer to e.g. create a basic metadata object by simply setting the value of a "title" argument; this will then generate correctly-formatted HTTP calls in either Atom XML (for v2.0) or JSON (for v3.0).

As Thoth is written in Rust, which supports the inclusion of Python modules, and as it too has a [Python client library](https://github.com/thoth-pub/thoth-client/), the SWORD Python libraries are good candidates for providing SWORD support within Thoth.

### Thoth integration: initial tests

Brief investigation of both the SWORD Python libraries showed that they installed successfully (via `pip`) and broadly worked as described in the (sometimes patchy) documentation. Although the v2.0 library documentation suggests it only works within Python 2.7, it was installed and ran successfully within Python 3.

The v3.0 library could not be tested against any repository servers, but metadata objects were successfully created locally. Of note, it is not immediately clear from the documentation (unlike for v2.0) how to supply authentication credentials for a server. If we obtain access to any repository using the SWORD v3.0 protocol, this will need to be resolved in order to test interaction with it.

#### EPrints

The v2.0 library was successfully used to upload both metadata and small files (e.g. one-page PDFs) to the Bath Spa EPrints instance. Success was confirmed by viewing the deposits in the GUI and redownloading them. An attempt to upload a larger PDF book file (\~50MB) failed due to a time-out during local processing of the data. This may have been the result of a misconfiguration, e.g. the Python 2.7 vs Python 3 issue; further investigation will be required in order to deposit standard-size content files.

#### DSpace

Following the successful test of the Bath Spa EPrints instance, a similar investigation was carried out on a test instance of the Cambridge Library "Apollo" system, which was at the time using DSpace v6 (SWORD v2). Brief testing with the SWORD v2.0 Python library (as above) resulted in successful creation of a basic metadata record (publicly viewable), within a dedicated collection set up for our testing.

### Thoth integration: full implementation

Following these tests, the SWORD v2.0 Python library was later used as the basis for the SWORD v2 module in the Python-based [Thoth Dissemination Service](https://github.com/thoth-pub/thoth-dissemination/).