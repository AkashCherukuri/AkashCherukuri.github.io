---
title: "Deep Learning and CNNs"
permalink: /notes/dl/intro
classes: wide
---
<script type="text/javascript" src="http://code.jquery.com/jquery-1.7.1.min.js"></script>
<script>
	function showPic(){
		var pic = "/assets/images/Soc2021/VGGNet_Est.png"
		document.getElementById('whut').src = pic.replace('90x90', '225x225');
		document.getElementById('whut').style.display='block';
	}
</script>
<script>
	function test(){
		$.get("https://neural-nets.herokuapp.com/api/search/", function(data){
			document.getElementById("test").src = "data:image/png;base64, " + data;
			document.getElementById('whut').style.display='block';
			console.log("data:image/png;base64, " + data);
		})
	}

	window.onload = test()
</script>

These are the notes made by me while I was trying to implement [this](https://arxiv.org/pdf/1611.07004.pdf) paper. A rigorous mathematical approach is not followed (mainly to streamline the process of note making), rather, I have noted down the concepts and the intuition behind the concepts. Mathematical analysis of the topics covered can be found [here](/notes/dl/resources).

Use the navigation ui on the left to browse through my notes. I have summarized the results of the various networks constructed by me below. 

<button onClick="test()">whot</button>
<img id="test" src="test">