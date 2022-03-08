*objective is to help satan out by sending Cantor to the depths of hell for practicing mathematics for some fucking reason????????*

*Seriously though, might wanna get this clarified by someone...*



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

- Input Tape: The “cells” in the tape are enumerated as $w_1,\ldots w_n$ from the left to right after which all cells are the blank character $B$. The set of tape alphabets is represented by $\tau$. Note that $Σ \sube τ - \{B\}$

- Control: A pointer which points to a cell of the tape. The control has states and transitions amongst these states tell the pointer to move to the left/right.

  $w_i/0,R$ transition on the state $q_j$ .... the pointer points to $w_i$ on the tape, replace $w_i$ with 0, and move 1 cell to the right.

For example, consider the language $L = \{ 0^n 1^n\vert n\geq0 \}$. The Turing machine for this language would be given by:

*draw and put*



More formally, a Turing machine would be given by the 7-tuple:
$$
M = (Q, Σ, \tau, δ, q₀,B, F)
$$


| Symbol   | Meaning                                                  |
| -------- | -------------------------------------------------------- |
| $Q$      | Set of states                                            |
| $\Sigma$ | Set of alphabet                                          |
| $\tau$   | Set of tape alphabet, $Σ\sub\tau$                        |
| $\delta$ | Transition function, $δ:Q\times\tau\to Q\timesτ×\{L,R\}$ |
| $q₀$     | Start state                                              |
| $B$      | Blank tape symbol                                        |
| $F$      | Final state                                              |

Similar to PDA, we have a notion of Instantaneous Descriptions (IDs), where the symbol $\vdash$ refers to a single move of the M. The turing machine $M$ is said to accept the word $w_{inp}$ iff $(q₀,w_{inp})\vdash^* (qₖ,x)$ where the machine **halts** and $qₖ$ is a **final state**.



#### Variations of the Turing Machine

Note that all these variations have the same expressive power. The first three variations are called “Syntactic Sugar” because they don’t add ant computational capability.

- 2-way infinite tape
- Multiple tape heads
- non-deterministic Turing Machine
- Output tape (write only) immutable *the kentucky loving fuck???*



> ### HW
>
> 1Q. Write the TM for the language $L = \{ aⁿbⁿcⁿ\vert n\geq 1 \}$
>
> 

> ### HW
>
> 2Q. $L = \{ ww\vert w\in(a+b)^*, \vert w\vert\geq1 \}$
>
> 
