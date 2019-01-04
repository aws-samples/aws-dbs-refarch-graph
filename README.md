__Graph Database__ workloads are operational and business intelligence database workloads that store and query highly connected data. 

Key characteristics of a graph database workload include:

  * Data volumes are expected to comprise many millions or billions of items and relationships.
  * Data can change frequently, with additions and changes to items and connections made available to clients less than a second after having been made durable.
  * Queries begin by finding one or more starting points in the graph, and then explore the neighbouring portions of the graph in order to discover connected items or compute results as they traverse the paths that connect items, with subsecond response times.
  * Items may exhibit variable schema, insofar as two items of the same type may not necessarily share the exact same set of attributes.
  * Items may be connected to one another in many different ways, with no two pairs of items necessarily connected in the exact same way.

Data workloads in which data items are implicitly or explicity connected to one another can be implemented using a wide range of relational and non-relational technologies, but in situations where the data is not only highly connected but also the queries addressed to the data exploit this connected structure, there are many design, development and performance benefits to using a graph database optimized for graph workloads.

[Amazon Neptune](https://aws.amazon.com/neptune/) is a fast and reliable graph database optimized for storing and querying connected data. It's ideal when your query workloads require navigating connections and leveraging the strength, weight, or quality of the relationships between items. Combined with other AWS services, you can use Neptune as the database backend for applications and services whose data models and query patterns represent graph workloads, and as a datastore for graph-oriented BI and light analytics.

### Choosing a Data Technology For Your Workload

When choosing a database for your application you should ensure the operational, performance and data architecture characteristics of your candidate technologies are a good fit for your workload. Sometimes you will have to make tradeoffs between these characteristics. Many relational and non-relational technologies can be used to implemented connected data scenarios, but the balance of design and development effort involved, resulting performance, and ease with which you can evolve your solution will vary from technology to technology. 

You can use a relational database, such as one of the managed engines supported by the [Amazon Relational Database Service](https://aws.amazon.com/rds/) (Amazon RDS), to build a connected data application, using foreign keys and join tables to model connectedness, and join-based queries to navigate the graph structure at query time. However, the variations in structure that manifest themselves in many large graph datasets can present problems when designing and maintaining a relational schema. Complex traversal and path-based operations can result in large and difficult to understand SQL queries. Furthermore, the performance of join-intensive SQL queries can deteriorate as the dataset grows.

A non-relational document or key-value store, such as [Amazon DynamoDB](https://aws.amazon.com/dynamodb/), can similarly be used to model connected data. DynamoDB offers high-throughput, low-latency reads and writes at any scale. However, it is best suited to workloads in which items or collections of items are inserted or retrieved without reference to or joining with other items in the dataset. Applications that need to take advantage of the connections between items will have to implement joins in the application layer and issue multiple requests per query, making the application logic more complex, impacting performance, and undermining the isolation offered by a single query.

Neptune offers two different graph data models and query languages that simplify graph data modelling and query development, ACID transactions for creating and modifying connected structures, and a storage layer that automatically grows in line with your storage requirements, up to 64 TB. Complex graph queries are easier to express in Neptune than they are in SQL or in your own application logic, and will often perform better. RDS-based relational solutions, however, remain better suited to workloads that filter, count or perform simple joins between sets, while DynamoDB continues to excel at inserting and retrieving discrete items or collections of items with predictably low latencies at any scale.

## Data Architectures

### [Data Models and Query Languages](src/data-models-anmd-query-languages)


<table><tr><td><a href="https://github.com/aws-samples/aws-dbs-refarch-graph/tree/master/src/data-models-anmd-query-languages"><img src="https://raw.githubusercontent.com/aws-samples/aws-dbs-refarch-graph/master/src/data-models-anmd-query-languages/thumbnail.png"/></a></td><td>

Neptune supports two different graph data models: the property graph data model, and the Resource Description Framework. Each data model has its own query language for creating and querying graph data. For a property graph, you create and query data using Apache Tinkerpop Gremlin, an open source query language supported by several other graph databases. For an RDF graph you create and query data using SPARQL, a graph pattern matching language standardized by the W3C.

</td></tr></table>


## License Summary

The documentation is made available under the Creative Commons Attribution-ShareAlike 4.0 International License. See the LICENSE file.

The sample code within this documentation is made available under a modified MIT license. See the LICENSE-SAMPLECODE file.
