---
title: Non Deterministic Automata
permalink: /notes/cs310/lec4
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


Non determinism is of two types:

1. **Don't Care**: The choice offered doesn't matter eg: simplifying the LHS or RHS of an equation first
2. **Don't Know**: We need to guess the right choices

NDA's are of the second type. The transition function $\delta$ is redefined to a transition *relation* which outputs a set containing all possible next states. 

NDA is said to accept a word if **any one** of the possible end states is a final state.
{: .notice--info}



### Epsilon Transitions

NFA's also allow $\epsilon$-transitions between states. 

H1) Draw the NFA for $L=  \{ abc \} \cup \{\text{all strings not ending in }cc\}$ where $\Sigma=\{a,b,c\}$

It seems that NFAs have more expressive power than DFAs, as expressing languages in NFA seems simpler and easier. But is this actually the case?

**NO.**

NFA (with/without $\epsilon$ transitions) has the same expressive power as DFA. They are both equivalent.
{: .notice--warning}

&nbsp;



## Decision Properties of Regular languages

There are two kinds of properties, closure and decision. We will be focusing on decision properties for now.

*Membership problem* is checking if a word $w\in L$. The problem is said to be **decidable** iff the algorithm used for solving it has the following two properties:

1. **Soundness**: The algorithm is correct
2. **Terminate**: The algorithm terminates in finite time

A list of problems that we will be dealing with in this course are:

| Problem       | Question                                                     |
| ------------- | ------------------------------------------------------------ |
| Emptiness     | $L=\phi$ ?                                                   |
| Finiteness    | Is $L$ finite?                                               |
| Minimality    | Can a DFA with smaller states accept the same language? (use distinguishable states) |
| Membership    | Is $w\in L$?                                                 |
| Equivalence   | Are $L_1$ and $L_2$ equivalent?                              |
| Impossibility | Show $L$ cannot be accepted by any DFA (Pumping Lemma)       |

**Pumping Lemma** is used to show that $a^nb^n$ cannot be expressed by a DFA.