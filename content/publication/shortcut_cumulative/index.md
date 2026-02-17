---
title: "Enhancing Shortcut Models with Cumulative Self-Consistency Loss for One-Step Diffusion"
authors:
- admin

# date: "2021-09-01T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2026-02-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: In *International Conference in Learning and Representation (ICLR) 2026*
publication_short: "ICLR 2026"

abstract: Although iterative denoising (i.e., diffusion/flow) methods offer strong generative performance, they suffer from low generation efficiency, requiring hundreds of steps of network forward passes to simulate a single sample. Mitigating this requires taking larger step-sizes during simulation, thereby allowing one- or few-step generation. Recently proposed shortcut model learns larger step-sizes by enforcing alignment between its direction and the path defined by a base many-step flow-matching model through a self-consistency loss. However, its generation quality is significantly lower than the base model. In this paper, we interpret the self-consistency loss through the lens of optimal control by formulating the few-step generation as a controlled base generative process. This perspective enables us to develop a general cumulative self-consistency loss that penalizes the misalignment at both the current step and future steps along the trajectory. This encourages the model to take larger step-sizes that not only align with the base model at the current time step but also guide subsequent steps towards high-quality generation. Furthermore, we draw a connection between our approach and reinforcement learning, potentially opening the door to a new set of approaches for few-step generation. Extensive experiments show that we significantly improve one- and few-step generation quality under the same training budget.

# Summary. An optional shortened abstract.
summary: In *International Conference in Learning and Representation (ICLR) 2026*

#tags:
#- Source Themes
featured: false

# links:
# - name: ""
#   url: ""
url_pdf: https://openreview.net/pdf?id=cZqAk87Lu4
url_code: 'https://github.com/paribeshregmi/Shortcut-CSL'
# url_dataset: ''
# url_poster: ''
# url_project: ''
# url_slides: ''
# url_source: ''
# url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---

