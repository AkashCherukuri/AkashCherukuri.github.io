---
title: "Deep Learning and CNNs"
permalink: /notes/dl/intro
classes: wide
author_profile: false
sidebar:
    nav: "notes_soc"
gallery1:
  - image_path: /assets/images/Soc2021/AlexNet_Res.png
    url: /assets/images/Soc2021/AlexNet_Res.png
    title: "AlexNet"
  - image_path: /assets/images/Soc2021/VGGNet_Res.png
    url: /assets/images/Soc2021/VGGNet_Res.png
    title: "VGG-Net"
  - image_path: /assets/images/Soc2021/ResNet_Res.png
    url: /assets/images/Soc2021/ResNet_Res.png
    title: "ResNet"
gallery2:
  - image_path: /assets/images/Soc2021/AlexNet.png
    url: /assets/images/Soc2021/AlexNet.png
    title: "Modified AlexNet Structure"
  - image_path: /assets/images/Soc2021/VGG-Net.png
    url: /assets/images/Soc2021/VGG-Net.png
    title: "Modified VGG-Net Structure"
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

---
These are the notes made by me while I was trying to implement [this](https://arxiv.org/pdf/1611.07004.pdf) paper. A rigorous mathematical approach is not followed (mainly to streamline the process of note making), rather, I have noted down the concepts and the intuition behind the concepts. Mathematical analysis of the topics covered can be found [here](/notes/dl/resources).

Use the navigation ui on the left to browse through my notes. The results of various netowrks constructed are summarized below.

### Classification Networks' Structure
Three networks based on the structure of [AlexNet](https://papers.nips.cc/paper/2012/file/c399862d3b9d6b76c8436e924a68c45b-Paper.pdf), [VGGNet](https://arxiv.org/pdf/1409.1556.pdf) and [ResNet](https://arxiv.org/pdf/1512.03385.pdf) have been constructed for the MNIST dataset. Their architecture, and graphs comparing their loss with epochs are shown below.

{% include gallery id="gallery1" caption="Graphs for AlexNet, VGG-Net and ResNet respectively" %}
{% include gallery id="gallery2" caption="Modified AlexNet and VGG-Net Architectures"%}

ResNet's architecture is identical to the one described in the above linked paper.
{: .notice--primary}

ResNet has been implemented below. You can press the button to generate two random images and classify them in real time.

(This might take upwards of 30 seconds because heroku app would need to boot up. I only did this because I thought that **executing** a script in a section called "**Executive** Summary" was funny for some reason. That's an entire weekend that I am never getting back.)

<img id="est_img" src="est_img" style="display: none;">
<img id="whut1" src="whut1" style="display: none;">
<div style="text-align: center;">
<button id="Class" class="exec" onClick="classify()"><span>Classify!</span></button>
</div>

&nbsp; 
### Generative Adversial Networks' Architecture

One GAN has been implemented for the MNIST dataset so far. The architectures of the generator and the discriminator are displayed below, along with the "Loss vs Epochs" graph obtained during the training. Do notice that this GAN needed to be trained for much longer than any of the above classification networks.

<!-- Architecture gallery add kro -->
<!-- Image of loss vs epochs for ~100 epochs -->

Again, you can click on the button below to obtain a random output of the network. Not all the generated images resemble a digit, but *most* of them do.

<img id="gen_img" src="gen_img" style="display: none;">
<img id="whut2" src="whut2" style="display: none;">
<div style="text-align: center;">
<button id="Gen" class="exec" onClick="generate()"><span>Generate!</span></button>
</div>

<script>
	var load = "/assets/images/spin.svg"
	function showPic1(){
		document.getElementById("whut1").src = load.replace('90x90', '225x225');
		document.getElementById("whut1").style.display='block';
		document.getElementById('whut1').style.marginLeft='auto';
		document.getElementById('whut1').style.marginRight='auto';
	}

	function showPic2(){
		document.getElementById("whut2").src = load.replace('90x90', '225x225');
		document.getElementById("whut2").style.display='block';
		document.getElementById('whut2').style.marginLeft='auto';
		document.getElementById('whut2').style.marginRight='auto';
	}

	function classify(){
		// Before the image loads
		showPic1()
		document.getElementById('est_img').style.display='none';
		document.getElementById("Gen").disabled = true;
		document.getElementById("Class").disabled = true;
		$.get("https://neural-nets.herokuapp.com/api/soc/class", function(data){
			document.getElementById("est_img").src = "data:image/png;base64, " + data.data;
			document.getElementById('est_img').style.display='block';
			document.getElementById('est_img').style.marginLeft='auto';
			document.getElementById('est_img').style.marginRight='auto';
			document.getElementById("whut1").style.display="none";
			document.getElementById("Gen").disabled = false;
			document.getElementById("Class").disabled = false;
		})
	}

	function generate(){
		// Before the image loads
		showPic2()
		document.getElementById('gen_img').style.display='none';
		document.getElementById("Gen").disabled = true;
		document.getElementById("Class").disabled = true;
		$.get("https://neural-nets.herokuapp.com/api/soc/gen", function(data){
			document.getElementById("gen_img").src = "data:image/png;base64, " + data.data;
			document.getElementById('gen_img').style.display='block';
			document.getElementById('gen_img').style.marginLeft='auto';
			document.getElementById('gen_img').style.marginRight='auto';
			document.getElementById("whut2").style.display="none";
			document.getElementById("Gen").disabled = false;
			document.getElementById("Class").disabled = false;
		})
	}
</script>