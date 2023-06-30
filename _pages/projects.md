---
title: "Projects"
permalink: /projects/
layout: splash
---

<!-- divs for the header page -->
<div id="right" class="side">
  <div class="title">
    Getting things done 
    <span id="fancy">right.</span>   
  </div>
</div>
<div id="left" class="side">
  <div class="title">
    Getting things done 
    <span id="fancy">quick.</span>   
  </div>
</div>

<script>
  const left = document.getElementById("left");

  const onMove = e => {
    const perc = e.clientX / window.innerWidth * 100;

    left.style.width = `${perc}%`;
  }

  document.onmousemove = e => onMove(e);
  document.ontouchmove = e => onMove(e.touches[0]);
</script>

<div id="prj-body" style="padding-top: 110vh;">

<!-- Cards for projects and stuff -->
<div id="pcard-body">
  <div class="pcard">
    <div class="pcard-content">Offered a Pre-Placement Offer at Samsung Korea for exceptional performance!</div>
  </div>
  <div class="pcard">
    <div class="pcard-content">Test 2</div>
  </div>
  <div class="pcard">
    <div class="pcard-content">Test 3</div>
  </div>
  <div class="pcard">
    <div class="pcard-content">Test 4</div>
  </div>
</div>

<!-- Handle the effect for changing the highlights of card -->
<script>
document.getElementById("main").onmousemove = e => {
  for(const card of document.getElementsByClassName("pcard")) {
    const rect = card.getBoundingClientRect(),
          x = e.clientX - rect.left,
          y = e.clientY - rect.top;

    card.style.setProperty("--mouse-x", `${x}px`);
    card.style.setProperty("--mouse-y", `${y}px`);
  };
}
</script>



  Page under construction, check back later.

Look at the cool donut while you're here I guess, weee!

<pre id="donut" style="text-align: center;"></pre>
</div>
<!-- This is the code for the rotating donut -->
<script>
function multiplyMatrix(mat1, mat2) {
  // dimensions of matrices
  const dim1 = mat1.length;
  const dim2 = mat2[0].length;

  // check if matrix multiplication is possible
  if (mat1[0].length !== mat2.length) {
    console.error("Matrices cannot be multiplied");
    return null;
  }

  // create result matrix
  const result = new Array(dim1);
  for (let i = 0; i < dim1; i++) {
    result[i] = new Array(dim2).fill(0);
  }

  // multiply matrices
  for (let i = 0; i < dim1; i++) {
    for (let j = 0; j < dim2; j++) {
      for (let k = 0; k < mat1[0].length; k++) {
        result[i][j] += mat1[i][k] * mat2[k][j];
      }
    }
  }

  return result;
}

const INC = 0.08; // Increments of THETA and PHI
const R_TOR = 5;
const R_DON = 2.5;

const pix = ['.', ',', '-', '~', ':', ';', '=', '*', '$', '@'];
const IV = [[-1 / Math.sqrt(3)], [-1 / Math.sqrt(3)], [1 / Math.sqrt(3)]];

const RESO = [18,18]; // Resolution of the screen displaying the torus
const elem = document.getElementById('donut');

function draw_torus(R_x) {
  const screen = Array.from({ length: RESO[0] }, () => Array.from({ length: RESO[1] }, () => ' '));
  const scre_z = Array.from({ length: RESO[0] }, () => Array.from({ length: RESO[1] }, () => -Infinity));

  // Rotation of the torus
  const Rot_x = [    [1, 0, 0],
    [0, Math.cos(R_x), -Math.sin(R_x)],
    [0, Math.sin(R_x), Math.cos(R_x)],
  ];

  let THETA = 0;
  let PHI = 0;
  while (THETA < 2 * Math.PI) {
    while (PHI < 2 * Math.PI) {
      const P = [        [(R_TOR - R_DON * Math.cos(PHI)) * Math.cos(THETA)],
        [(R_TOR - R_DON * Math.cos(PHI)) * Math.sin(THETA)],
        [R_DON * Math.sin(PHI)],
      ];
      P[0][0] = (R_TOR - R_DON * Math.cos(PHI)) * Math.cos(THETA);
      P[1][0] = (R_TOR - R_DON * Math.cos(PHI)) * Math.sin(THETA);
      P[2][0] = R_DON * Math.sin(PHI);

      const rotatedP = multiplyMatrix(Rot_x, P);

      const x = rotatedP[0][0];
      const y = rotatedP[1][0];
      const z = rotatedP[2][0];

      const xc = Math.floor(x + RESO[0] / 2);
      const yc = Math.floor(y + RESO[1] / 2);

      if (z > scre_z[xc][yc]) {
        const norm = [          [-Math.cos(THETA) * Math.cos(PHI)],
          [-Math.sin(THETA) * Math.cos(PHI)],
          [Math.sin(PHI)],
        ];

        const rotatedNorm = multiplyMatrix(Rot_x, norm);

        let illum = 0;
        for (let i = 0; i < 3; i++) {
          illum += rotatedNorm[i][0] * IV[i][0];
        }

        let il_idx = Math.floor(illum / 0.1);
        if(il_idx < 0){
          il_idx = 0;
        }
        screen[xc][yc] = pix[il_idx == 10 ? 9 : il_idx];
        if(screen[xc][yc] == undefined){
          console.error(xc, yc, il_idx);
        }
        scre_z[xc][yc] = z;
      }
      PHI += INC;
    }
    PHI = 0;
    THETA += INC;
  }

  let disp = "";

  for (const row of screen) {
    // disp += (row.join('')) + "\n";
    for (const cr of row) {
      if(cr == NaN){
        console.error("what");
      }
      disp += (cr+cr);
    }
    disp += "\n";
  }

  elem.textContent = disp;

}

let Rot_X = 0;

function print_tor(){
  draw_torus(Rot_X);
  Rot_X -= 0.04;
  if (Rot_X > (2*Math.PI)){
    Rot_X = Rot_X - 2*Math.PI;
  }
}

setInterval(print_tor, 17);
</script>