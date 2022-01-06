---
title: Regular Expressions
permalink: /notes/cs310/lec2
classes: wide
author_profile: false
#sidebar:
#    nav: "notes_cs310"
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

We try to express a language using a base case, and an inductive case. There are four kinds of inductive rules:

| $E_1 + E_2$ | Union          | $L(E_1+E_2) = \{E_1, E_2\}$                    |
| ----------- | -------------- | ---------------------------------------------- |
| $E_1 E_2$   | Concatenation  | $L(E_1E_2) = \{E_1E_2\}$                       |
| $E_1^*$     | Repetition (?) | $L(E_1^*) = \{\epsilon, E_1, E_1E_1, \ldots\}$ |

Note that Finite State Automata and Regular Expressions are equivalent to each other, as discussed in the previous lecture.

Note that $(ab+ba)^* = \{ \epsilon, ab, ba, abba, baab, \ldots\}$



HW1.

**Language using a,b as alphabets; accepts all words with even number of a's**

The FSA for this language is easy enough. The regular expression equivalent would be given by:
$$
L = (b^*ab^*ab^*)^*
$$


HW2.

**Same alphabets as before; but even number of a's AND odd number of b's**

https://www.geeksforgeeks.org/generating-regular-expression-from-finite-automata/



# Push Down Automata

We want the FSM to have access to another data structure for more expressive power (a stack). The bottom of the stack is denoted by $Z_o$ with the **stack symbols** being pushed on top of it. Do note that the input signals need not be the same as the stack symbols.

This lets the PDA to:

1. Move to a new state
2. Pop/Push from a stack

The transitions are labeled as $(a,X\vertaX)$. Meaning that the transition corresponds to alphabet $a$ and we are pushing it onto the stack. Similarly $(b,aX\vertX)$ meaning $a$ is popped from the stack. 

==A word is accepted on an EMPTY STACK; rejected when no transition or stack not empty==

HW3.
$$
L = \{ \text{Number of a's < 2}\times\text{number of b's} \}
$$
Write the above language using **CFG**.



doubt1 - $a\vertWa$ meaning?

doubt2 - How is an empty string rejected?



### Non-Determinism

Consider a language on $a,b$ which contains all palindromes. For example, $abbbba$ is a word in the language. This can be represented by a **Non-Deterministic** Automata, where we need to *guess* where we stop pushing and start popping.