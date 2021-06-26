---
title: "Deep Learning and CNNs"
permalink: /notes/dl/intro
classes: wide
---
<script type="text/javascript" src="https://code.jquery.com/jquery-1.7.1.min.js"></script>


These are the notes made by me while I was trying to implement [this](https://arxiv.org/pdf/1611.07004.pdf) paper. A rigorous mathematical approach is not followed (mainly to streamline the process of note making), rather, I have noted down the concepts and the intuition behind the concepts. Mathematical analysis of the topics covered can be found [here](/notes/dl/resources).

Use the navigation ui on the left to browse through my notes. I have summarized the results of the various networks constructed by me below. 

<img id="est_img" src="est_img" style="display: none;">
<img id="whut1" src="whut1" style="display: none;">
<div style="text-align: center;">
<button onClick="classify()">classify stuff</button>
</div>

<img id="gen_img" src="gen_img" style="display: none;">
<img id="whut2" src="whut2" style="display: none;">
<div style="text-align: center;">
<button onClick="generate()">generate stuff</button>
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
		$.get("https://neural-nets.herokuapp.com/api/soc/class", function(data){
			document.getElementById("est_img").src = "data:image/png;base64, " + data.data;
			document.getElementById('est_img').style.display='block';
			document.getElementById('est_img').style.marginLeft='auto';
			document.getElementById('est_img').style.marginRight='auto';
			document.getElementById("whut1").style.display="none";
		})
	}

	function generate(){
		// Before the image loads
		showPic2()
		document.getElementById('gen_img').style.display='none';
		$.get("https://neural-nets.herokuapp.com/api/soc/gen", function(data){
			document.getElementById("gen_img").src = "data:image/png;base64, " + data.data;
			document.getElementById('gen_img').style.display='block';
			document.getElementById('gen_img').style.marginLeft='auto';
			document.getElementById('gen_img').style.marginRight='auto';
			document.getElementById("whut2").style.display="none";
		})
	}

	window.onload = classify()
	window.onload = generate()
</script>