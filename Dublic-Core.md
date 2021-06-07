[Dublin Core](https://dublincore.org/) defines a set of 15 "core" metadata elements for the description of digital resources. Dublin Core has been standardized as [ISO 15836](https://www.iso.org/standard/71339.html).

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

All 15 elements are covered by the metadata schema underlying Thoth and therefore Thoth should be able to output Dublin Core data in which language required.

The way in which Dublin Core elements are encoded has not been specified. Here is an example provided by the [LOC](http://lcweb2.loc.gov/ammem/award/docs/dublin-examples.html) in SGML:

```
<!DOCTYPE dublinCore PUBLIC '-//OCLC//DTD Dublin core v.1//EN'>
<dublinCore>
  <title>[Portrait of Zora Neale Hurston]</title>
  <author type='photographer'>Van Vechten, Carl</author>
  <otherAgent type='digitizer'>Any Library</otherAgent>
  <subject scheme='gmgpc'>Portrait Photographs</subject>
  <objectType>image</objectType>
  <form scheme='IMT'>image/jpeg</form>
  <relation type='ammemParent'>vanv</relation>
  <identifier type='URN'>hdl:loc.pp.vanv/5a52142</identifier>
</dublinCore>
```

A different example from [Wikipedia](https://en.wikipedia.org/wiki/Dublin_Core), following the encoding suggested by [this users' guide](https://paladini.github.io/dublin-core-basics/): 

```
    <meta name="DC.Format" content="video/mpeg; 10 minutes" />
    <meta name="DC.Language" content="en" />
    <meta name="DC.Publisher" content="publisher-name" />
    <meta name="DC.Title" content="HYP" />
```




