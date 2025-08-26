# Few-Shot Learning Papers Shortlist

## Core Gradient Descent Implementation
- papers:
  - https://arxiv.org/abs/2212.07677 "Transformers learn in-context by gradient descent" von Oswald et al. 2022
  - https://arxiv.org/abs/2306.09927 "Trained Transformers Learn Linear Models In-Context" Zhang et al. 2023
  - https://arxiv.org/abs/2307.03576 "One Step of Gradient Descent is Provably the Optimal In-Context Learner with One Layer of Linear Self-Attention" Mahankali et al. 2023

summary: Transformers literally implement gradient descent through attention mechanisms - a single linear self-attention layer computes exactly one gradient step on least-squares objectives. Multi-layer transformers implement preconditioned gradient descent with learned preconditioning matrices. The mechanism is provably optimal for linear regression and emerges naturally from training on autoregressive objectives, explaining why transformers excel at in-context learning.

## Mesa-Optimization and Internal Algorithms
- papers:
  - https://arxiv.org/abs/2309.05858 "Uncovering mesa-optimization algorithms in Transformers" Schaeffer et al. 2023
  - https://arxiv.org/abs/2211.15661 "What learning algorithm is in-context learning? Investigations with linear models" Akyürek et al. 2022
  - https://dl.acm.org/doi/10.5555/3666122.3668099 "Transformers learn to implement preconditioned gradient descent for in-context learning" NeurIPS 2023

summary: Transformers discover mesa-optimization during training - implementing subsidiary learning algorithms within their forward pass. They construct internal objectives from context examples and solve them near-optimally, with early layers performing iterative preconditioning and later layers executing gradient steps. The models adaptively select between algorithms (least squares, ridge regression, gradient descent) based on prompt structure.

## Universal Approximation and Turing Completeness
- papers:
  - https://arxiv.org/abs/1912.10077 "Are Transformers universal approximators of sequence-to-sequence functions?" Yun et al. 2019
  - https://arxiv.org/abs/1901.03429 "On the Turing Completeness of Modern Neural Network Architectures" Pérez et al. 2019
  - https://arxiv.org/abs/2411.01992 "Ask, and it shall be given: On the Turing completeness of prompting" 2024

summary: Transformers are universal approximators of continuous permutation-equivariant sequence functions and achieve Turing completeness through hard attention. Recent work proves prompting itself is Turing-complete - there exists a finite transformer that can compute any computable function given the right prompt. This establishes theoretical foundations for the surprising versatility of prompt engineering and in-context learning.

## Bayesian Inference Framework
- papers:
  - https://ai.stanford.edu/blog/understanding-incontext/ "How does in-context learning work? A framework for understanding" Xie et al. 2022
  - https://arxiv.org/abs/2306.04637 "Transformers as Statisticians: Provable In-Context Learning with In-Context Algorithm Selection" Bai et al. 2023

summary: In-context learning performs implicit Bayesian inference, marginalizing over latent task concepts learned during pretraining. Models infer task posterior p(θ|examples) and use it for prediction. Success depends on signal-to-noise ratio between concepts. Random output labels minimally hurt performance (5% degradation), suggesting models primarily use input distributions. Transformers adaptively select statistical algorithms based on context.

## Mechanistic Interpretability Discoveries
- papers:
  - https://transformer-circuits.pub/2023/monosemantic-features "Towards Monosemanticity: Decomposing Language Models With Dictionary Learning" Bricken et al. 2023
  - https://transformer-circuits.pub/2024/scaling-monosemanticity/ "Scaling Monosemanticity: Extracting Interpretable Features from Claude 3 Sonnet" Templeton et al. 2024
  - https://www.neelnanda.io/mechanistic-interpretability/glossary "A Comprehensive Mechanistic Interpretability Explainer & Glossary" Nanda 2023

summary: Induction heads emerge as primary in-context learning mechanism - specialized attention patterns implementing pattern completion. Sparse autoencoders extract monosemantic features from superposition, revealing how transformers encode thousands of concepts in lower dimensions. Transformers decompose into interpretable circuits through path expansion, with each path corresponding to specific computational functions.

## Function Vectors and Task Representations
- papers:
  - https://arxiv.org/abs/2310.15213 "Function Vectors in Large Language Models" Todd et al. 2024
  - https://github.com/ericwtodd/function_vectors "Function Vectors in Large Language Models (ICLR 2024)" Todd et al. 2024

summary: Transformers encode input-output functions as directions in activation space called function vectors. These vectors can be extracted, transplanted between contexts, and composed through arithmetic - adding vectors improves performance on both tasks simultaneously. This reveals tasks as geometric objects in high-dimensional space, with vector operations corresponding to task composition and modification.

## Memory Capacity and Information-Theoretic Bounds
- papers:
  - https://arxiv.org/abs/2405.13718 "Upper and lower memory capacity bounds of transformers for next-token prediction" Tian et al. 2024
  - https://arxiv.org/abs/2408.12186 "Transformers are Minimax Optimal Nonparametric In-Context Learners" 2024

summary: Single-layer transformers achieve Θ(n) memory capacity for n contexts, with tight bounds O(n log n) upper and Ω(n) lower. For nonparametric regression, transformers achieve minimax optimal rates O(n^(-β/(2β+d))) for β-smooth functions in d dimensions. These information-theoretic limits establish fundamental constraints on what transformers can learn from context.

## Statistical Learning Theory and Generalization
- papers:
  - https://proceedings.mlr.press/v202/li23l.html "Transformers as Algorithms: Generalization and Stability in In-context Learning" Li et al. 2023
  - https://arxiv.org/abs/2208.01066 "What Can Transformers Learn In-Context? A Case Study of Simple Function Classes" Garg et al. 2022

summary: Transformers satisfy PAC learning bounds through algorithmic stability, with excess risk bounded by |R(T) - R̂(T)| ≤ 2L√(log(2/δ)/(2M)) for L-Lipschitz stable models. Rademacher complexity provides sequence-length-independent generalization guarantees. Models exhibit phase transitions with depth - single layers implement gradient descent, medium depth achieves ridge regression, deep networks converge to Bayesian estimators.

## Test-Time Training and Adaptation
- papers:
  - https://arxiv.org/abs/2503.11842 "Test-Time Training Provably Improves Transformers as In-context Learners" 2025

summary: Test-time training through gradient updates on context examples provably improves in-context learning performance. The approach combines benefits of parametric optimization with non-parametric in-context learning, achieving better sample complexity than either approach alone. Theoretical analysis shows convergence to optimal predictors under mild conditions.

## Prompt Engineering Theory
- papers:
  - https://arxiv.org/abs/2402.07927 "A Systematic Survey of Prompt Engineering in Large Language Models: Techniques and Applications" 2024
  - https://arxiv.org/abs/2309.03409 "Large Language Models as Optimizers" Yang et al. 2023
  - https://aclanthology.org/2023.findings-emnlp.930/ "Coverage-based Example Selection for In-Context Learning" 2023

summary: Example selection admits optimization through Determinantal Point Processes P(S) ∝ det(K_S) balancing similarity and diversity. Coverage-based selection using BERTScore-Recall yields 17-point improvements on compositional tasks. OPRO treats LLMs as optimizers, using natural language optimization descriptions to iteratively improve prompts (50% improvement on reasoning). Order matters - increasing entropy correlates with better performance.

## Layer-wise Information Processing
- papers:
  - https://arxiv.org/abs/2402.11917 "A Mechanistic Analysis of a Transformer Trained on a Symbolic Multi-Step Reasoning Task" 2024

summary: Information flows through transformer layers in predictable patterns: early layers (1-6) perform task identification and concept encoding, middle layers (7-18) handle information integration and feature composition, late layers (19-24) execute task-specific computations. The residual stream serves as communication highway with all components reading/writing to shared representation, enabling parallel processing of multiple subproblems.

## Classical Theory Connections
- papers:
  - https://games-automata-play.github.io/blog/VC/ "VC dimension, Rademacher complexity, and growth function" 
  - https://thegradient.pub/in-context-learning-in-context/ "In-Context Learning, In Context" 2023

summary: Deep connections exist between transformer in-context learning and classical learning theory. VC dimension and Rademacher complexity frameworks extend to transformer architectures, providing rigorous generalization guarantees. The connection reveals in-context learning as a form of empirical risk minimization with implicit regularization through the transformer architecture itself.

## Historical Context
- papers:
  - https://en.wikipedia.org/wiki/Attention_Is_All_You_Need "Attention Is All You Need - Wikipedia" Vaswani et al. 2017

summary: The original transformer paper introducing self-attention as the primary mechanism, replacing recurrence and convolutions. While not explicitly about few-shot learning, it established the architectural foundation that would later prove capable of implementing learning algorithms internally. The key innovation was scaled dot-product attention enabling dynamic computation based on input context.
