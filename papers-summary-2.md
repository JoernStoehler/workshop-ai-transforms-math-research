# Few-Shot Prompting Benchmarks for Talk

## Primary Source (MUST HAVE)

### GPT-3 Paper (Brown et al. 2020)
**Source**: https://arxiv.org/abs/2005.14165
**Full PDF**: https://arxiv.org/pdf/2005.14165.pdf

**Key Figures to Download**:
- **Figure 1.2**: Performance vs model parameters (shows scaling effect)
- **Figure 1.3**: Zero-shot to few-shot performance progression
- **Figure 3.1**: Visual explanation of zero/one/few-shot learning
- **Figure 3.8**: LAMBADA performance by model size
- **Figure 3.11**: SuperGLUE comparison with BERT

**Key Results**:
- LAMBADA: 76% (0-shot) → 86.4% (few-shot) [+10.4pp improvement]
- SuperGLUE: GPT-3 with 32 examples beats fine-tuned BERT++
- HellaSwag: 78.9% (0-shot) → 79.3% (few-shot)
- Model scaling: 125M → 175B parameters shows consistent improvement

## Benchmark Performance Data

### LAMBADA (Sentence Completion)
| Model | Zero-Shot | Few-Shot | Improvement |
|-------|-----------|----------|-------------|
| GPT-3 125M | 42.7% | 57.0% | +14.3pp |
| GPT-3 1.3B | 47.0% | 72.5% | +25.5pp |
| GPT-3 13B | 56.0% | 83.7% | +27.7pp |
| GPT-3 175B | 76.2% | 86.4% | +10.2pp |

**Key Insight**: Larger models need fewer examples (improvement gap shrinks)

### SuperGLUE (Language Understanding)
| Model | Performance | Notes |
|-------|------------|--------|
| Fine-tuned BERT-Large | 69.0% | Trained on full dataset |
| Fine-tuned BERT++ | 69.8% | State-of-art at time |
| GPT-3 (32-shot) | 71.8% | No fine-tuning needed |
| GPT-3 (0-shot) | 51.4% | Without examples |

### Mathematical/Reasoning Tasks
| Task | Zero-Shot | Few-Shot | Notes |
|------|-----------|----------|-------|
| 2-digit addition | 76.9% | 100% | Perfect with examples |
| 2-digit subtraction | 58.0% | 98.9% | Near-perfect |
| 3-digit addition | 8.4% | 40.6% | Still challenging |

## Modern Model Progression

### GPT Series Evolution
**Sources for comparison graphs**:
- GPT-Fathom paper: https://arxiv.org/abs/2309.16583
- OpenAI Model Cards: https://openai.com/index/gpt-4-research/

| Model | Year | Zero-Shot Capability | Few-Shot Gain |
|-------|------|---------------------|---------------|
| GPT-2 | 2019 | Poor (~30% avg) | +20-30pp |
| GPT-3 | 2020 | Moderate (~50% avg) | +10-20pp |
| GPT-3.5 | 2022 | Good (~65% avg) | +5-15pp |
| GPT-4 | 2023 | Excellent (~80% avg) | +2-8pp |
| GPT-4o/Claude-3.5 | 2024 | Near-human (~85% avg) | +1-5pp |

## Specific Benchmarks to Show

### 1. Scaling Effect Graph
**What to show**: Log-scale plot of performance vs parameters
**Source**: GPT-3 Figure 1.2 or 1.3
**Message**: "Emergence of few-shot learning with scale"

### 2. Zero vs Few-Shot Comparison
**What to show**: Bar chart comparing 0, 1, 5, 32 shots
**Source**: GPT-3 paper tables for any benchmark
**Message**: "Diminishing returns after ~10 examples"

### 3. Task Difficulty Impact
**What to show**: 
- Simple tasks (sentiment): Small improvement
- Complex tasks (reasoning): Large improvement
**Source**: GPT-3 Section 3 results

### 4. Modern Models Comparison
**What to show**: GPT-3 vs GPT-4 on same benchmarks
**Sources**: 
- GPT-4 Technical Report: https://arxiv.org/abs/2303.08774
- GPT-Fathom comparison: https://arxiv.org/abs/2309.16583

## Live Demo Examples

### Linear Interpolation
```
Zero-shot prompt:
"What comes next? 2→7, 5→16, 8→25, 11→?"

Few-shot prompt:
"Pattern: f(x) = 3x + 1
f(2) = 7
f(5) = 16  
f(8) = 25
f(11) = ?"
```
Expected: Zero-shot fails, few-shot succeeds

### Series Continuation
```
Zero-shot: "Continue: 51, 64, 78, 91, 104, ?"
Few-shot: "13×4-1=51, 13×5-1=64, 13×6-1=77... Continue the pattern"
```

### Induction Head Demo
```
"The cat sat on the mat. The dog sat on the"
```
Shows pattern completion (should output "mat")

## Additional Benchmark Sources

### Recent Comparisons (2023-2024)
- **Scaling Laws Analysis**: https://cameronrwolfe.substack.com/p/llm-scaling-laws
  - Shows GPT-3 to O3 progression
    - Includes few-shot scaling curves

    - **PromptHub Guide**: https://www.prompthub.us/blog/the-few-shot-prompting-guide
      - Practical examples of improvement
        - Order effects in few-shot learning

        - **Analytics Vidhya Comparison**: https://www.analyticsvidhya.com/blog/2023/09/power-of-llms-zero-shot-and-few-shot-prompting/
          - LAMBADA benchmark graphs
            - SuperGLUE comparison charts
              - Shows ~12pp improvement on LAMBADA

              ## Key Takeaway Messages

              1. **Consistent Pattern**: 
                 - 0-shot: Baseline performance
                    - 1-shot: +5-10% typical improvement  
                       - Few-shot (5-10): +10-20% improvement
                          - Diminishing returns after 10-15 examples

                          2. **Model Size Matters**:
                             - Smaller models: Need many examples
                                - Larger models: Fewer examples needed
                                   - Modern models: Often work zero-shot

                                   3. **Task Complexity Correlation**:
                                      - Simple tasks: Minimal improvement
                                         - Complex reasoning: Substantial gains
                                            - Novel tasks: Critical for success

                                            ## Figures Download Priority

                                            **Must Have**:
                                            1. GPT-3 Figure 1.2 or 1.3 (scaling)
                                            2. LAMBADA performance table/graph
                                            3. SuperGLUE vs BERT comparison

                                            **Nice to Have**:
                                            4. Task complexity comparison
                                            5. Modern model progression (GPT-3 vs GPT-4)
                                            6. Example ordering effects

                                            ## Quick Reference for Talk

                                            **Opening stat**: "GPT-3 improved 10% on LAMBADA with just 5 examples"

                                            **Core message**: "Few-shot learning works because transformers implement gradient descent internally"

                                            **Closing insight**: "Modern models need fewer examples because they're better optimizers"

                                            ## Paper Citations

                                            ```bibtex
                                            @article{brown2020language,
                                              title={Language models are few-shot learners},
                                                author={Brown, Tom and others},
                                                  journal={NeurIPS},
                                                    year={2020}
                                                    }

                                                    @article{wei2023gptfathom,
                                                      title={GPT-Fathom: Benchmarking Large Language Models},
                                                        author={Wei, Jason and others},
                                                          journal={arXiv preprint arXiv:2309.16583},
                                                            year={2023}
                                                            }
                                                            ```