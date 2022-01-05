---
title: Relational Models
permalink: /notes/cs317/lec2
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

*Domain* - The set of allowed values for each attribute

Usually, attribute values are required to be **atomic** (indivisible). A special value **null** is part of every domain.

Example: parts of roll numbers in IITB can be used to interpret the branch of that particular student, meaning it isn't atomic (and is bad practice)

Is `null < 5` True or False?
{: .notice--warning}

*missed*

**Database Schema** - logical structure of database; `intructor(ID, name, dept_name, salary)`

**Database Instance** - snapshot of data in database at a given instant

&nbsp;

### Keys

Let $R$ be the set of all attributes in a database. Let $K$ be a subset of $R$.

K is a **Superkey** of R if values of K are sufficient to identify a unique tuple of each possible relation $r(R)$.

A minimal superkey is called a **Candidate key**. One of the candidate keys is chosen to be the **Primary Key**.

**Foreign Key Constraint** is an integrity constraint which enforces that value in one relation in another. This avoids errors caused by improper data entry.

Example: `dept_name` in the `instructor` table can be linked to the `dept_name` in the `department` table. Here, `instructor` is called the **Referencing Relation** and `department` is the **Refrenced Relation**.

Referenced Relation should be a primary key?
{: .notice--info}

