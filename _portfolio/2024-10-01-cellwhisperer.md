---
title: "CellWhisperer"
date: 2024-10-01
description: "A multimodal AI system that enables chat-based analysis of single-cell RNA sequencing data, published in Nature Biotechnology (2025)."
tags: [Publication]
media:
  - type: video
    src: https://medical-epigenomics.org/papers/schaefer2025cellwhisperer/video/TutorialNarrated.mp4
  - type: image
    src: /static/assets/img/portfolio/cellwhisperer-the-scientist.png
  - type: link
    src: https://www.linkedin.com/posts/christoph-bock_wanna-talk-to-your-cells-try-out-cellwhisperer-activity-7252972812900966400-YoZC
    label: Original LinkedIn post
  - type: link
    src: https://www.the-scientist.com/an-ai-lab-partner-helps-sift-through-transcriptomics-data-72415
    label: The Scientist article
---

CellWhisperer is a multimodal AI system that enables chat-based analysis of single-cell RNA sequencing data. It aligns transcriptomic embeddings with natural language representations, allowing researchers to query gene expression profiles in plain English. A fine-tuned LLM chat assistant interprets these aligned representations, supporting free-text search, annotation, and interactive exploration of transcriptome datasets without writing code.

The system was trained on over one million bulk and pseudo-bulk transcriptomes with AI-curated textual annotations from GEO and CELLxGENE Census. CellWhisperer integrates into a modified CELLxGENE Explorer interface, where users type queries such as "Show me structural cells with immune functions" and receive scored, color-coded results across all cells in a dataset. Selecting a cell cluster and prompting "Describe these cells in detail" produces a natural language characterization grounded in the underlying expression data.

In a benchmarked comparison, CellWhisperer completed a dataset exploration workflow more than four times faster than conventional bioinformatics. The tool supports analysis of large public datasets including Tabula Sapiens and GEO collections.

Published in Nature Biotechnology (2025). Open-source training data, web application for public datasets, and local installation for private data are available.

- [Paper (Nature Biotechnology, open access)](https://www.nature.com/articles/s41587-025-02857-9)
- [Web app: cellwhisperer.bocklab.org](https://cellwhisperer.bocklab.org/)
- [Code: github.com/epigen/CellWhisperer](https://github.com/epigen/CellWhisperer)
- [Coverage: The Scientist](https://www.the-scientist.com/an-ai-lab-partner-helps-sift-through-transcriptomics-data-72415)
