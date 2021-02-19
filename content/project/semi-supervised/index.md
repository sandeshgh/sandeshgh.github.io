---
title: Regularization and Semi supervised Learning
summary: Apply smoothness based regularization to help semi supervised learning.
tags:
- Learning
- Probabilistic

date: "2016-04-27T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  
  focal_point: Smart

<!-- links:
- icon: twitter
  icon_pack: fab
  name: Follow
  url: https://twitter.com/georgecushen -->
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
<!-- slides: example -->
---

In the presence of small amount of data-labels, how to utilize the unlabeled data in the context of deep learning? This is the question that semi-supervised learning asks. To answer this question, we leverage the idea of the smoothness of classifier with respect to input or with respect to latent representation to regularize the training. Employing ideas from analytical learning theory and function continuity, we show that enforcing the notion of smoothness during training by utlizing unlabeled data improves accuracy.

I am working with Prashnna Kumar Gyawali under superviion of Prof. Linwei Wang in this direction.

## References

1. Gyawali, P.K., Ghimire, S. and Wang, L., 2020. Enhancing Mixup-based Semi-Supervised Learning with Explicit Lipschitz Regularization. arXiv preprint arXiv:2009.11416.

2. Gyawali, P.K., Ghimire, S., Bajracharya, P., Li, Z. and Wang, L., 2020. Semi-supervised Medical Image Classification with Global Latent Mixing. arXiv preprint arXiv:2005.11217.

3. Gyawali, P.K., Li, Z., Ghimire, S. and Wang, L., 2019, October. Semi-supervised learning by disentangling and self-ensembling over stochastic latent space. In International Conference on Medical Image Computing and Computer-Assisted Intervention (pp. 766-774). Springer, Cham.
