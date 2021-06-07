The [San Francisco Declaration on Research Assessment](https://sfdora.org/read/) (DORA) sets out a wide-ranging set of recommendations to all actors within the research landscape.

Specifically, the DORA declaration includes the recommendations for publishers below. 

> ### For publishers

> 6. Greatly reduce emphasis on the journal impact factor as a promotional tool, ideally by ceasing to promote the impact factor or by presenting the metric in the context of a variety of journal-based metrics (e.g., 5-year impact factor, EigenFactor [8], SCImago [9], h-index, editorial and publication times, etc.) that provide a richer view of journal performance.

> 7. Make available a range of article-level metrics to encourage a shift toward assessment based on the scientific content of an article rather than publication metrics of the journal in which it was published.

> *8. Encourage responsible authorship practices and the provision of information about the specific contributions of each author.*

> 9. Whether a journal is open-access or subscription-based, remove all reuse limitations on reference lists in research articles and make them available under the Creative Commons Public Domain Dedication [10].

> 10. Remove or reduce the constraints on the number of references in research articles, and, where appropriate, mandate the citation of primary literature in favor of reviews in order to give credit to the group(s) who first reported a finding.

In particular point 8 seems relevant for Thoth, namely the clear acknowledgment of the authors of the metadata records produced in Thoth. Currently, ONIX records output in Thoth only list the "sender" in the header, with incorrect email address:

```
<ONIXMessage release="3.0">
<Header>
<Sender>
<SenderName>punctum books</SenderName>
<EmailAddress>javi@openbookpublishers.com</EmailAddress>
</Sender>
<SentDateTime>20210607T113458</SentDateTime>
</Header>
<Product>
```

Suggestion would be to link the sender data to the account that created the metadata record that is being output. Though multiple user accounts may work on the same metadata record, this would at least give a better approximation of authorship acknowledgment and potentially make Thoth records DORA compliant.



