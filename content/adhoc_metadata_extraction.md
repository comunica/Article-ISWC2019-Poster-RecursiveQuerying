## Ad hoc Metadata Extraction
{:#adhoc_metadata_extraction}

In order to enable querying over TPF interfaces,
the Comunica query engine detects and extracts metadata from RDF responses through two modules,
which will be discussed in more detailed hereafter:

* [**Hydra Count Extractor**](https://github.com/comunica/comunica/tree/master/packages/actor-rdf-metadata-extract-hydra-count): Extracts cardinality estimates.
* [**Hydra Controls Extractor**](https://github.com/comunica/comunica/tree/master/packages/actor-rdf-metadata-extract-hydra-controls): Extracts URL templates with variable mappings.

### Hydra Count Extractor

TPF interfaces expose cardinality estimates for the current fragment via the `hydra:totalItems` predicate.
This allows client-side engines to determine an efficient join order between the different triple patterns of a SPARQL query.
[](#data-count) shows an example of this count metadata.

Due to the simplicity of this data shape,
the Hydra Count Extractor module simply iterates over the triples (or quads),
and finds the cardinality in the triple object
once the `hydra:totalItems` predicate is found.
This implementation can be found on [GitHub](https://github.com/comunica/comunica/blob/master/packages/actor-rdf-metadata-extract-hydra-count/lib/ActorRdfMetadataExtractHydraCount.ts){:.mandatory}.

<figure id="data-count" class="listing">
````/code/data-count.ttl````
<figcaption markdown="block">
Part of the metadata from http://fragments.dbpedia.org/2016-04/en in TriG
that declares the cardinality estimate with the `hydra:totalItems` predicate.
</figcaption>
</figure>

### Hydra Controls Extractor

TPF interfaces expose their triple pattern search form via [Hydra templated links](http://www.hydra-cg.com/spec/latest/core/#templated-links){:.mandatory}.
This allows client-side engines to determine what kind of queries can be sent to the interface (triple pattern queries in this case),
and how the query should be encoded into the URL.
[](#data-templatedlinks) shows an example of this templated link metadata.

This data shape is significantly more complex than the previous one for counts.
That is why the Hydra Controls Extractor module consists of a non-trivial implementation.
This module iterates over the triples (or quads), and detects all predicates that start with the `hydra:` prefix.
For all triples with Hydra predicates, an in-memory triple index is maintained in the order of _predicate_, _subject_, _object_.
Once all triples have been read, the index is read to find all objects for the `hydra:search` predicate,
which gives us all search form identifiers.
Next, the index is traversed for all `hydra:mapping` predicates and search form identifies as subjects,
to find all mapping identifiers for each search form.
Next, for each mapping, the index is traversed for `hydra:variable` and `hydra:property` predicates with mapping identifiers as subjects,
to find their respective values.
Finally, all discovered values are collected and saved in a convenient search form datastructure
that can be used by other modules in the further querying process.
This implementation can be found on [GitHub](https://github.com/comunica/comunica/blob/master/packages/actor-rdf-metadata-extract-hydra-controls/lib/ActorRdfMetadataExtractHydraControls.ts){:.mandatory}.

<figure id="data-templatedlinks" class="listing">
````/code/data-templatedlinks.ttl````
<figcaption markdown="block">
Part of the metadata from http://fragments.dbpedia.org/2016-04/en in TriG
that declares the Hydra templated link to execute a triple pattern query.
</figcaption>
</figure>
