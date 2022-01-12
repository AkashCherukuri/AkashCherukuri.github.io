---
title: Incremental Construction of Compilers
permalink: /notes/cs302/lec2
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

**Retargetable Compiler** dies not require manual changes, the backend is generated according to the specifications. *the fuck*

A compiler essentially maps Source features to Target features through phases of compilation.

![image-20220107113554537](../../../assets/images/typora/image-20220107113554537.png)

*problem with this?* To solve this, the target features were partitioned but there was no improvement. The source features were partitioned as well *ugh missed entire thing*

Finally, we partition the different "increments" of language to modularly increase the reach of the compiler.

*image*