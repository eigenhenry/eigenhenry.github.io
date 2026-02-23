---
title: "Contribution to Error Analysis of Deep Neural Networks: Case of the Activation Functions"
collection: publications
category: conferences
date: 2025-11-22
venue: "Hal Open Science"
citation: "Cruz, M. L. R., Ruiz-Rohena, K., Guel, Y. I., Salgado, H., Taldir, L., Ramos, E. P., Cervantes, N., Rivero, T., Ceberio, M., Lauter, C., & Volkova, A. (2025). Contribution to Error Analysis of Deep Neural Networks: Case of the Activation Functions."
---
Deep neural networks are widely used in high-stakes applications such as medical imaging and autonomous perception, where numerical reliability is as critical as predictive accuracy. While prior work has focused on gradient stability, the propagation of small floating-point errors through nonlinear network components remains underexplored. This paper provides a quantitative analysis of error amplification in common activation functions, including ReLU, sigmoid, tanh, and softmax. For each function, we evaluate the perturbation response using two complementary approaches: absolute-error analysis, which captures the exact or bounded output change for a given additive input perturbation, and relative-error analysis, which measures the multiplicative amplification of errors relative to the nominal function value. By systematically deriving these bounds and expressions, we compare the numerical behavior across activations. These results enable a detailed description of the error propagation characteristics of each function, offering practical guidance for designing numerically stable and robust neural architectures in contexts where even minor computational errors can significantly affect downstream predictions.
