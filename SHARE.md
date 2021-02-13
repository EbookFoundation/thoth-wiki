SHARE is an open-source community developing tools and services to connect related research outputs for new kinds of scholarly discovery. Their meta-search includes >1.3 mio. OA books.

The [SHARE infrastructure](https://github.com/CenterForOpenScience/SHARE) was developed by the [Association of Research Libraries](http://www.arl.org/) in partnership with the [Center for Open Science](http://cos.io/). SHARE is funded by the [Institute of Museum and Library Services](http://www.imls.gov/) and the [Alfred P. Sloan Foundation](http://www.sloan.org/). The SHARE initiative was founded in 2013 by ARL, the Association of American Universities (AAU), and the Association of Public and Land-grant Universities (APLU). 

SHARE's data exchange points include:

* an elasticsearch API endpoint at https://share.osf.io/api/v2/search/creativeworks/_search
   * doc at https://share-research.readthedocs.io/en/latest/elasticsearch.html
* API Endpoints for accessing transformed metadata: https://share.osf.io/api/v2
* Overall documentation: https://share-research.readthedocs.io/en/latest/

It seems that data can be pushed directly into the SHARE database via a "subset of JSON-LD graphs" (see [doc here](https://share-research.readthedocs.io/en/latest/share_api.html#push-data-directly-into-the-share-database)). 