---
title: "Hello."
layout: splash
sitemap: false
header:
  overlay_image: /assets/images/Home/home_head.jpg
  overlay_color: "#141010"
  overlay_filter: 0.6
  actions:
    - label: Github
      url: https://github.com/AkashCherukuri
excerpt: >
  I am Akash Cherukuri, a senior undergraduate in the Computer Science and Engineering department of IIT Bombay.
permalink: /
intro1:
  - excerpt: Feel free to go through the content on my website through the tabs located at the top. You can also search for anything specific. <br> Keep scrolling to learn more about me.
---

{% include feature_row id="intro1" type="center" %}

<!-- Okay so the background image. I've been trying for two years on and off trying to get the image to scroll less compared to the foreground for a much cooler depth effect. I swear I've gone thorugh the stages of grief multiple times over this one thing before learning to let go -->

<!-- In case you do know how to do this, I beg of you to let me know, I will literally give you a shoutout here -->



<!-- Okay I gotta figure out how to add a cursor that blinks, that would be suepr cool imo -->



<div class="container">
  <div class="text">
    <h1>
    <span id="prof" style="color: #f21368;"></span>_
    </h1>
  </div>
  <div class="image">
    <img src="/assets/images/me.jpeg" style="opacity: 0.75; border-radius: 10%;">
  </div>
</div>


<script>
  const languages = ["Machine Learning Enthusiast",
                     "Supportive and Inclusive",
                     "Proactive and self-motivated worker",
                     "Constantly learning and exploring",
                     "Open Source Enthusiast",
                     "Experimental and Adventurous",
                     "Detail-oriented and Perfectionist",
                     "Effective communicator and listener"];
  let langIndex = 0;
  let charIndex = 0;
  const element = document.getElementById('prof');
  
  const back_delay = 50;
  const ford_delay = 300;
  const wait_delay = 600;
  
  let fwd = true;
  let disp_cur = true;
  
  const cursor = '|';
  
  function typestuff(){
    if(fwd){
        if(charIndex <= languages[langIndex].length){
          setTimeout(() => {
            charIndex++;
            element.textContent = languages[langIndex].slice(0, charIndex);
          }, ford_delay);
        }
        else{
          // Wait for a while and then switch modes
          setTimeout(() => {fwd = false}, wait_delay);
        }
    }
    else{
      // We're deleting stuff, so go back with back_delay
        if(charIndex > 0){
          charIndex--;
          element.textContent = languages[langIndex].slice(0, charIndex);
      } 
      else{
        langIndex++;
        if(langIndex >= languages.length){
          langIndex = 0;
        }
        fwd = true;
      }
    }
  }
  
  setInterval(typestuff, back_delay);
</script>


<!-- This is me talking about myself and being all happy happy -->
<br>
<div style="color: #f21368;">
<h1>Sup.</h1>
</div>

Welcome to my website, hope you enjoy your stay. <br> I work on this site whenever inspiration strikes me, so you can expect occasional updates to keep it fresh and relevant.

I am proficient in multiple programming languages including <span style="color: #9be3c3;">C++</span> and <span style="color: #9be3c3;">Python</span>. <br> As a passionate machine learning enthusiast, I am eager to explore the diverse range of applications this field has to offer across various industries and domains.
<br>
I have experience working with various frontend technologies including <span style="color: #9be3c3;">ReactJS</span>, <span style="color: #9be3c3;">Angular</span>, and <span style="color: #9be3c3;">Django</span>, among others. You can find the projects that I have worked on so far in the [Projects](/projects) tab above.

<br>
<div style="color: #f21368;">
<h1>Hobbies.</h1>
</div>



<div class="container">
  <div class="image">
    <img src="/assets/images/dnd.jpg" style="opacity: 0.75; border-radius: 10%;">
  </div>
  <div class="text" style="text-align: left;">
    <p>
      I am interested in Dungeons and Dragons, and I participate in sessions with friends when we all are free. 
    </p>
    <p>
      Recently, I've been exploring the world of 3D printing and modeling as a way to create unique figurines and other captivating trinkets to enhance our gaming campaigns.
    </p>
    <p>
      After a few months of self-guided learning, I've gained proficiency in both <span style="color: #9be3c3;">Fusion360</span> and <span style="color: #9be3c3;">Blender</span>, which has allowed me to bring my imaginative designs to life.
    </p>
    <p>
      There's a picture of us playing DnD together!
    </p>
  </div>
</div>