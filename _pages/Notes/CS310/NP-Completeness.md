# Decision Problems

The class of problems with yes/no answers are called as decision problems. For example, given two TM $M_1$ and $M_2$; “Are the languages accepted by the two Turing Machines identical?” 

Complexity classes are defined to compare the difficulty and the nature of such problems.

## Complexity Classes : P

The class of decision problems that can be solved in **polynomial time** by a deterministic Turing machine. That is, the number of steps taken by the TM to halt should be polynomial in the size of input.

## Complexity Classes : NP

The class of decision problems that can be solved in polynomial time by a **non deterministic** Turing machine. Non Deterministic TM are the “don’t know” kind, wherein all possible combinations have to be checked and the TM accepts if anyone combination accepts.

If we can “guess” and “verify” in polynomial time, then the complexity of the problem is NP. (Guessing need not be polynomial, but the verification must take polynomial time by a deterministic algorithm/TM)

### NP-HARD

A problem is in NP-Hard when, if the problem is in P then P=NP but the problem itself doesn’t belong to NP. Example would be the tautology problem.

## Complexity Classes: NP Complete

A problem such that if it is in **P**, then every problem in NP would also be in P. That is, $M$ is NP there should be a polytime algorithm from every problem in NP to $M$.

### Reductions

Given two problems $L_1$ and $L_2$ we say that $L_1\leq_pL_2$ if $L_1$ can be reduced to $L_2$ in polynomial time. “$L_2$ as at least as complex as $L_1$”.

> If the optimization versions of NP-Complete problems can be solved in polytime, then P=NP. (Meaning that even the optimization versions are not solvable in polytime)

## SAT Problem

This is an NP-Complete problem. Given a boolean expression in CNF, we would like to know if there exists an assignment of truth values such that the expression is satisfied. It is clear that SAT belongs in NP, we can simply “guess” the values and solve the equation in polynomial time.

==SAT is NP-Complete! - Cook’s Theorem== (Reduce to 3SAT in polynomial time and build a TM on that..., also note that 2SAT is in P!)

## Node Cover Problem

The node cover problem is reducible to the 3SAT problem, which we know to be NP-Complete. Therefore, the node cover problem is NP-Complete as well!

## Knapsack Problem

==Converting from 3SAT to Knapsack uses some high level shit, base32 numbers???==



