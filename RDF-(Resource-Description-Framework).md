https://www.w3.org/TR/rdf11-primer/

Note: The Wellcome Library has created RDF-XML, Turtle, N-Tuple files for all OBP titles eg https://wellcomelibrary.org/item/b28462312#?c=0&m=0&s=0&cv=0


The Resource Description Framework (RDF) is a framework for expressing information about resources. Resources can be anything, including documents, people, physical objects, and abstract concepts.

RDF is intended for situations in which information on the Web needs to be processed by applications, rather than being only displayed to people. RDF provides a common framework for expressing this information so it can be exchanged between applications without loss of meaning. Since it is a common framework, application designers can leverage the availability of common RDF parsers and processing tools. The ability to exchange information between different applications means that the information may be made available to applications other than those for which it was originally created.

In particular RDF can be used to publish and interlink data on the Web. For example, retrieving http://www.example.org/bob#me could provide data about Bob, including the fact that he knows Alice, as identified by her IRI (an IRI is an "International Resource Identifier"; see Sec. 3.2 for details). Retrieving Alice's IRI could then provide more data about her, including links to other datasets for her friends, interests, etc. A person or an automated process can then follow such links and aggregate data about these various things. Such uses of RDF are often qualified as Linked Data

Specifications of serialization formats for RDF:
Turtle [TURTLE] and TriG [TRIG]
JSON-LD [JSON-LD] (JSON based)
RDFa [RDFA-PRIMER] (for HTML embedding)
N-Triples [N-TRIPLES] and N-Quads [N-QUADS] (line-based exchange formats)
RDF/XML [RDF11-XML] (the original 2004 syntax, updated for RDF 1.1)

