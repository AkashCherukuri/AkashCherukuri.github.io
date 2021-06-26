---
title: "Deep Learning and CNNs"
permalink: /notes/dl/intro
classes: wide
---
<script type="text/javascript" src="https://code.jquery.com/jquery-1.7.1.min.js"></script>


These are the notes made by me while I was trying to implement [this](https://arxiv.org/pdf/1611.07004.pdf) paper. A rigorous mathematical approach is not followed (mainly to streamline the process of note making), rather, I have noted down the concepts and the intuition behind the concepts. Mathematical analysis of the topics covered can be found [here](/notes/dl/resources).

Use the navigation ui on the left to browse through my notes. I have summarized the results of the various networks constructed by me below. 

<img id="est_img" src="est_img" style="display: none;">
<img id="whut" src="whut" style="display: none;">
<div style="text-align: center;">
<button onClick="test()">whot</button>
</div>

<script>
	var load = "/assets/images/spin.svg"
	function showPic(){
		document.getElementById("whut").src = load.replace('90x90', '225x225');
		document.getElementById("whut").style.display='block';
		document.getElementById('whut').style.marginLeft='auto';
		document.getElementById('whut').style.marginRight='auto';
	}

	function test(){
		// Before the image loads
		showPic()
		document.getElementById('est_img').style.display='none';
		$.get("http://192.168.0.189:5000/api/search/", function(data){
			document.getElementById("est_img").src = "data:image/png;base64, " + data;
			document.getElementById('est_img').style.display='block';
			document.getElementById('est_img').style.marginLeft='auto';
			document.getElementById('est_img').style.marginRight='auto';
			document.getElementById("whut").style.display="none";
		})
	}

	window.onload = test()
</script>