## Introduction
{:#introduction}

[Linked Data](cite:cites linkeddata) is published via different kinds of Web interfaces,
such as [SPARQL endpoints](cite:cites spec:sparqlprot),
[Linked Data documents](cite:cites LinkedDataPrinciples),
or [Triple Pattern Fragments (TPF)](cite:cites ldf).

TPF is a hypermedia interface that follows the [REST principles](cite:cites rest) by being *self-descriptive*.
This allows intelligent clients to discover *metadata* about the source,
such as how the interface can be *controlled*,
and the *estimated cardinality* of the data fragment.
In the case of TPF, this control is a paged triple pattern query form
that is described with the [Hydra Core vocabulary](cite:cites hydra) in [RDF](cite:cites spec:rdf).
Intelligent hypermedia-based clients such as [Comunica](cite:cites taelman_iswc_resources_comunica_2018)
are able to detect and interpret this metadata
to enable [SPARQL queries](cite:cites spec:sparqllang) over one or more TPF interfaces.
For this, the client must split up the SPARQL query into multiple smaller triple pattern queries.
These triple pattern queries can be executed by the TPF interface,
after which their results can be joined together client-side.

To the best of our knowledge, all hypermedia-based clients extract this metadata in an ad hoc way.
Concretely, the RDF triples contained in the HTTP response are parsed, and iterated over.
When specific predicates are detected --such as `hydra:totalItems` for cardinality estimates--,
the object value is extracted and stored in a metadata object for later use.
While this method works well for simple metadata shapes --such as cardinality estimates--,
it becomes harder for more complex metadata shapes --such as variable mappings within URL templates--.

This *ad hoc metadata extraction* is essentially a manual querying process.
Since this process is typically part of a hypermedia-based query engine,
the querying capabilities of the engine could be reused to achieve *query-based metadata extraction*.
Instead of manually implementing logic to extract metadata,
this logic can be replaced with a single query.

In this article, we discuss the ad hoc metadata extraction process
within the Comunica query engine in [](#adhoc_metadata_extraction).
After that, we introduce a query-based metadata extraction process for Comunica in [](#querybased_metadata_extraction).
Finally, we conclude in [](#conclusions).
