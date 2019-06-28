## Conclusions
{:#conclusions}

Clients that enable querying over hypermedia interfaces such as TPF
require metadata *detection*, *extraction*, and *shaping*.
Ad hoc metadata extraction performs each of these steps separately,
while query-based metadata extraction allows these steps to be performed
by recursively invoking the query engine on a subset of the RDF response.

Moving from ad hoc metadata extraction towards a query-based metadata extraction
comes with the main advantage that the implementation of the extraction modules
is significantly less complex, which lowers implementation effort.
On the other hand, preliminary evaluation shows that query-based metadata extraction introduces a 10~20% overhead
compared to ad hoc metadata extraction in Comunica.
The main bottleneck lies within the recursive invocation of Comunica.

Our preliminary results shows that abstraction comes at the cost of reduced performance,
so there is a trade-off between development efficiency and execution efficiency.
Since Comunica's main purpose is *flexibility*, and not *efficiency*, reduced performance is not a problem.
Nevertheless, both the query-based and ad hoc modules are available,
where the former can be used for quick prototyping when performance is less important,
and the latter can be used in performance-sensitive environments.
