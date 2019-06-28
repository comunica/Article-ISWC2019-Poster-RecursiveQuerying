## Introduction
{:#introduction}

Linked Data is published via different kinds of Web interfaces,
such as SPARQL endpoints,
Linked Data documents,
or [Triple Pattern Fragments (TPF)](cite:cites ldf).

TPF is a *self-descriptive* hypermedia interface
that exposes *metadata* to allow intelligent clients to detect how the interface can be used.
TPF metadata contains a triple pattern query form
that is described with the [Hydra Core vocabulary](cite:cites hydra) in RDF.
Intelligent hypermedia-based clients such as [Comunica](cite:cites taelman_iswc_resources_comunica_2018)
are able to detect and interpret this metadata
to enable SPARQL queries over one or more TPF interfaces.
For this, the client splits up the SPARQL query into multiple triple pattern queries,
that are then executed by the TPF interface, and joined client-side.

Hypermedia-based clients extract metadata
by iterating over triples in the HTTP response and matching specific predicates,
which is hard to implement for complex metadata shapes.
This *ad hoc metadata extraction* is essentially a manual querying process.
Since we are using a hypermedia-based query engine,
its querying capabilities could be reused to achieve *query-based metadata extraction*.
Instead of manually implementing logic to extract metadata,
this logic can be replaced with a single query.

In this article, we discuss the ad hoc metadata extraction process
within the Comunica query engine in [](#adhoc_metadata_extraction).
After that, we introduce a query-based metadata extraction process for Comunica in [](#querybased_metadata_extraction).
Finally, we conclude in [](#conclusions).
