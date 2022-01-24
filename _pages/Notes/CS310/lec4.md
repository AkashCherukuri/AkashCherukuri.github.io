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

A set of languages is called as a Language Class, and Language classes have two kinds of properties, **closure** and **decision**. We will be focusing on decision properties for now.

**Decision Property** for a class takes the formal description of a language to see if a property holds. (Formal description - using DFA)

**Closure Properties** are used to prove if a language is regular or not. For example, $L_1=\{0^n1^n\}$ is not a regular language. However, proving $L_2=\{\text{equal number of 0's and 1's}\}$  to not be regular is tougher. Closure can be used as follows, if $L_2$ was regular, then RHS should be regular as well (contradiction!)
$$
L_2 \cap L(0^*1^*)= L_1
$$
==**Pumping Lemma** is used to show that $a^nb^n$ cannot be expressed by a DFA.==



*Membership problem* is checking if a word $w\in L$. The problem is said to be **decidable** iff the algorithm used for solving it has the following two properties:

1. **Soundness**: The algorithm is correct
2. **Terminate**: The algorithm terminates in finite time

A list of problems that we will be dealing with in this course are given in the table below. The methods to solve the problems have been discussed further below the table.

| Problem       | Question                                                     |
| ------------- | ------------------------------------------------------------ |
| Emptiness     | $L=\phi$ ?                                                   |
| Infiniteness  | Is $L$ infinite?                                             |
| Containment   | Given $L,M$ is $L \subseteq M?$                              |
| Minimality    | Can a DFA with smaller states accept the same language? (use distinguishable states) |
| Membership    | Is $w\in L$?                                                 |
| Equivalence   | Are $L_1$ and $L_2$ equivalent?                              |
| Impossibility | Show $L$ cannot be accepted by any DFA (Pumping Lemma)       |

&nbsp;

## Infiniteness Property

If the DFA has $n$ states, and the language contains any string of length $n$ or more, then the language is infinite. Otherwise, the language is surely finite. (Proof using the pigeon-hole principle)

### Pumping Lemma

For every regular language $L$ there exists an integer $n$ such that every string $w$ in $L$ of length greater than $n$, we can write $w = xyz$ such that

1. $\vert xy \vert < n$
2. $\vert y \vert>0$
3. $\forall i\geq0, xy^iz\in L$

This is closely related to the infiniteness algorithm we stated earlier. $y$ is the pert of the DFA which has a loop, and can thus be infinitely “pumped” to keep generating new strings.

We can now prove that $\{0^k1^k\}$ is not a regular language. Assume it was, and let the integer be $n$. Consider the word $0^n1^n$ written as $xyz$. Because $\vert xy \vert<n$, $y$ is made up fully of $0's$. Therefore, $xy^iz$ does not belong in $L$ as the number of $1's$ and $0's$ is not equal.

 &nbsp;

## Equivalence Algorithm

Given two DFA’s, take the cross-product between them. $(q,r)$ is a final state of this DFA iff **exactly one** of the two is a final state in its original DFA. That is, this new DFA accepts $L_1\oplus L_2$. If they were equivalent, then this new DFA would not accept any states. 

**Containment Algorithm** is exactly the same, except that we search for words accepted by $L$ and not by $M$.

&nbsp;

## Minimality Algorithm

Create a table containing pairs of all states in the DFA. Two states are said to be **distinguishable** if there exists a string which takes exactly one of the two to a final state. We can use induction using this property.

1. Mark all pairs where exactly one is the final state (basis)
2. Mark all pairs where a letter takes exactly one of the two to a previously marked state
3. Remove states unreachable from the start state

It can be proven using induction/contraction that the DFA obtained using this method is **THE** minimal DFA.



&nbsp;

# Closure Properties of Regular Languages

*have to write notes*