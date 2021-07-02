---
title: "Recurrent Neural Networks"
permalink: /notes/chemcat/rnn
---
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML" async></script>

<!-- Will do formatting and stuff on Sunday hopefully -->

Recurrent Neural Networks (RNNs) are used in situations where the sequence of data is as important (if not more) than the data itself. These networks essentially have a hidden "state" which stores the data about the information seen so far.

<div class="notice--info">
	RNNs see usage in:
	- Sequence Generation
	- NLP classification
	- NLP generation
</div>

RNNs consist of a looped network whose output is the "hidden state". That is, every word in a sequence of $n$ words is sent one-at-a-time; and at each iteration, the current hidden state is concatenated with the next word in the sequence to form the input.

Sticking with the same example, the "hidden state" gives memory to the network. This is quite useful in the case of NLP, as the meaning of a word quite heavily depends on the words that might have come before it.

<!-- Add an image of RNN if possible? -->

## Drawbacks with RNNs

<div class="notice--warning">
	There are two major drawbacks of RNNs
	- Short term memory due to vanishing gradient
	- One direction is ignored
	These are discussed below
</div>

Consider the sentence "I live in Germany. I speak ______." In this case, it is a very reasonable guess that the person speaks German. And it has been shown that RNNs predict the word "German" with a high degree of accuracy. However, in the sentence "I live in Germany. I am quite fond of watching movies and playing basketball. I am fluent in ______."

In this case, the word "Germany" is very far away from the blank, meaning that it is very likely for the RNN to have dismissed this information. Also, because the network has multiple iterations done, a problem of vanishing gradient arises which makes learning that "Germany" is important infeasible. This is a drawback of the technique.

Another  drawback lies in the very nature of training. The words are input sequentially, meaning that a RNNs do not have information to the data which comes AFTER the word in the sentence. This can cause issues as the meaning of a word depends on what words are present on both of its sides. 

<div style="text-align: center;">
	"I speak _____. I am a German."
</div>

Also, training RNNs is slow because the words are input sequentially. GPUs' strongest suit is parallel processing, and this is not taken advantage of because each word is sent one after another.

<div class="notice--success">
	The above problems are mitigated to some extent via the following procedures respectively:
	- Utilizing LSTM networks
	- BiDirectional techniques such as BERT with Attention
</div>