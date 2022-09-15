An OAI (Open Archives Initiative) Identifier is a unique identifier of a metadata record defined in the
Open Archives Initiative Protocol for Metadata Harvesting (OAI-PMH) specification. `http://www.openarchives.org/OAI/2.0/guidelines-oai-identifier.htm
`

The adoption of OAI-PMH across repositories is these days nearly ubiquitous. The OAI Identifiers consist of a globally unique prefix identifying the repository and a suffix that is locally unique to a given metadata record in the repository. This makes OAI Identifiers globally unique without the need for a central registration entity. CORE has built a global resolver for OAI identifiers at `https://core.ac.uk/oai_resolver` . The RESTful call
to resolve an OAI is: `https://oai.core.ac.uk/oai:zzz:yyy` . 

These may be used as PIDs by repositories hosting, for example, Author Accepted Manuscripts which may vary from the published Version of Record - that will link the AAM to the VoR without minting a new DOI. More info: `https://core.ac.uk/resources/oai-identifiers-and-resolver-2022.pdf`
