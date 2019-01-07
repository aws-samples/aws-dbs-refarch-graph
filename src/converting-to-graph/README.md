# Converting Other Data Models to a Graph Model

As described in [Overview of the Design Process](../graph-data-modelling#overview-of-the-design-process), when building a graph database application it is best to design an application graph data model and graph queries by working backwards from a set of application use cases, and using the model as a target for any subsequent data ingest from other systems.

However, you may sometimes need to take data from another data technology and ingest it into a graph database prior to undertaking any explicit application-specific graph data modelling. In these circumstances you can apply a number of 'mechanical' transformations that yield a naive graph model. This model will not necessarily be optimised for specific use cases and queries, but it can provide the basis for exploration and the iterative development of an application graph data model.
