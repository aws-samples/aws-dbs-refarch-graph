__Graph Database__ workloads are operational and business intelligence database workloads that store and query highly connected data. 

Key characteristics of a graph database workload include:

  * Data volumes are expected to comprise many millions or billions of items and relationships.
  * Data can change frequently, with additions and changes to items and connections made available to clients less than a second after having been made durable.
  * Queries begin by finding one or more starting points in the graph, and then explore the neighbouring portions of the graph in order to discover connected items or compute results as they traverse the paths that connect items, with subsecond response times.
  * Items may exhibit variable schema, insofar as two items of the same type may not necessarily share the exact same set of attributes.
  * Items may be connected to one another in many different ways, with no two pairs of items necessarily connected in the exact same way.

Data workloads in which data items are implicitly or explicity connected to one another can be implemented using a wide range of relational and non-relational technologies, but in situations where the data is not only highly connected but also the queries addressed to the data exploit this connected structure, there are many design, development and performance benefits to using a graph database optimized for graph workloads.

[Amazon Neptune](https://aws.amazon.com/neptune/) is a fast and reliable graph database optimized for storing and querying connected data. It's ideal when your query workloads require navigating connections and leveraging the strength, weight, or quality of the relationships between items. Combined with other AWS services, you can use Neptune as the database backend for applications and services whose data models and query patterns represent graph workloads, and as a datastore for graph-oriented BI and light analytics.



## License Summary

The documentation is made available under the Creative Commons Attribution-ShareAlike 4.0 International License. See the LICENSE file.

The sample code within this documentation is made available under a modified MIT license. See the LICENSE-SAMPLECODE file.
