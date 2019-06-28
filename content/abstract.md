## Abstract
<!-- Context      -->
Linked Datasources can be exposed through hypermedia-based interfaces such as Triple Pattern Fragments.
When intelligent clients query over such interfaces,
they need to extract controls from their metadata.
<!-- Need         -->
This extraction process typically happens by manually iterating over the RDF triples,
which is hard to implement for complex control shapes.
<!-- Task         -->
Since hypermedia-based query engines already have querying capabilities at their disposal,
this *extraction* process can be simplified through a *single declarative query*.
<!-- Object       -->
In this article, we implement and test this simplification using GraphQL-LD queries.
<!-- Findings     -->
We show that this *query-based* metadata extraction process reduces implementation effort
at the cost of a slight increase in overhead during query execution.
<!-- Conclusion   -->
As such, there is a *trade-off* between *development* efficiency and *execution* efficiency.
<!-- Perspectives -->

