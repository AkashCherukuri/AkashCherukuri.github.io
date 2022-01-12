---
title: Relational Algebra
permalink: /notes/cs317/lec3
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

There are six basic operators:

1. Select
2. Project
3. Union
4. Set Difference
5. Cartesian Product
6.  



**Select Operation**
$$
\sigma_\rho (r) \qquad \rho\text{ - Selection Predicate}
$$
Only the rows which satisfy the selection predicate are present in the returned relation.



**Project Operation**
$$
\Pi_{A_1, \ldots, A_k}(r) \qquad A_i\text{ - Attribute}
$$
The attributes that are not listed are removed from the relation $r$.

These operations can be composed as shown in the below expression.
$$
\Pi_{name}(\sigma_{dept\_name = Physics}(instructor))
$$


**Cartesian Product**
$$
r_1 \times r_2
$$
Every row of $r_1$ is paired with every row of $r_2$. Cartesian product is usually used along with the select operation to compare rows between two different relations. This composition can be written in short as shown below:
$$
\sigma_\theta(r\times s) \equiv r \infty_\theta s
$$
Note that the predicate $\theta$ is over the union of the attributes of $r,s$.



**Union Operation**
$$
r\cup s
$$
The union operation is valid if:

1. $r,s$ have the same *arity* (same number of attributes)
2. The attribute domains must be comparable

Two relations with the above properties are said to be **compatible**.

{: .notice--info}

==doubtful==



**Set Intersection Operation**
$$
r\cap s
$$
==dammit man==



**Set Difference Operation**
$$
r - s
$$
==eugh==



**Assignment Operation**
$$
tmp \leftarrow r
$$
This operator acts similar to assignment in programming languages. This is used to break complex queries into smaller, more manageable queries. 



**Rename Operation**
$$
\rho_x(E)\qquad \rho_{x(A_1, \ldots A_n)}(E)
$$
This solves the issue of multiple attributes with the same name. That is, $r\times r$ would have every attribute repeated twice. The expression $E$ is renamed to $x$ in the first representation, and the attributes of the expression are renamed to $A_1, \ldots A_n$ in the second expression.



## Aggregate Functions

| Operation |     Function     |
| :-------: | :--------------: |
|    avg    |  Average value   |
|    min    |  Minimum value   |
|    max    |  Maximum value   |
|    sum    |  Sum of values   |
|   count   | Number of values |

$Y_{aggregate function} (r)$ returns a single value. For example, $Y_{avg(salary)}(student)$ returns the average salary of all students.

However, ${}_{dept\_name} Y_{avg(salary)}(student)$ groups the average salary of students in each department.

{: .notice--info}