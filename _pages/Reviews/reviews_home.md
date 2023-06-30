---
title: "Video Game Reviews"
layout: splash
sitemap: false
header:
  overlay_image: /assets/images/Reviews/voli.jpg
  actions:
    - label: Guide
      url: /reviews/about/
permalink: /reviews/
excerpt: >
  I plan on mentioning a few games I enjoy here.
---


<div style="text-align: center;">
    <button class="image-button" style="background-image: url(/assets/images/KatanaZero/kz_but_disp.jpg);"
            onclick="location.href = '/reviews/KatanaZero';">
        <span class="button-text">Katana Zero <br> Review</span>
    </button>
</div>

---
<div class="gameSumm">
  <div class="buttonBox">
    <button class="image-button" style="background-image: url(/assets/images/Reviews/outerWilds/outer_wilds.jpg);"
            onclick="location.href = 'https://store.steampowered.com/app/753640/Outer_Wilds/';">
        <span class="button-text">Outer Wilds <br> Steam</span>
    </button>
  </div>
  <div class="summ" style="color: #ff7d25; font-weight: bold;">
    Interstellar Archeology, Timeloop Nihilism, and inevitability of death. <br>
    You explore a solar system trying to uncover its mysteries while fighting against the flow of time. <br>
    It is an experience like none other, and I often wish I could play it again for the first time. <br>
  </div>
</div>
---

<script>
  // Get all gameSumm elements
  var gameSumms = document.querySelectorAll('.gameSumm');

  // Add event listener to each gameSumm
  gameSumms.forEach(function(gameSumm) {
      gameSumm.addEventListener('mouseenter', function(event) {
          // Get the corresponding buttonBox element
          var buttonBox = event.currentTarget.querySelector('.buttonBox');
          var summ = event.currentTarget.querySelector('.summ');

          // Update widths and display properties
          buttonBox.style.width = '40%';
          summ.style.display = 'block';
          summ.style.width = '60%';

          // Wait for the transition to finish, then fade in the text
          setTimeout(function() {
              summ.style.opacity = '1';
          }, 300); // 300ms is the duration of the width transition
      });

      gameSumm.addEventListener('mouseleave', function(event) {
          // Get the corresponding buttonBox element
          var buttonBox = event.currentTarget.querySelector('.buttonBox');
          var summ = event.currentTarget.querySelector('.summ');

          // Reset widths and display properties
          buttonBox.style.width = '100%';
          summ.style.display = 'none';
          summ.style.width = '0';
          summ.style.opacity = '0';
      });
  });
</script>