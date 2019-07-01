## Query-based Metadata Extraction
{:#querybased_metadata_extraction}

Due to the complexity of ad hoc metadata extraction,
we introduce a query-based metadata extraction process inside the Comunica query engine.
We write the queries using [GraphQL-LD](cite:cites taelman_iswc_demo_graphqlld_2018) instead of SPARQL because:

1. Queries are *compact* because *IRIs are hidden* behind a JSON-LD context.
2. Results corresponds to *query shape*, removing the need for *post-processing*.

[](#query-count) and [](#query-templatedlinks) show the
GraphQL-LD queries that respectively achieve the same task as
the Hydra Count Extractor and Hydra Controls Extractor modules in Comunica.
[](#query-context) shows the JSON-LD context to expand query terms to IRIs.

Both queries are precompiled to reduce runtime overhead as much as possible.
Before query execution, the `$pageUrl` variables in these queries are bound to the actual TPF page URL that is being requested,
so that the proper metadata will be extracted.
In order to execute the queries, a temporary in-memory indexed triple store is created
over which Comunica is able to execute these GraphQL-LD queries.
Since the query shape directly corresponds to the data shape that is expected within Comunica's metadata datastructure,
minimal post-processing is needed once the results are available.
Furthermore, since GraphQL-LD exploits JSON-LD's `@type` feature for mapping RDF literal datatypes to JavaScript primitives,
we don't need to manually transform between datatypes for fields such as the numerical `totalItems`.

<!--TODO: show after accept-->
<!--The implementation of these query-based metadata extraction module can be found on [GitHub](https://github.com/comunica/comunica/blob/refactor/metadata/packages/){:.mandatory} in the `actor-rdf-metadata-extract-hydra-count-query` and `actor-rdf-metadata-extract-hydra-controls-query` packages.-->

<figure id="query-context" class="listing">
````/code/query-context.txt````
<figcaption markdown="block">
JSON-LD context for expanding terms in GraphQL-LD queries.
</figcaption>
</figure>

<div>
<figure id="query-count" class="listing" style="width: 40%; display: block-inline; float: left">
````/code/query-count.txt````
<figcaption markdown="block">
GraphQL-LD query for extracting cardinality estimates.
</figcaption>
</figure>

<figure id="query-templatedlinks" class="listing" style="width: 40%; display: block-inline; float: right">
````/code/query-templatedlinks.txt````
<figcaption markdown="block">
GraphQL-LD query for extracting templated links.
</figcaption>
</figure>

<br style="clear: both" />
</div>
