---
title: "Noninvasive Reconstruction of Transmural Transmembrane Potential with Simultaneous Estimation of Prior Model Error"
authors:
- admin

# date: "2015-09-01T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2019-03-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["0"]

# Publication name and optional abbreviated publication name.
publication: In *Transactions in Medical Imaging, 2019*
publication_short: "TMI"

# abstract: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum. Sed ac faucibus dolor, scelerisque sollicitudin nisi. Cras purus urna, suscipit quis sapien eu, pulvinar tempor diam. Quisque risus orci, mollis id ante sit amet, gravida egestas nisl. Sed ac tempus magna. Proin in dui enim. Donec condimentum, sem id dapibus fringilla, tellus enim condimentum arcu, nec volutpat est felis vel metus. Vestibulum sit amet erat at nulla eleifend gravida.

# Summary. An optional shortened abstract.
summary: In *Transactions in Medical Imaging, 2019*
#tags:
#- Source Themes
featured: false

# links:
# - name: ""
#   url: ""
# url_pdf: http://arxiv.org/pdf/1512.04133v1
# url_code: ''
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
## Summary
This paper looks at the generation of electrocardiogram (ECG) as a generative process and represents it with a hierarchical graphical model. This allows incorporation of several prior information like knowledge of dynamics of transmembrane potential, possibe error in the dynamic representation, sparsity of the errors, etc. in a common framework of probabilistic graphical model. Then, combining ideas like variational inference and expectation maximization, we propose algorithm to estimate transmembrane potential (TMP) together with possible error. We then go on to analyze the performance of the algorithm by connecting it with machine learning algorithms like relevance vector machine. In addition to principled formulation and rigorous mathematical analysis, this paper has several interesting ideas like using Fenchel duality to obtain lower bound variational approximation of generalized Gaussian distribution, using matrix identities and algebra to obtain time-optimized update equations and analysis of performance in terms of singular values of forward matrix. 

