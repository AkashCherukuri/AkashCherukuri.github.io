# Semantic Analysis

The constraints defining semantic validity cannot be described by CFGs. Therefore, a different approach is required to handle the semantic validity of a program. 

A **symbol table** is used to hold the names and information regarding variables. This table can be scanned later to check for constraints such as “A variable needs to be declared before it is defined” and the such.



![image-20220314151312640](../../../assets/images/typora/image-20220314151312640.png)

An example of a semantic error found by the Optimizer would be “no return found on any control flow path”. Practical compilers give **warnings** for undefined behaviors. 

![image-20220314151806392](../../../assets/images/typora/image-20220314151806392.png)



&nbsp;

## Syntax Directed Definitions (SDDs)

**Syntax Directed Attribute Evaluation** is used to define attributes of symbols and use them for semantic analysis.


$$
A\to\alpha\vert b=f(c₁,c₂\ldots cₖ)
$$


Here, $b$ is an attribute of $A$ and $cᵢ$ are attributes of the symbols in $\alpha$. Semantic rules are evaluated when the corresponding grammar rule is used for derivation (top-down parser) or reduction (bottom up parser).

Usually, we take attributes called `name`, `value` to be stored in a symbol table called `symtab`.

![image-20220314152607807](../../../assets/images/typora/image-20220314152607807.png)



### SDD for generating code

*didn’t write notes for this, seemed pretty self-explanatory...*
