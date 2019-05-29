# RDF Data Modelling

TODO

## Using Edges to Facilitate Efficient Graph Queries

The performance of a graph query depends on how much of the graph the query has to 'touch' in order to generate a set of results. The larger the working set, the longer it will take to get from storage and then traverse once it has been cached in main memory.

![Large Query](large-query.png)

You can ensure your queries touch the minimum amount of data by naming predicates in a way that allows the query engine to follow only those relationships relevant to the query being executed. 

![Small Query](small-query.png)

Predicate compose and partition the graph. By connecting vertices, they structure the whole, creating a complex composite from what would otherwise be simple islands of data. At the same time they serve to partition the graph, differentiating connections between elements based on name, direction and property values so that queries can identity specific subgraphs within a larger, more variably connected structure. By focussing your queries on certain predicates and the paths they form, you allow the query engine to exclude irrelevant parts of the graph from consideration, effectively materializing a particular view of the graph dedicated to addressing a specific query need.

### Predicate names

Derive your predicates from your use cases. Doing so helps structure and partition your data so that queries ignore triples that have no bearing on the working set necessary to satisfy the query.

### Bi-directional relationships

If you need to model bi-directional relationships, you will have to add pairs of predicates.

![Bi-Directional Relationships](bi-directional-relationships.png)

```
PREFIX j: <http://www.example.com/jobs#>

INSERT
{
    j:p-1 j:worksWith j:p-2 .
    j:p-2 j:worksWith j:p-1 .
}
WHERE {}
```

### Uni-Directional relationships

The directed nature of edges naturally lends itself to expressing uni-directional relationships.

![Unit-Directional Relationships](uni-directional-relationships.png)

In SPARQL:

```
PREFIX s: <http://www.example.com/social#>

SELECT ?followees WHERE {
    s:p-1 s:follows ?followees
}
```

and:

```
PREFIX s: <http://www.example.com/social#>

SELECT ?followers WHERE {
    ?followers s:follows s:p-1
}
```

### Multiple relationships between nodes

With RDF you can connect any pair of nodes with multiple relationships with different names. Connecting a pair of nodes with multiple relationships with the same name is slightly more complicated. RDF does not have a concept of relationship identity that would serve to distinguish predicate instances. To connect a pair of nodes with multiple relationships with the same name you will have to introduce intermediate nodes, one per instance of the relationship.

![Multiple Relationships](multiple-relationships.png)




