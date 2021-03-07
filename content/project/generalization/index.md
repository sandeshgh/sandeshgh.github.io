---
title: Generalization, Robustness and Uncertainty
summary: How to understand and improve generalization and robustness in deep networks?
tags:
- Learning


date: "2016-04-27T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: 

image:
  focal_point: Smart
---

I believe that generalization, robustness and uncertainty are deeply related. I am particularly interested in understanding this relationship from the function space perspective. For example, what is the role of smoothness in each of these? How can we improve robustness and generalization of deep neural networks? How does that affect uncertainty estimation?

My previous works have tried to understand and improve generalization of deep neural networks in the context of medical imaging applications. We have proposed ideas from two perspectives:

1) Generalization by addressing mismatch between training and test distribution

2) Generalization by controlling complexity based on learning theory

Currently, I am exploring the connections in more details, especially using tools from functional analysis and kernel methods.

## References

1. Ghimire, S., Gyawali, P.K. and Wang, L., 2020. Reliable Estimation of Kullback-Leibler Divergence by Controlling Discriminator Complexity in the Reproducing Kernel Hilbert Space. arXiv, pp.arXiv-2002.

2. Ghimire, S., Gyawali, P.K., Dhamala, J., Sapp, J.L., Horacek, M. and Wang, L., 2019, June. Improving generalization of deep networks for inverse reconstruction of image sequences. In International Conference on Information Processing in Medical Imaging (pp. 153-166). Springer, Cham.

3. Ghimire, S., Kashyap, S., Wu, J.T., Karargyris, A. and Moradi, M., 2020, October. Learning invariant feature representation to improve generalization across chest x-ray datasets. In International Workshop on Machine Learning in Medical Imaging (pp. 644-653). Springer, Cham.