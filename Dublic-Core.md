[Dublin Core](https://dublincore.org/) defines a set of 15 "core" metadata elements for the description of resources. Dublin Core has been standardized as [ISO 15836](https://www.iso.org/standard/71339.html).

The following [15 elements](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/#section-3) form the Dublin Core:

* contributor
* coverage
* creator 
* date
* description
* format
* identifier
* language
* publisher
* relation
* rights
* source
* subject
* title
* type

The way in which Dublin Core elements are encoded has not been specified. Here is an example provided by the LOC:

`<!DOCTYPE dublinCore PUBLIC '-//OCLC//DTD Dublin core v.1//EN'>
<dublinCore>
  <title>[Portrait of Zora Neale Hurston]</title>
  <author type='photographer'>Van Vechten, Carl</author>
  <otherAgent type='digitizer'>Any Library</otherAgent>
  <subject scheme='gmgpc'>Portrait Photographs</subject>
  <objectType>image</objectType>
  <form scheme='IMT'>image/jpeg</form>
  <relation type='ammemParent'>vanv</relation>
  <identifier type='URN'>hdl:loc.pp.vanv/5a52142</identifier>
</dublinCore>`

