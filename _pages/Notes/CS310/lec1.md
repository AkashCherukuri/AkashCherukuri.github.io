---
title: Chomsky Hierarchy
permalink: /notes/cs310/lec1
classes: wide
author_profile: false
# sidebar:
#     nav: "notes_cs310"
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

The languages in increasing order of generality are:

1. Regular Languages - Finite State Automata
2. Context Free Grammar - Push Down Automata
3. Unrestricted Grammar - Turing Machine

&nbsp;

### Finite State Automaton Problems

Q1. Is a bitstring's decimal representation divisible by 7?

A. Make an FSM tracking the remainder, start at 0. 


HW1. What if the bitstring is fed in reverse?

HW2. Instead of a base2 input, what is the FSA if the input is decimal (base10)?


### Context Free Grammar

FSA cannot be drawn for CFG. Example: $a^nb^n$ cannot be obtained using a finite state automaton. 

It can be written in grammar notation however, as follows:

$$\begin{align}
  S &\rightarrow \epsilon \\
  S &\rightarrow aSb \\
\end{align}$$

Another example of a language which cannot be represented by FSA is the "matching parentheses" problem. Both these can be represented using a PDA/grammar notation.

We would like un-ambiguous grammar, meaning that no two rules are the "same". The following grammar is not ambiguous, the proof will be discussed later.

$$\begin{align}
  S &\rightarrow \epsilon \\
  S &\rightarrow (S) \\
  S &\rightarrow SS \\
\end{align}$$

<!-- 
Similarly, the grammar for a language where the words have equal number of a's and b's is:

$$\begin{align}
  S &\rightarrow \epsilon \\
  S &\rightarrow aSb \\
  S &\rightarrow bSa \\
  S &\rightarrow SS \\
\end{align}$$
 -->

The grammar in CFG has 4 components:

$$ G = (V, \Sigma, R, S) $$

V - Non-terminal variables (S in previous case)
$\Sigma$ - alphabet
R - Rules ($S \rightarrow SS$)
S - Start symbol *what dis*


### Unrestricted Grammar

CFG Grammar's restrictions on R can be lifted to obtain unrestricted grammar.

$$ UG = (V, \Sigma, P, S) $$

P - The rules are of form $\alpha \rightarrow \beta$ where $\alpha\beta\in (V \cup \Sigma)^\*$

Turing Machine and Unrestricted Grammar are equivalent. They can compute **any** mathematical function.
{: .notice--info}


HW3. $L = \{ a^{n^2} \vert n\geq 0 \}$