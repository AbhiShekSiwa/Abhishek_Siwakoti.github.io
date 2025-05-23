---
layout: page
title: Aerospace Projects Portfolio
subtitle: From rocket simulations to space robotics
author: Abhishek Siwakoti
permalink: /portfolio/
---

<style>
  body {
    background: linear-gradient(135deg, #ff758c, #ff7eb3, #ffb3c6);
    color: white;
    font-family: 'Segoe UI', sans-serif;
  }

  main {
    padding: 6rem 2rem;
    max-width: 1000px;
    margin: auto;
    line-height: 1.8;
    font-size: 1.1rem;
  }

  .box-highlight {
    background: rgba(255, 255, 255, 0.15);
    padding: 1rem;
    border-radius: 8px;
    margin: 2rem 0;
  }

  h2, h3 {
    color: #fff0f5;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin: 1.5rem 0;
  }

  th, td {
    padding: 0.85rem;
    border: 1px solid rgba(255, 255, 255, 0.3);
    text-align: left;
    color: white;
    background: transparent;
  }

  th {
    font-weight: bold;
    text-align: center;
  }

  blockquote {
    background: rgba(0, 0, 0, 0.15);
    padding: 1rem 1.5rem;
    border-left: 4px solid #ffd6e8;
    border-radius: 6px;
    margin: 1.5rem 0;
    color: #fff;
    font-style: italic;
  }
</style>


Welcome to my aerospace projects portfolio! Each section showcases a different project I’ve worked on, with interactive image galleries to show progress, results, and final implementations.

---

## 🚀 ASEN 2804 Lab 1 – Boost-Glide Vehicle Modeling

As the team leader, I led the design and simulation of a boost-glide vehicle. This involved developing a thrust model from static test data, coding aerodynamic models for lift, drag, and weight, and integrating flight dynamics for the entire trajectory—from launch to glide.

Here is the complete report and presentation slides for ASEN 2804 Lab 1. Use the buttons below to view each slide interactively:

<div id="pdf3-controls" style="text-align:center; margin-bottom: 1em;">
  <button onclick="prevPDFPage3()">⬅ Prev</button>
  <span>Page <span id="pdf3-page-num">1</span> of <span id="pdf3-page-count">?</span></span>
  <button onclick="nextPDFPage3()">Next ➡</button>
</div>

<div style="display: flex; justify-content: center; margin-bottom: 2em;">
  <canvas id="pdf3-canvas" style="border: 1px solid #ccc; max-width: 100%; height: auto;"></canvas>
</div>

<h4 style="text-align:center; margin-top: 2em;">🔧 Exploded CAD Animation (Interactive Slider)</h4>
<p style="text-align:center;">Slide to manually explore the part animation</p>

<div style="text-align:center; margin-bottom: 2em;">
  <img id="frame-slider-image" src="/assets/annimation/Frame001.png"
     style="max-width: 100%; height: 500px; object-fit: contain; border: 1px solid #ccc; border-radius: 6px;" />
  <input type="range" id="frame-slider" min="0" max="95" value="1" style="width: 100%; margin-top: 1em;">
</div>


<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.min.js"></script>
<script>
  const pdf3Url = '/assets/pdfs/2804_Pres.pdf'; // Make sure filename has no spaces
  let pdf3Doc = null, pdf3PageNum = 1, pdf3Rendering = false, pdf3PendingPage = null;
  const pdf3Canvas = document.getElementById('pdf3-canvas');
  const pdf3Ctx = pdf3Canvas.getContext('2d');
  const pdf3Scale = 1.3;

  pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.worker.min.js';

  function renderPDF3Page(num) {
    pdf3Rendering = true;
    pdf3Doc.getPage(num).then(function(page) {
      const viewport = page.getViewport({ scale: pdf3Scale });
      pdf3Canvas.height = viewport.height;
      pdf3Canvas.width = viewport.width;

      const renderContext = { canvasContext: pdf3Ctx, viewport: viewport };
      const renderTask = page.render(renderContext);

      renderTask.promise.then(function() {
        pdf3Rendering = false;
        if (pdf3PendingPage !== null) {
          renderPDF3Page(pdf3PendingPage);
          pdf3PendingPage = null;
        }
      });
    });

    document.getElementById('pdf3-page-num').textContent = num;
  }

  function queueRenderPDF3Page(num) {
    if (pdf3Rendering) {
      pdf3PendingPage = num;
    } else {
      renderPDF3Page(num);
    }
  }

  function prevPDFPage3() {
    if (pdf3PageNum <= 1) return;
    pdf3PageNum--;
    queueRenderPDF3Page(pdf3PageNum);
  }

  function nextPDFPage3() {
    if (pdf3PageNum >= pdf3Doc.numPages) return;
    pdf3PageNum++;
    queueRenderPDF3Page(pdf3PageNum);
  }

  pdfjsLib.getDocument(pdf3Url).promise.then(function(pdfDoc_) {
    pdf3Doc = pdfDoc_;
    document.getElementById('pdf3-page-count').textContent = pdf3Doc.numPages;
    renderPDF3Page(pdf3PageNum);
  });
</script>

---

## 🛠️ ASEN 2803 Lab 1 – VR Roller Coaster G-Force Modeling

For this project, our team designed a virtual roller coaster intended as a pilot simulator using VR goggles. Each group member was responsible for a different track element: a loop, a zero-G parabola, a banked turn, and a braking section. We created MATLAB functions to model the normal, tangential, and lateral G-forces experienced by a cart through these segments and visualized the data to verify safe acceleration limits.

I contributed significantly to the braking and loop sections, handling both derivations and implementation. We validated the loop physics through centripetal force modeling, simulated weightlessness on the parabola with zero normal force, minimized lateral forces on the banked turn through proper geometry, and implemented a constant deceleration profile for braking.

The full MATLAB simulation allowed us to assess g-forces throughout the track, showing our system stayed within safe limits. Key takeaways included learning how to simulate complex motion in MATLAB and understanding the importance of transitions and force smoothing in ride design.

<div class="carousel" id="carousel-1">
  <button class="carousel-btn prev" onclick="plusSlides(-1, 0)">&#10094;</button>
  <div class="carousel-images">
    <img src="/assets/img/asen2803_lab1_Complete_plot.png" class="carousel-image active" alt="Loop simulation">
    <img src="/assets/img/asen2803_lab1_loop_plot.png" class="carousel-image" alt="G-force plot">
    <img src="/assets/img/asen2803_lab1_parabola_plot.png" class="carousel-image" alt="Track profile and segment layout">    
    <img src="/assets/img/asen2803_lab1_banking_plot.png" class="carousel-image" alt="Track profile and segment layout">
  </div>
  <button class="carousel-btn next" onclick="plusSlides(1, 0)">&#10095;</button>
</div>

---

## ⚙️ ASEN 2803 Lab 2 – Locomotive Crank: Modeling & Experimental Validation

In this lab, we investigated the kinematics of a locomotive crank mechanism, which demonstrates general planar motion through a rotating disk and a translating collar. I derived a model that related the disk’s angular position and velocity to the vertical speed of the collar using a combination of geometry and rigid body motion analysis.

We implemented the model in MATLAB (`LCSMODEL.m`) and validated it through simulations. I then analyzed real-world data collected via sensors (a motor encoder and a linear potentiometer), comparing the model predictions to experimental measurements using a structured data processing pipeline (`LCSDATA.m`). Discrepancies between model and experiment were assessed by plotting residuals and computing statistics like mean error and standard deviation.

Key takeaways included identifying noise and small misalignments as dominant error sources, and refining model accuracy by better characterizing system geometry and sensor limitations.

<div class="carousel" id="carousel-2">
  <button class="carousel-btn prev" onclick="plusSlides(-1, 1)">&#10094;</button>
  <div class="carousel-images">
    <img src="/assets/img/asen2803_lab2_model_plot.png" class="carousel-image active" alt="Model: Collar velocity vs angle">
    <img src="/assets/img/asen2803_lab2_experimental_comparison.png" class="carousel-image" alt="Experimental comparison">
    <img src="/assets/img/asen2803_lab2_residuals.png" class="carousel-image" alt="Residuals and error analysis">
  </div>
  <button class="carousel-btn next" onclick="plusSlides(1, 1)">&#10095;</button>
</div>

---

## 🧪 ASEN 2803 Lab 3 – Rotary Arm: PD Control and System Identification

This lab involved developing and validating a closed-loop control model for a rigid rotary arm using a PD (Proportional-Derivative) controller. I derived and simulated the second-order system dynamics in MATLAB, and used both simulation and hardware experiments to analyze the impact of different gain configurations on overshoot and settling time.

Using feedback from potentiometer readings and calculated angular velocities, I tuned proportional and derivative gains to meet performance criteria—less than 20% overshoot and 5% settling within 1 second. Experimental plots were compared to MATLAB simulations to analyze modeling accuracy and physical limitations such as motor saturation and friction.

Additionally, I designed and evaluated a flexible arm system using strain gauge feedback. The system was modeled as a two-DOF spring-mass-damper, and a multi-sensor PD control scheme was implemented. I explored the interaction of flexible dynamics with controller gains, identifying sensor-based corrections to reduce tip displacement.

<div class="carousel" id="carousel-3">
  <button class="carousel-btn prev" onclick="plusSlides(-1, 2)">&#10094;</button>
  <div class="carousel-images">
    <img src="/assets/img/asen2803_lab3_sim_response.png" class="carousel-image active" alt="Simulated response">
    <img src="/assets/img/asen2803_lab3_hardware_response.png" class="carousel-image" alt="Hardware vs sim">
    <img src="/assets/img/asen2803_lab3_control_diagram.png" class="carousel-image" alt="Control diagram">
  </div>
  <button class="carousel-btn next" onclick="plusSlides(1, 2)">&#10095;</button>
</div>

---

<style>
.carousel {
  position: relative;
  max-width: 700px;
  margin: auto;
  margin-top: 1em;
}
.carousel-images {
  position: relative;
  overflow: hidden;
}
.carousel-image {
  display: none;
  width: 100%;
  border-radius: 10px;
}
.carousel-image.active {
  display: block;
}
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(0,0,0,0.4);
  color: white;
  border: none;
  font-size: 2em;
  cursor: pointer;
  padding: 0 12px;
  z-index: 1;
}
.carousel-btn.prev { left: 0; }
.carousel-btn.next { right: 0; }

#frame-slider {
  -webkit-appearance: none;
  width: 100%;
  background: transparent;
  margin-top: 1em;
  height: 2em;
  cursor: pointer;
}
#frame-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  height: 20px;
  width: 20px;
  border-radius: 50%;
  background: white;
  box-shadow: 0 0 5px rgba(0,0,0,0.2);
  border: 1px solid #aaa;
  margin-top: -8px;
}
#frame-slider::-moz-range-thumb {
  height: 20px;
  width: 20px;
  border-radius: 50%;
  background: white;
  box-shadow: 0 0 5px rgba(0,0,0,0.2);
  border: 1px solid #aaa;
}
#frame-slider::-webkit-slider-runnable-track,
#frame-slider::-moz-range-track {
  height: 6px;
  background: transparent;
  border: none;
}
</style>


<script>
let slideIndices = [1, 1, 1]; // Adjust length if you have more/less carousels

function plusSlides(n, carouselIndex) {
  showSlides(slideIndices[carouselIndex] += n, carouselIndex);
}

function showSlides(n, carouselIndex) {
  const carousels = document.querySelectorAll('.carousel');
  const images = carousels[carouselIndex].querySelectorAll('.carousel-image');

  if (n > images.length) slideIndices[carouselIndex] = 1;
  if (n < 1) slideIndices[carouselIndex] = images.length;

  images.forEach(img => img.classList.remove('active'));
  images[slideIndices[carouselIndex] - 1].classList.add('active');
}

document.addEventListener("DOMContentLoaded", () => {
  for (let i = 0; i < slideIndices.length; i++) {
    showSlides(slideIndices[i], i);
  }
});
</script>

<script>
  const frameSlider = document.getElementById('frame-slider');
  const frameImage = document.getElementById('frame-slider-image');

  frameSlider.addEventListener('input', () => {
    let index = parseInt(frameSlider.value, 10);

    // Loop every 48 frames forward
    index = index % 48; // 0–47
    const frameNum = String(index + 1).padStart(3, '0'); // Frame001–Frame048

    frameImage.src = `/assets/annimation/Frame${frameNum}.png`;
  });
</script>

