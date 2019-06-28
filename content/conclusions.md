## Conclusions
{:#conclusions}

Intelligent clients that enable querying over hypermedia interfaces such as TPF
require metadata *detection*, *extraction*, and *shaping*.
Ad hoc metadata extraction processes perform each of these steps separately,
by manually detecting predicates,
extracting matching triples into a temporary index,
and reshaping the relevant parts of the index in a more convenient datastructure.
As shown in this article, query-based metadata extraction allows these three steps to be performed automatically
by recursively invoking the query engine on a subset of the RDF response.

Moving from ad hoc metadata extraction towards a query-based metadata extraction
comes with the main advantage that the implementation of the extraction modules
is significantly less complex, as the module contains not much more than just a GraphQL-LD query.
This significantly lowers implementation effort and reduces chances of potential bugs.
On the other hand, preliminary evaluation shows that query-based metadata extraction introduces a 10~20% overhead
compared to ad hoc metadata extraction in Comunica.
Profiling shows that the main bottleneck lies within the recursive invocation of Comunica.

This shows that abstraction comes at the cost of reduced performance.
As such, there is a trade-off between development efficiency and execution efficiency.
Since Comunica's main purpose is *flexibility*, and not *efficiency*, this is not a problem.
Nevertheless, both the query-based and ad hoc metadata extraction modules are both available,
where the former can be used for quick prototyping when performance is less important,
and the latter can be used in performance-sensitive production environments.
