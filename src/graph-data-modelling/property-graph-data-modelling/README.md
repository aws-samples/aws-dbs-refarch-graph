# Property Graph Data Modelling

## An Application Graph Data Model

An application-specific property graph data model describes how your graph data is structured in ways that express your domain and make it easy and efficient to query for your most important use cases: 

  - What types of vertices do you have in your graph, as represented by vertex labels? 
  - What properties do you attach to each type of vertex? 
  - How are different vertices connected? 
  - What edge labels do you use to represent different types of edges? 
  - What properties do you attach to these edges? 

By answering these questions you describe an application property graph data model that is specialized for your specific application or set of uses cases.

In the relational world we'd express an application-specific relational model using schema and constraints. In the property graph world, however, there are very few commonly-adopted formal constructs for doing the same. Some graph databases advertise themselves as being schema-free, others allow for optional schema or constraints to be layered on top of the data, while a few require an upfront schema to be defined using a product-specific schema language.

>  Neptune is a schema-free graph database. No two vertices, even those with the same labels, need share the exact same set of properties. No two values of a particular property need use the same datatype. No two pairs of vertices need be connected in the exact same way. 
> The only constraints that Neptune asserts are:
>  - Every edge must have a start vertex and an end vertex. These can be the same vertex: that is, Neptune allows self edges.
>  - All vertex IDs must be unique, and all edge IDs must be unique. However, Neptune does allow a vertex and an edge to have the same ID.

You can use traditional data and application modelling techniques, including entity relationship diagrams (ERD) and the Unified Modelling Language (UML) to model your graph, but many graph application designs begin by illustrating a small, representative example of the graph, with specific vertices, labels, properties and edges showing how instances of things in the application domain are attributed and connected to one another. These _specifications by example_ can then be easily turned into representative datasets against which you can develop and test your queries. 

## Vertices

Use vertices to represent instances of a thing (an entity, concept, event, etc). You can think of a vertex as being roughly equivalent to a row in a relational table.

### Vertex IDs

Some graph databases automatically assign IDs to vertices when they are created, others allow you to supply your own. If the database allows it, consider supplying your own IDs when creating vertices. These could be a stable domain attribute that uniquely identifies an entity – an employee number, for example, or a product SKU – or an ID derived from an original source for the data, such as a primary key in a relational table.

> Neptune allows you to supply your own IDs when you create a vertex. If you don't supply an ID, Neptune will create a string-based UUID for you.

### Vertex labels

Use a vertex label to indicate the entity type or the role that the vertex plays in your dataset. _People, users, customers, products, jobs, policies_: in the singular, _person, user, customer, product, job_ and _policy_ – all good candidate vertex labels.

Try to limit ach vertex to having just one label. Entities can sometimes play multiple roles in your dataset: if that's the case, it's fine to attach multiple labels to a vertex. But avoid using labels as flags or enumerated tags that group entities of a particular type. Better to use a property to perform this partitioning. For example, if you wanted to version vertices in your graph, it would be best to do this by attaching a `version` property containing a numeric property value to each vertex, rather than labelling each vertex `v1`, `v2`, `v3`, etc.

### Vertex properties

Use vertex properties to represent the attributes of an entity: _first name, last name, invoice number, height, width, colour, ISBN, price_, etc. One of the modelling benefits of the property graph is that it allows you to 'chunk up' entity attributes into a discrete, easily understood record-like structure: that is, into a labelled vertex with multiple properties.

As well as using vertex properties to model entity attributes, you can also use them to store vertex metadata such as a version number, last updated timestamp, or access control list.

> Gremlin supports single, set and list cardinality for vertex properties. Neptune, however, supports only single and set cardinality, not list, with set cardinality the default. Set cardinality allows you to model multi-value vertex properties containing unique values: an `emailAddress` property, for example, could contain a set such as `[john.smith@example.com,j.smith@example.org,johnsmith@example.net]`.
> 
> If you need to model a list with Neptune – either to maintain list order or to store duplicate values – you have a couple of choices:
>  - If none of your queries need to filter the list's contents, you can store the list as a delimited string representation. To modify the contents of the list, you'll need to implement some logic in your application to retrieve the current representation of the list, parse it into a list type to which you can apply any necessary modifications, and then update the property with a string representation of the new list value.
>  - If you need to filter on the list's contents during a traversal, you'll have to pull the list values out as properties on separate vertices. You can connect these list value vertices either directly to the 'parent' vertex, or to a 'list' vertex that is attached to the parent. You can then use additional properties, either on the edges or on the value vertices themselves, to store metadata, such as item order. While this solution allows for filters or predicates to be applied to list values during a traversal, it introduces more complexity into both the data model and the queries that apply these filters. It may also increase both query latencies and storage costs (every value has the storage overhead of its being a vertex).