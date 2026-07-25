---
permalink: /science/
title: Science
layout: single
classes: wide
author_profile: false
---

<p class="science-intro">I engineer interpretable AI that reveals why therapies succeed or fail in individual patients, and I translate that insight into better diagnosis and treatment. My work sits at the intersection of artificial intelligence, systems biology, and medicine.</p>

<div class="science-grid">

  <article class="science-card">
    <div class="science-card__media science-card__media--contain"><img src="{{ '/static/assets/img/science/cellwhisperer-abstract.png' | relative_url }}" alt="CellWhisperer: joint embedding of transcriptomes and text" loading="lazy"></div>
    <div class="science-card__text">
      <div class="science-card__num">01</div>
      <h2 class="science-card__title">Multimodal, interpretable AI for biomedical data</h2>
      <p class="science-card__body">Large-scale biomedical data, especially single-cell genomics, has created an analysis bottleneck that keeps biologists from directly interrogating their own data. I conceived and led <strong>CellWhisperer</strong>, a first-of-its-kind multimodal AI that grounds single-cell transcriptomes in natural language, turning explorative analysis into a chat conversation. At Stanford I extended this paradigm to histopathology and cancer immunotherapy with <strong>SpatialWhisperer</strong>. The tools are open-source and accessible through intuitive web apps, and the community is adopting them fast.</p>
      <div class="science-card__works">
        <a href="https://doi.org/10.1038/s41587-025-02857-9" target="_blank" rel="noopener">CellWhisperer · Nature Biotechnology 2025</a>
        <a href="https://doi.org/10.1101/2025.07.14.664402" target="_blank" rel="noopener">SpatialWhisperer · bioRxiv 2025</a>
      </div>
    </div>
  </article>

  <article class="science-card science-card--noimg">
    <div class="science-card__text">
      <div class="science-card__num">02</div>
      <h2 class="science-card__title">Integrative frameworks for functional genomics</h2>
      <p class="science-card__body">Gene expression reflects a combination of regulatory mechanisms that any single assay captures only partially. I build integrative methods that extract robust signals from complex, multimodal datasets. In my PhD I combined orthogonal microRNA target-prediction algorithms with three molecular assays and validated the results with CRISPR-knockout experiments to pinpoint bona fide functional targets. I applied the same integrative philosophy to genome-scale CRISPR screens, from conserved coronavirus host factors to modifications that boost CAR T cell efficacy.</p>
      <div class="science-card__works">
        <a href="https://doi.org/10.1038/s41586-025-09507-9" target="_blank" rel="noopener">CRISPR-boosted CAR T · Nature 2025</a>
        <a href="https://doi.org/10.15252/embr.202254762" target="_blank" rel="noopener">miRNA targets · EMBO Reports 2022</a>
        <a href="https://doi.org/10.1186/s13073-022-01013-1" target="_blank" rel="noopener">Coronavirus host factors · Genome Medicine 2022</a>
      </div>
    </div>
  </article>

  <article class="science-card">
    <div class="science-card__media science-card__media--contain"><img src="{{ '/static/assets/img/science/simulategpt-abstract.png' | relative_url }}" alt="SimulateGPT: LLMs as biomedical simulators" loading="lazy"></div>
    <div class="science-card__text">
      <div class="science-card__num">03</div>
      <h2 class="science-card__title">Simulating and engineering biology with AI</h2>
      <p class="science-card__body">I develop AI tools for designing cells and molecules and for simulating biology. I led a proof-of-concept, <strong>SimulateGPT</strong>, that formulates biomedical problems as "what-if" questions a large language model reasons through step by step, showing that these models can act as qualitative bio-simulators. For molecular design, I built <strong>PAVOOC</strong>, a web application that designs CRISPR gene knockouts directly on 3D protein structures via an AI guide-efficacy algorithm. Together, these turn AI into an interactive instrument for engineering biological systems.</p>
      <div class="science-card__works">
        <a href="https://doi.org/10.1016/j.compbiomed.2024.108796" target="_blank" rel="noopener">SimulateGPT · Comput. Biol. Med. 2024</a>
        <a href="https://doi.org/10.1093/bioinformatics/bty935" target="_blank" rel="noopener">PAVOOC · Bioinformatics 2018</a>
      </div>
    </div>
  </article>

  <article class="science-card">
    <div class="science-card__media science-card__media--contain"><img src="{{ '/static/assets/img/science/cellwhisperer-webui.jpg' | relative_url }}" alt="CellWhisperer web app: querying and visually selecting cells on a UMAP" loading="lazy"></div>
    <div class="science-card__text">
      <div class="science-card__num">04</div>
      <h2 class="science-card__title">Open, impactful, interconnected science</h2>
      <p class="science-card__body">Amid declining trust in scientific institutions, I counter the trend through open science, public engagement, and accessible tools. CellWhisperer was built for democratization: it integrates the open-source CELLxGENE Explorer as a self-deployed public web app, so non-computational users can run sophisticated single-cell analyses. I bring research to non-academic audiences, from the Chaos Communication Congress (38C3) to Vienna's Long Night of Research, and I moderated open-science panels for the OILS Zurich initiative. Through the EU-LIFE postdoc working group I created a funded exchange program for early-career researchers.</p>
      <div class="science-card__works">
        <a href="https://cellwhisperer.bocklab.org/" target="_blank" rel="noopener">CellWhisperer web app</a>
        <a href="{{ '/portfolio/38c3-hacking-life-talk/' | relative_url }}">38C3 talk</a>
      </div>
    </div>
  </article>

</div>
