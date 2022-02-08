# Context Free Grammars

This is a methodology for representing languages. It is more powerful than DFAs and RE, but is still not enough to define all the possible languages. The basic idea is to use “variables” as stand-ins for sets of strings.

Formally, the terms described below define a CFG.

- **Terminals** - The symbols of the alphabet
- **Variables / Non terminals** - A finite set of other symbols
- **Start Symbol** - The variable whose language is being defined
- **Production** - A rule of the form “$\text{variable} \rightarrow \text{variables} ∪ \text{terminals}$“

“Productions of A” refers to the set of all strings that are *derivable* from $A$ using the rules defined by the CFG. A string $\gamma$ is said to be derived from $\alpha$ iff the application of a rule results in $\gamma$. This is represented as $\alpha\implies\gamma$.

Derivation using 0 or more steps is represented by $\overset{*}{\implies}$.

Any string derived from the start string is called as a **Sentential Form**. It essentially is a string “on its way” to becoming part of the language.

A language defined by a CFG is called as a Context Free Language. {: .notice--info}



### BNF Notation (Backus-Naur-Form)

This is a method of representing the rules of CFG in a programming way.

| CFG Part                          | BNF Representation                           | Example                                  |
| --------------------------------- | -------------------------------------------- | ---------------------------------------- |
| Variable                          | \<word\>                                     | \<statement\>                            |
| Terminals                         | multicharacter strings in bold or underlined | while, **while**, <u>while</u>           |
| $\rightarrow$ in rule definitions | $::=$                                        | \<state\> ::= a                          |
| “or” in rule definitions          | $\vert$                                      | \<state\> ::= a$\vert$b                  |
| (not) Kleene Closure ($a^+$)      | “...”                                        | \<state\> ::= \<\state>...               |
| Optional Elements                 | [...]                                        | \<state\> ::= \<statea\> [or \<stateb\>] |
| Grouping $(ab)^*$                 | {...}                                        | \<state\> :== {\<statea\>\<stateb\>}..   |



### Leftmost and Rightmost derivations

A problem with CFGs is that every word may have more than one derivations possible. This makes verification and confirmation difficult. A derivation is said to be “Leftmost” when only the leftmost non-terminal is operated on in every step of the derivation. The same definition works for rightmost derivations as well.



&nbsp;



# Parse Trees

Trees whose nodes are labeled by the symbols of a particular CFG. The leaves are labeled by terminals or $\epsilon$, Interior nodes by variables and the root by the start symbol.

The **yield** of a parse tree is given by concatenating the leaves in a left-to-right order. (The order of preorder traversal)

![image-20220204160748905](../../../assets/images/typora/image-20220204160748905.png)



> For every parse tree, there is a unique leftmost derivation. Conversely, for every leftmost derivation, there is a unique parse tree with the same yield.

The forward part can be proven using strong induction on the height of parse tree, and the backwards part can be proven using strong induction on the length of the derivation. Also, it can be seen from the proof that obtaining a parse tree doesn’t depend on the derivation being “leftmost”.

> For any derivation, there exists a unique parse tree with the similar yield.



### Ambiguous Grammar and LL(1) Grammar

Leftmost and Rightmost derivations had been introduced to alleviate confusions caused by multiple derivations. However, it is not guaranteed that a unique leftmost (or rightmost) derivation exists for a given string.

For example, consider grammar with the following rule. Two parse trees exist for the string “()()()” 


$$
S\rightarrow SS\vert (S)\vert ()
$$
 ![image-20220204162158963](../../../assets/images/typora/image-20220204162158963.png)



From the theorems discussed earlier, it can be concluded that two leftmost and rightmost derivations would exist for this grammar. This is thus called **Ambiguous Grammar**.



Note that ambiguity is a property of the grammar, and not the language itself. That is, we can write equivalent unambiguous grammar for the above example.


$$
\begin{align*}
B \rightarrow &(RB\vert\epsilon \\
R \rightarrow &)\vert (RR
\end{align*}
$$
Grammar such as the above example, where we can figure out the production to use in a leftmost derivation by looking at the string left-to-right and looking at the next one symbol is called $LL(1)$ grammar. **L**eftmost derivation, **L**eft-to-right scan, **1** symbol of lookahead.

$LL(1)$ grammars are never ambiguous. {: .notice--info}

Note that some languages are **inherently ambiguous**, meaning that there does not exist an unambiguous grammar that accepts the CFL’s language. For example, $\{0^i1^j2^k\vert i=j\text{ or }j=k\}$ is inherently ambiguous. This can be understood intuitively by looking at $0^n1^n2^n$, which could have been obtained from either the first check or the second check.



&nbsp;



## Eliminating Useless Symbols

Useless symbols are of two kinds:

1. Symbols which do not derive a terminal string
2. Symbols which are not reachable from the start

We shall look at methods for elimination of such symbols.




### Eliminating Symbols which do not derive a terminal string

Consider the following set of rules:


$$
\begin{align*}
S&\rightarrow AB \\
A&\rightarrow aA\vert a\\
B&\rightarrow AB
\end{align*}
$$


It can be said that $S$ derives nothing and the language is empty. The algorithm for deducing this is quite simple and is based on induction.

#### Algorithm

**Basis** - If there is a production $A\rightarrow w$ where $w$ is composed of terminals, then $A$ derives a terminal string

**Induction** - If $A\rightarrow \alpha$ and $\alpha$ consists only of terminals and variables known to derive terminals, then $A$ derives a terminal string.

For a given set of rules, we perform the above induction and mark all the variables which generate a terminal string. We can then remove all the rules which involve a variable which include a variable which has not been marked.

![image-20220204164928701](../../../assets/images/typora/image-20220204164928701.png)



### Eliminating Unreachable Symbols

The symbols which are unreachable from the starting symbol are said to be *unreachable*. We can remove all rules which involve such strings as they are not relevant. 



### Epsilon Productions

A production of the form $A\rightarrow \epsilon$ is said to be an $\epsilon$-production.

> If L is a CFL, then $L-\{\epsilon\}$ has a CFG with no $\epsilon$-productions.

To eliminate these productions, we first discover **nullable variables**. (variables where $A\overset{*}{\implies}\epsilon$)  If there is a production $A\rightarrow \alpha$ with **all** symbols of $\alpha$ being nullable, then $A$ is nullable itself.

*the algorithm is quite muddy*



### Unit Productions

