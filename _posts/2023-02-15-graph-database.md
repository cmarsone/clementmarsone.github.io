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

### Neo4J basics

*Data model*: labeled, directed graphs

*Data manipulation language* (CRUD): Cypher, used to describe data
and patterns to be matched

*Relationship* descriptions in Cypher: -- (undirected) vs. --> or <-- (directed)

*Patterns* combine node and relationship descriptors

### Graph stores: summary

• Graph databases repeatedly "attempted" but not fully
"solved" yet

• Very convenient data model, natural representation

• Typically no strict schema

• No standard query language

• Semantic graphs are a particular case (RDF and SPARQL are
standards)

• Most powerful tools around: distributed graph stores (Pregel,
Spark GraphX)

– Extra dimension: graph partitioning
– Less effort on query language; in progress


























