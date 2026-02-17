---
title: "Learning Object-Centric Dynamic Modes from Video and Emerging Properties"
authors:
- admin

# date: "2021-09-01T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2023-03-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: In *Learning for Dynamics and Control 2023*
publication_short: "L4DC 2024"

abstract: One of the long-term objectives of Machine Learning is to endow machines with the capacity of structuring and interpreting the world as we do. This is particularly challenging in scenesinvolving time series, such as video sequences, since seemingly different data can correspond to the same underlying dynamics. Recent approaches seek to decompose video sequences into their composing objects, attributes and dynamics in a self-supervised fashion, thus simplifying the task of learning suitable features that can be used to analyze each component. While existing methods can successfully disentangle dynamics from other components, there have been relatively few efforts in learning parsimonious representations of these underlying dynamics. In this paper, motivated by recent advances in non-linear identification, we propose a method to decompose a video into moving objects, their attributes and the dynamic modes of their trajectories. We model video dynamics as the output of a Koopman operator to be learned from the available data. In this context, the dynamic information contained in the scene is encapsulated in the eigenvalues and eigenvectors of the Koopman operator, providing an interpretable and parsimonious representation. We show that such decomposition can be used for instance to perform video analytics, predict future frames or generate synthetic video. We test our framework in a variety of datasets that encompass different dynamic scenarios, while illustrating the novel features that emerge from our dynamic modes decomposition- Video dynamics interpretation and user manipulation at test-time. We successfully forecast challenging object trajectories from pixels, achieving competitive performance while drawing useful insights.

# Summary. An optional shortened abstract.
summary: In *Annual Conference on Learning for Dynamics and Control, 2023*

#tags:
#- Source Themes
featured: false

# links:
# - name: ""
#   url: ""
url_pdf: https://proceedings.mlr.press/v211/comas23a/comas23a.pdf
# url_code: 'https://github.com/sandeshgh/Reliable-KL-estimation'
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

