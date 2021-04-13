---
title: "CS251 - Python"
permalink: /notes/cs251py/
---

### Introduction

---

Python is an interpreted language; meanwhile C++ is a compiled Language.

**Compiling:** Check Syntax -> Semantic Analysis -> Optimizations -> Convert optimized to x86-64 program. This x86-64 program can be run as many times as needed. Semantic Analysis is **Static** in nature.

**Interpretation:** Syntax Analysis -> ByteCode Generator -> ByteCode Optimization. This ByteCode runs on a Virtual Machine Simulator which runs (gets Interpreted) on your laptop. The Semantic Analysis in this case is **dynamic**, meaning that it occurs when the ByteCode is being executed.



### ByteCode Analysis

---

`import dis` is the module to be imported; and to view the ByteCode of a function, do `dis.dis(<function_name>)`.

The output of the corresponding code should be in the format of 5 columns.

| Python Line                                                  | `>>`                                                         | Functions being done                                         | ???                              | Variable name                                                |
| ------------------------------------------------------------ | :----------------------------------------------------------- | ------------------------------------------------------------ | -------------------------------- | ------------------------------------------------------------ |
| Points to the line in the original Python File to which the stack corresponds to | Present means that a pointer (of sorts) is stored to the particular line. Done when a "jump" to the line is needed to be done; usually for `for`, `while` or `else` cases. | All the stuff that the Virtual Machine does at the corresponding line, in sequence. | Address of the variable or smth? | The corresponding variable name in the Python File, or the value of the corresponding constant in the Python File. |





---

To run a python script from the Python Shell; do `exec(open('<YourFile>.py').read())`. After the script has been executed; you can print any variables in the environment without adding `print()` statements and running it again. 

This might help in debugging the code faster.

---

### Operator Hacks

- `x = n // 2` does integer division of `n` and `2`. That means this is similar to `int(n/2)`.



### Usage of Basic Functions

- `print(var, end = '<ending char>')` -- Print `n` and the character in `end` after it. By default; `end = \n`.
- `input(<string>)` -- Prints `<string>` and waits for input in the same line.