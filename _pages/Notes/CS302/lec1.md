---
title: Implementation of Programming Languages
permalink: /notes/cs302/lec1
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

**Binding** refers to finding certain attributes of certain objects. There are 6 steps involved here:

1. Conceptualization
2. Coding
3. Compiling
4. Linking - Obtain addresses of external functions, data
5. Loading - Actual addresses of code and data
6. Execution - Variable values, user inputs are obtained. There are no unbound objects at execution stage

We are concerned with the "binding time" taken between the coding and compiling stages.

## Implementation Mechanisms

There are two methods;

1. **Translator** which translates the source program into a target program, after which the machine executes the target program. Two distinct steps are present here, translation and execution. Inputs are taken at execution and not needed at translation.

2. **Interpreter** is a program which takes both source program and Input data to execute the code. 

Note that the source program is never executed directly on the machine in either case. This is because there is a "gap" between the "levels" between the course program and execution. That is, the source code is high-level but the machine operates on low-level.

| Level | State | Operations |
|---|---|---|
|High Level|Variable values|Expressions, control flow|
|Low Level |Register values|Machine Instructions|

- Translator reduces the level of specification to execution level.

- Interpreter raises execution level to specification level. The program (interpreter) executes the code, not the system.

||Translation|Interpretation|
|---|---|---|
||Analysis + Synthesis|Analysis + Execution|
||Bindings before runtime|Bindings at runtime|
|Turn around time| compilation + execution | analysis + execution |

The turnaround time for interpreters is faster, but compilation needs to be done only once for multiple executions, saving time.
{: .notice--info}


|Language|Method|
|---|---|
|C, C++|Compilation (Backend)|
|Java, C#, Python|Interpretation + JIT Compilation (Virtual Machine)|

JIT (Just In Time) Compilation is where a repeated part of the byte code is compiled by the virtual machine for faster execution. Do note that this is done in runtime.

**Frontend** - Language
**Backend** - The machine ISA

$m \text{ frontends } + n\text{ backends } = m\times n \text{ compilers}$

&nbsp;

## Compiler Structure

{% include figure image_path="/assets/images/CS302/compiler.png" caption="Compilation overview" %}


The first two steps in compilation are scanning and parsing. Parsing creates a "concrete Parse tree" with terminal and non-terminal nodes. 

{% include figure image_path="/assets/images/CS302/tree.png" caption="Abstract Syntax Tree" %}

An *abstract syntax tree* (AST) is constructed by the semantic analyzer to ensure that there are no type errors. 

The abstract syntax tree is then used to construct the **TAC list** (Three Address Code). TAC stores the intermediary variables. This linearizes the control flow by flattening the nested control constructs.

{% include figure image_path="/assets/images/CS302/tree_2.png" caption="Compiled sample code" %}

**RTL List** converts the instructions in the TAC list to the ISA. Addresses are still unknown at this stage. RTL List is converted to the **Assembly Code** wherin proper assembly language with register addresses and offsets using ISA.