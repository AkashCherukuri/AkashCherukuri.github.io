---
title: Syntax Analysis
permalink: /notes/cs302/synt
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

Syntax analysis aims to discover the larger structures in a program. The tokens identified through scanning are analyzed to infer the relationships between them. These relationships are represented in the form of a **Parse Tree of (concrete) Syntax Tree**. An Abstract Syntax Tree is derived from this parse tree by the IR.

![image-20220202112805316](../../../assets/images/typora/image-20220202112805316.png)

Parser ensures that the program is well formed by performing **syntax checking**. There are three places where a parser is placed in a compiler organization.

1. **Parse Driven Backend** : The parser is works as an autonomous body, not concerned with other processes of a compiler
2.  **Parser Driven Frontend** : The frontend (scanner, semantic analysis) is interleaved with the parser
3.  **Parser Driven Compilation** : Entirety of compilation (scanner, semantic analysis, and code generation) is interleaved with the parser

Although parsers were originally written manually, we not have tools which can automatically generate parsers.



## Syntax Specification

The syntax of a program should be specified such that it is unambiguous, correct and complete, and convenient for both the designer and implementer. **Context Free Grammars** meet these requirements, and are thus used for syntax specification.



$$
G = (N,T,S,P)
$$



$N$ is a set of non-terminals, $T$ is a set of terminals, $S$ is a special nonterminal ($S\in T$) called the start, and $P$ is the set of production rules. A statement is obtained from the given set of rules via a **derivation**.

Its easy to generate a statement from a start state. However, our aim now is to ascertain whether a given statement belongs to a CFG. This is tough to do efficiently as we can’t simply just apply every rule without logic.



$$
\text{type idlist }\implies \text{ integer idlist, id;}
$$



Here, we say that `type idlist` derives `integer idlist, id;`.

| Symbol                     | Meaning                                 |
| -------------------------- | --------------------------------------- |
| $a\implies b$              | $a$ derives $b$ in a single step        |
| $a\overset{*}{\implies} b$ | $a$ derives $b$ in a zero or more steps |
| $a\overset{+}{\implies} b$ | $a$ derives $b$ in a one or more steps  |



### Sentential Forms

A string $\alpha\in (N\cup T)^{\*}$ that is derivable from the start state itself is called a **sentential form** of the CFG $G$. That  is, $S\overset{\*}{\implies} \alpha$ . Note that every sentence is a sentential form but not the other way around. 

> A sentential form is “on its way” towards becoming a sentence



### Leftmost and Rightmost derivations

Denoted by $a\overset{lm}{\implies} b$ and $a\overset{rm}{\implies} b$ respectively. Leftmost derivation is when the leftmost non terminal string is expanded upon. Similarly for rightmost.

![image-20220202122900907](../../../assets/images/typora/image-20220202122900907.png)



A *parse tree* is a pictorial form of representing a derivation. The root of the tree is labeled with the start state ($S$), and each of the leaf nodes is labeled with a terminal or $\epsilon$. The derivation of a parse tree is given by reading its leaves left-to-right.



### Ambiguous Grammars

A grammar is said to be ambiguous when more than one parse tree exists for a derivation. (implying that more than one leftmost, rightmost derivations exist) Note that this is a property of the grammar and not the language itself.

Ambiguities are eradicated via:

- Precedence
- Associativity

&nbsp;



## Parsing Strategies

“Parsing” refers to the technique of building the parse tree. This can be done bottom-up or in a top-down manner. We shall be looking at bottom-up parsing in this course.

**Handle** - A right-sentential form $\gamma$ such that there exists a production rule $A\rightarrow\beta$ and $\beta$ is a substring of $\gamma$.

We shall assume that we know how to detect handles in a string, and proceed with parsing algorithms.

#### Shift Reduce Parsing

There are 4 basic actions of the shift-reduce parser;

1. **Shift** - We move a single lexeme from the input buffer onto the stack until the appearance of a handle
2. **Reduce** - Upon noticing a handle, it is popped and replaced with the LHS of the corresponding production rule
3. **Accept** - The parser accepts the string when the input buffer is empty and the start symbol $S$ is the only symbol present on the stack
4. **Error** - An error is thrown in all other cases, with the string being rejected

This method is also called as LR(0) parsing. Note that $ is used to represent the bottom of the stack and the end of the input buffer string.

#### SLR Parsing

The only difference between SLR parsing and LR parsing is the parsing table. Follow the given parse table blindly for now.
