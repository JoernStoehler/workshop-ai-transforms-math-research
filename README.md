# Few-Shot Learning Talk - Paper Reference Guide

## Papers in Presentation Order

### 1. Introduction & Benchmarks
**Show the phenomenon with data**

1. **[Language Models are Few-Shot Learners](papers/2005.14165_gpt3_language_models_few_shot.pdf)**  
   Brown et al. (2020) - GPT-3  
   *The foundational paper showing LAMBADA (76.2% → 86.4%), SuperGLUE results, and scaling effects*

2. **[GPT-4 Technical Report](papers/2303.08774_gpt4_technical_report.pdf)**  
   OpenAI (2023)  
   *Modern benchmark comparisons showing reduced few-shot gains as models improve*

3. **[GPT-Fathom: Benchmarking Large Language Models](papers/2309.16583_gpt_fathom.pdf)**  
   Wei et al. (2023)  
   *Comprehensive benchmark comparisons across GPT model generations*

### 2. Core Theory: Gradient Descent in Attention
**The main discovery**

4. **[Transformers Learn In-Context by Gradient Descent](papers/2212.07677_transformers_gradient_descent.pdf)**  
   von Oswald et al. (2022)  
   *CRITICAL: Proves linear self-attention computes exactly one gradient descent step*

5. **[Transformers Learn In-Context by Gradient Descent (duplicate)](papers/2212.07677_transformers_learn_in_context_by_gradient_descent.pdf)**  
   Same paper, duplicate file

### 3. What Algorithms Do Transformers Implement?
**Beyond simple gradient descent**

6. **[What Learning Algorithm is In-Context Learning?](papers/2211.15661_learning_algorithm.pdf)**  
   Akyürek et al. (2022)  
   *Shows transformers implement GD → ridge regression → OLS as depth increases*

7. **[What Can Transformers Learn In-Context?](papers/2208.01066_what_can_transformers_learn.pdf)**  
   Garg et al. (2022)  
   *Empirical study of what function classes transformers can learn from examples*

8. **[Trained Transformers Learn Linear Models In-Context](papers/2306.09927_linear_models.pdf)**  
   Zhang et al. (2023)  
   *Shows transformers learn to implement linear models in their forward pass*

9. **[One Step of Gradient Descent is Provably Optimal](papers/2307.03576_one_step_gradient.pdf)**  
   Mahankali et al. (2023)  
   *Proves single linear self-attention layer is optimal for in-context learning*

### 4. Mesa-Optimization Framework
**The inner vs outer optimizer concept**

10. **[Risks from Learned Optimization](papers/1906.01820_risks_learned_optimization.pdf)**  
   Hubinger et al. (2019)  
   *Introduces mesa-optimization terminology: base/mesa optimizer, inner alignment problem*

11. **[Uncovering Mesa-Optimization Algorithms in Transformers](papers/2309.05858_mesa_optimization.pdf)**  
   von Oswald et al. (2023)  
   *Shows standard training creates internal optimizers through two-stage process*

12. **[On Mesa-Optimization in Autoregressively Trained Transformers](papers/2405.16845_mesa_optimization_emergence.pdf)**  
    Zheng et al. (2024)  
    *Analyzes when and why mesa-optimization emerges from training dynamics*

### 5. Interpretability & Mechanisms

13. **[Function Vectors in Large Language Models](papers/2310.15213_function_vectors.pdf)**  
    Todd et al. (2024)  
    *Tasks encoded as directions in activation space that can be composed*

14. **[Transformers as Statisticians](papers/2306.04637_transformers_statisticians.pdf)**  
    Bai et al. (2023)  
    *Proves transformers perform in-context algorithm selection based on data*

### 6. Theoretical Foundations

15. **[Are Transformers Universal Approximators?](papers/1912.10077_universal_approximators.pdf)**  
    Yun et al. (2019)  
    *Proves transformers are universal approximators of sequence-to-sequence functions*

16. **[On the Turing Completeness of Modern Neural Networks](papers/1901.03429_turing_completeness.pdf)**  
    Pérez et al. (2019)  
    *Shows transformers with hard attention are Turing complete*

17. **[Ask, and It Shall Be Given: Prompting is Turing Complete](papers/2411.01992_prompting_turing_complete.pdf)**  
    (2024)  
    *Recent proof that prompting alone achieves Turing completeness*

### 7. Memory and Optimization Bounds

18. **[Upper and Lower Memory Capacity Bounds of Transformers](papers/2405.13718_memory_capacity.pdf)**  
    Tian et al. (2024)  
    *Proves Θ(n) memory capacity for n examples in single-layer transformers*

19. **[Transformers are Minimax Optimal Nonparametric In-Context Learners](papers/2408.12186_minimax_optimal.pdf)**  
    (2024)  
    *Shows transformers achieve minimax optimal rates for nonparametric regression*

### 8. Prompt Engineering & Practical Aspects

20. **[A Systematic Survey of Prompt Engineering](papers/2402.07927_prompt_engineering_survey.pdf)**  
    (2024)  
    *Comprehensive survey of prompt engineering techniques and their effectiveness*

21. **[Large Language Models as Optimizers](papers/2309.03409_llms_as_optimizers.pdf)**  
    Yang et al. (2023)  
    *OPRO: Using natural language to optimize prompts iteratively*

22. **[Test-Time Training Provably Improves In-Context Learning](papers/2503.11842_test_time_training.pdf)**  
    (2025)  
    *Explicit gradient updates at inference time improve few-shot performance*

23. **[A Mechanistic Analysis of a Transformer](papers/2402.11917_mechanistic_analysis.pdf)**  
    (2024)  
    *Layer-by-layer breakdown of how transformers process information*

## Additional Resources (Web Only - See .md files)

- **[Anthropic Transformer Circuits](papers/transformer_circuits_monosemantic_2023.md)** - Induction heads discovery
- **[Scaling Monosemanticity](papers/transformer_circuits_scaling_2024.md)** - Superposition and feature extraction
- **[Stanford Blog on Bayesian Framework](papers/stanford_blog_bayesian_framework.md)** - ICL as Bayesian inference
- **[Various practical guides](papers/)** - See other .md files for web resources

## Quick Navigation for Talk

### Opening (Benchmarks)
- Start with [GPT-3 paper](papers/2005.14165_gpt3_language_models_few_shot.pdf) - Figures 1.2, 3.1, 3.8

### Core Theory
- [von Oswald 2022](papers/2212.07677_transformers_gradient_descent.pdf) - The key equation
- [Akyürek 2022](papers/2211.15661_learning_algorithm.pdf) - Algorithm progression with depth

### Mesa-Optimization
- [Hubinger 2019](papers/1906.01820_risks_learned_optimization.pdf) - Terminology
- [von Oswald 2023](papers/2309.05858_mesa_optimization.pdf) - Evidence

### For Q&A
- Have all papers above ready to reference
- Particularly the theory papers for mathematical questions