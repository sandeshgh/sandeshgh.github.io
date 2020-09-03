---
title: "Generative Modeling and Inverse Imaging of Cardiac Transmembrane Potential"
authors:
- admin
# date: "2020-07-01T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2018-09-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["0"]

# Publication name and optional abbreviated publication name.
publication: In *Medical Image Computing and Computer-Assisted Intervention (MICCAI),  2018*
publication_short: In *MICCAI 2018*

# abstract: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum. Sed ac faucibus dolor, scelerisque sollicitudin nisi. Cras purus urna, suscipit quis sapien eu, pulvinar tempor diam. Quisque risus orci, mollis id ante sit amet, gravida egestas nisl. Sed ac tempus magna. Proin in dui enim. Donec condimentum, sem id dapibus fringilla, tellus enim condimentum arcu, nec volutpat est felis vel metus. Vestibulum sit amet erat at nulla eleifend gravida.

# Summary. An optional shortened abstract.
summary: In *Medical Image Computing and Computer-Assisted Intervention (MICCAI),  2018*

featured: false

links:
#- name: Custom Link
#  url: http://example.org
# url_pdf: http://eprints.soton.ac.uk/352095/1/Cushen-IMV2013.pdf
# url_code: '#'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: ''
# url_source: '#'
# url_video: '#'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  focal_point: "Smart"
  preview_only: false

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
## Summary
This paper fuses ideas from hierarchical graphical model and deep learning and performs efficient inference of cardiac transmural Transmembrane potential (TMP). Traditional algorithms in ECGi make use of the dynamics of electric propagation of wavefront inside heart by using electrophysiological (EP) model. While the EP model provides rich information, it comes with disadvantages like difficulty in simulataneous estimation of parameters, necessity to perform sequential estimate of TMP. In this paper, we resolve both of those problems by first learning a hierarchical graphical model whose conditional and prior probability distributions are learnt by using a deep neural network solely from the examples in an unsupervised way. Variational autoencoder is used for this purpose. Later, the learnt probability distributions are used to perform inference. 

