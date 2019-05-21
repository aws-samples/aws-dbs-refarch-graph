# Property Graph Data Modelling

## An Application Graph Data Model

An application-specific property graph data model describes how your graph data is structured to express your domain and make it easy and efficient to query for your most important use cases: 

  - What types of vertices do you have in your graph, as represented by vertex labels? 
  - What properties do you attach to each type of vertex? 
  - How are different vertices connected? 
  - What edge labels do you use to represent different types of edges? 
  - What properties do you attach to these edges? 

By answering these questions you describe an application property graph data model that is specialized for your specific application or set of uses cases.

In the relational world we'd express an application-specific relational model using schema and constraints. In the property graph world, however, there are very few commonly-adopted formal constructs for doing the same, and an overall lack of tooling. 

> Some graph databases advertise themselves as being schema-free, others allow for optional schema or constraints to be layered on top of the data, while a few require an upfront schema to be defined using a product-specific schema language. Neptune is a schema-free graph database. No two vertices, even those with the same labels, need share the exact same set of properties. No two values of a particular property need use the same datatype. No two pairs of vertices need be connected in the exact same way. 
> The only constraints that Neptune asserts are:
>  - Every edge must have a start vertex and an end vertex. These can be the same vertex: that is, Neptune allows self edges.
>  - All vertex IDs must be unique, and all edge IDs must be unique. However, Neptune does allow a vertex and an edge to have the same ID.