*objective is to help satan out by sending Cantor to the depths of hell for practicing mathematics for some fucking reason????????*



**Kolmogrov Complexity** - The number of lines that are required to “prove”/code up a program to solve/prove the problem/statement



Enumerable languages are either finite and infinite. Finite languages can be represented by regular languages, but some part of infinite languages can be represented by CFGs.



*Recursively Enumerable* - a language that is accepted by a Turing machine that halts after a finite (?) number of steps and either accepts the word or rejects it.



&nbsp;



# Turing Machines

Turing machines aim to recognize any Recursively enumerable language. 

> **Church Turing Thesis**
>
> Turing machines and recursive function theory can represent any *effectively computable language*. (“Thesis” and not a theorem because “effectively” is loosely defined)

==Not all languages are enumerable, even if $\Sigma$ is finite==



**Decidability** - Given $G$, is $L(G)$ empty (yes). “Is the complement of $L$, called $L^C$ empty?” (This is undecidable)

> **Halting Theorem**
>
> Given by Godel, if an algorithm can tell if **any** program terminates, then we have solved the halting problem.
>
> *some example?*



Turing Machines consist of:

- Input Tape: The “cells” in the tape are enumerated as $w_1,\ldots w_n$ from the left to right after which all cells are the blank character $B$. Tape alphabets are represented by $\Tau$

- Control: A pointer which points to a cell of the tape. The control has states and transitions amongst these states tell the pointer to move to the left/right.

  $w_i/0,R$ transition on the state $q_j$ .... the pointer points to $w_i$ on the tape, replace $w_i$ with 0, and move 1 cell to the right.

​	
