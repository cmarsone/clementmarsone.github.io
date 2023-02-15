---
layout: post
title: Graph stores
---

### Motivations

• Graphs correspond to a natural organization of knowledge
• They generalize relations, trees (documents), key-value pairs ...
• They do not simplify query evaluation and may make it more complex

### Graph database models
• Graph $= V$ (nodes) and $E$ (edges, subset $\subseteq V \times V$)
• Directed vs. undirected edges
• Nodes:
– Unlabeled
– With a single label (in some cases called type)
– With a set of attribute-value pairs
– With complex internal structure (persistent objects)
• Graphs may have semantics (Resource Description Framework Schema)

### Object-oriented databases

• *Idea*: capitalize on the flexibility of OO programming languages to handle databases of persistent objects
• Object Database Management Group (ODMG): consortium
of OODB vendors which produced a standard

1. Object Model: classes, attributes, methods...
2. Object Definition Language (ODL): persistency roots (persistent collections)
3. Object Query Language (OQL): navigation from one object to its attribute, method invocation, structured query language
4. C++ and Java Bindings
5. Mostly relational

