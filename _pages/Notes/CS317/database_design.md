# Database Design using E-R Model

In designing a database schema, we must ensure to avoid two main problems:

- Redundancy - causes inefficient use of storage, and inconsistency of all data is not updated
- Incompleteness - inability of the schema unable to represent certain aspects of the data

We will be looking at the **Entity Relationship model** in this chapter. An *entity* is an object that is distinguishable from each other, and a *relationship* shows the connection between different entities.

*Entity Set* $E$ contains all entities with a common attribute. A subset of the attributes form a **primary key of that entity set** to be able to uniquely distinguish entities in the set.

*Relationship Set* is a mathematical relation among $n\geq 2$ entities, each taken from entity sets. $(e_1, \ldots, e_n)$ is a relationship in the below formulation. They are represented using Diamonds in schema diagrams. **Note that relationship sets may have attributes specifically designed for them**. That is, we may want to keep track of when a student met their advisor for an “advisor” relationship.
$$
\{ (e_1, \cdots, e_n) \vert e_1\in E_1, \ldots, e_n\in E_n\}
$$
The occurrence of an entity set plays a role in the relationship. This is denoted by labeling the line connecting the set and the relationship set. The number of entity sets involved denotes the degree of the relationship set. (not the attributes!) Relationships with degree > 2 is very rare, however.

**Composite Attributes** allow us to divide them into subparts. They are represented by indenting the underlying attributes.

**Mapping Cardinalities** refers to denoting the entities which can be related to each other. They are denoted by using either an arrow(one) or a line(many).

