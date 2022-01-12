---
title: Compilation Models
permalink: /notes/cs302/lec3
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

There are two broad compilation models:

1. Aho Ullman Model
2. Davidson Fraser Model

![image-20220112111225989](../../../assets/images/typora/image-20220112111225989.png)

Register Transfer is not 3-coded(?), and this means that dependence on machine's hardware is introduced very early on in the Davidson Fraser model.

GCC uses a modified Davidson Fraser Model, where (optimizer, target indep. IR) are present before the expander. This adds machine independent optimization.

&nbsp;

### Typical Front Ends

Scanner, parser and the semantic analyzer form a typical front end of a compiler. The flow of information generally has been shown in the following image.

![image-20220112111718692](../../../assets/images/typora/image-20220112111718692.png)

### Typical Back Ends in Aho Ullman Model

Machine independent optimization is performed upon the IR before generating the code and performing machine dependent optimiation.

**Constant Propagation**: consider the lines `x=5;`, `y=10*x;` and let these be the only places where `x` comes into play. The compiler can then simply replace the second line with `y=10*5;` completely eliminating `x`. This is a compile-time optimization.

![image-20220112112415583](../../../assets/images/typora/image-20220112112415583.png)

Register allocator allocates global registers, while code generator allocates local registers.

Instruction scheduler tries to find the best possible order of instruction execution.

Peephole optimizer ???



### GCC Framework

![image-20220112113158479](image-20220112113158479.png)

