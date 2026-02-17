---
title: "Improving Generalization of Deep Networks for Inverse Reconstruction of Image Sequences"
authors:
- admin
# date: "2019-04-07T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2019-06-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: In *International Conference on Information Processing in Medical Imaging (IPMI), 2019*
publication_short: "IPMI 2019"

abstract: While many deep learning based approaches have been proposed for medical image analysis tasks like image reconstruction and classification, the question of generalization of these deep networks remains elusive and little explored in the medical imaging community. In this paper, we propose two ways to improve generalization of an encoder-decoder reconstruction network. First, drawing from analytical learning theory, we theoretically show that a stochastic latent space will improve the ability of a network to generalize to test data outside the training distribution. Second, based on information bottleneck principle, we show that decreasing the mutual information between the latent space and the input data will help a network generalize to unseen input variations. Subsequently, we present a sequence image reconstruction network optimized by a variational approximation of the information bottleneck principle with stochastic latent space. In the application setting of reconstructing the sequence of cardiac transmembrane potential from body-surface potential, we assess the two types of generalization abilities of the presented network against its deterministic counterpart and demonstrate their efficacy. 


# Summary. An optional shortened abstract.
summary: In *International Conference on Information Processing in Medical Imaging (IPMI), 2019*


featured: false

links:
# - name: Custom Link
#   url: http://example.org
url_pdf: https://arxiv.org/pdf/1903.02948
url_code: 'https://github.com/sandeshgh/Improving-Generalization'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: ''
# url_source: '#'
# url_video: '#'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 


# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
# - internal-project

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---

