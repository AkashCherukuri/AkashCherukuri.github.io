*objective is to help satan out by sending Cantor to the depths of hell for practicing mathematics for some fucking reason????????*

*Seriously though, might wanna get this clarified by someone...*

**Kolmogrov Complexity** - The number of lines that are required to “prove”/code up a program to solve/prove the problem/statement

# Turing Machines

The class of languages that can be recognized by Turing machines are called Recursively Enumerable Languages.

> **Church Turing Thesis**
>
> Turing machines and recursive function theory can represent any *effectively computable language*. (“Thesis” and not a theorem because “effectively” is loosely defined)

Not all languages are enumerable, even if $\Sigma$ is finite. This can be easily proven using diagonalization.



A class of languages is said to be decidable if given a word $w$, an algorithm exists to check if $w\in L$ for any $L$ that belongs to that language class. Recursively Enumerable Languages are decidable, but $L^C$ are **NOT** !

> **Halting Theorem**
>
> Given by Godel, if an algorithm can tell if **any** program terminates, then we have solved the halting problem.
>



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



### Instantaneous Descriptions (ID)

Similar to PDA, we have a notion of Instantaneous Descriptions (IDs), where the symbol $\vdash$ refers to a single move of the M. IDs are of the form $(\alpha q\beta)$, where $q$ refers to the current state of $M$ and the tape head points to the first character of $\beta$. For example, Consider the tape to be $\ldots BB00100BB\ldots$ with the head at $1$ and the state being $q$. The ID would be given by $(00q100)$.



#### Variations of the Turing Machine

Note that all these variations have the same expressive power. The first three variations are called “Syntactic Sugar” because they don’t add ant computational capability.

- 2-way infinite tape
- Multiple tape heads
- non-deterministic Turing Machine

Also note that the halting and accepting variants of Turing Machines are equivalent. Moreover, all these Turing machines are equivalent to $(Q,\Sigma=\{0,1\}, \Gamma = \{0,1,B\}, \delta, q, B, F = \{q_f\})$ which has a single final state.

The above machine can be **“encoded”** using only a string of 0s and 1s. Let the automaton move from $x_i$ to $x_j$, with the tape’s transition being $x_k\vert x_l,D_m$. 
$$
111 \ldots 11 0^i10^j10^k10^l10^m11\ldots111
$$
==Now that we have a binary encoding, we can clearly see that **Turing machines can be enumerated**.==

## Definitions

| Name                        | Definition                                             |
| --------------------------- | ------------------------------------------------------ |
| L is Recursively Enumerable | A recognizer TM exists that accepts L                  |
| L is Recursive              | A recognizer TM that accepts L must halt on all inputs |

==Note that RE languages are not closed under Complementation and Difference, but **recursive languages are**!==

Define $L_d$ to be the diagonal formed by all words and all Turing Machines. Define $L_u$ as follows:
$$
L_u = \{ \text{Enc}(M)\vert\vert \text{Enc}(w) : M\text{ is a TM which accepts }w \}
$$
$L_d$ is not recursively enumerable, whereas $L_u$ is Recursively Enumerable but it isn’t Recursive in nature. This can be proven using **Reduction**.

We can use diagonalization to give an example of a language that is not Recursive Enumerable in nature $(L_d)$. Moreover, the language of binary encoded tuples $<M,w>$ can be used to give  language that is Recursive Enumerable, but not recursive. The language is:
$$
L_u = \{ <M,w>\vert \text{ Turing Machine }M\text{ accepts the word }w \}
$$
The TM for $L_u$ would contain 3 Tapes; 

1. Holding the input $<M,w>$
2. Holding $M$‘s tape
3. Holding $M$‘s state

The following steps would be performed by the UTM:

1. Check that the encoding for $M$ is valid for a turing machine, reject and halt if not valid
2. Examine $M$ and figure out how many blocks are needed to represent all alphabets used by $M$
3. Initialize Tape2 to contain $w$ as the input for $M$
4. Simulate $M$ by using Tape1 and Tape3, and writing onto Tape2

This is obviously not recursive as $M$ is not guaranteed to halt.

&nbsp;

# Language Properties

A set of languages would be a **property** of languages. This can be represented as a TM problem: Given a property $P$ we would like the set of all Turing Machines $L_p$ such that every $L(M), M\in L_p$ has the property $P$.

> **Rice’s Theorem**
>
> $L_p$ is undecidable for every property other than the trivial *always-false*(empty set) and *always-true* (all languages accepted).

We shall use Reduction to prove this theorem.

## Reduction

A **reduction** from $L$ to $L'$ is given by a TM that always halts (algorithm) which takes $w$ and outputs $x$ such that $w\in L \iff x\in L'$.

Therefore, if we reduce $L$ to $L’$ and we know that $L'$ is decidable, it follows that $L$ is decidable as well. Conversely, if $L$ is not decidable then $L’$ would not be decidable as well.

### Proof of Rice’s Theorem

...didn’t understand that well...



### Post-Correspondence Problem

This is a general problem that $L_u$ can be reduced to, and is usually used to show undecidability of other problems.

Given two sets $W = \{ w_1, w_2\ldots w_k \}$ and $X = \{ x_1, x_2\ldots x_k \}$; the solution set is defined as the sequence $(i_1, \ldots, i_l)$ where $w_{i_1}\vert\vert w_{i_2}\ldots\vert\vert w_{i_l} = x_{i_1}\vert\vert x_{i_2}\ldots\vert\vert x_{i_l}$. This problem is Recursively Enumerable, but is not recursive in nature. (undecidable!)

This problem can be used to prove that the **Ambiguity Problem** is undecidable. The following grammar is ambiguous IFF PCP has a solution set. 
$$
\begin{align*}
	S&\to S_1\vert S_2\\
	S_1&\to w_iS_1a_i\vert w_ia_i \\
	S_2&\to x_iS_2a_i\vert x_ia_i \\
\end{align*}
$$
Similarly, ==CFL Equivalence, and Regularity of a CFL== are also undecidable.

