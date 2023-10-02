---
toc: true
comments: true
layout: post
title: Basics js with html
description:
type: plans
courses: { csse: {week: 6}, csp: {week: 0, categories: [4.A]}, csa: {week: 0} }
categories: [C1.4]
---

%%html
<!-- html code goes here (make sure to run) -->
<p id="topParagraph">Link Swap Test.</p>
<a id="link1" href="https://poway.instructure.com">Link 1</a>
<a id="link2" href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">Link 2</a>
<button id="swapButton">Swap Links</button>
<script>
  // your javascript code goes here
  document.addEventListener("DOMContentLoaded", function() {
  const link1 = document.getElementById("link1");
  const link2 = document.getElementById("link2");
  const topPara = document.getElementById("topPara");
  const swapButton = document.getElementById("swapButton");

  swapButton.addEventListener("click", function() 
    const tempHref = link1.href;
    link1.href = link2.href;
    link2.href = tempHref;

    topParagraph.innerHTML = "Switched!";
  });
});