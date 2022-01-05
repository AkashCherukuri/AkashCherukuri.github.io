---
title: The basics
permalink: /notes/cs317/lec1
classes: wide
author_profile: false
# sidebar:
#     nav: "notes_cs337"
---
<script type="text/javascript" src="https://code.jquery.com/jquery-1.7.1.min.js"></script>

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML" async></script>


<!-- Notes Begin from here -->

Databases are ever-present in our lives. Old database systems had problems with:

- data redundancy and inconsistency
- difficulty in accessing data
- data isolation
- integrity problems, assigning "rules" to variables
- crashes in between causing partial updates
- concurrent access by multiple users needs to be addressed. Embedded databases (SQLITE) do not have concurrency issues as they are always accessed by a single user (music app storing playlist locally)
- security problems

<!-- SQL was never designed to be scalable or to allow parallel access to databases. However, the  -->

&nbsp;

## Data Models 

*the fuck is a relational model*

*Yeah I have no idea what he said here*

## Relational Model

All the data is stored in tables. Relational models essentially are tables with rows (tuples) and columns (attributes).

**Logical Schema** is the overall logical structure of the table.

**Physical Schema** is the overall physical structure of the table. That is, the data structures used to store the table itself. 

Declarative Languages hide the physical schema and only show the logical schema to the programmer. *doubtful*

**Physical Data Independence**: the physical schema can be modified without changing the logical schema of the table.

&nbsp;

### Data Definition Language (DDL)

`numeric(8,2)` means 6 digits before decimal point, 2 after

### Data Manipulation Language (DML, Query Language)

Language used for accessing and updating the data organized by the data model.

*incomplete*

SQL is non-procedural and not turing complete. This simplicity lets the compiler to compile the program efficiently. It is embedded in APIs to perform other complex queries.

&nbsp;

### Database Design

Logical Design is created once, and needs to be carefully thought out. Physical design is flexible, as indexes and the such can be added on the fly. Improper design causes poor data storage and inefficient querying.

### missed something

### Storage Manager

*ughhh*



