# Talk Specification: Why & How Does Few-Shot Learning Work

## Context and Audience

**Event**: Week-long workshop on AI in Mathematical Research, University of Augsburg  
**Audience**: Mathematics professors from various universities  
- Diverse mathematical domains
- Basic ML knowledge (know what LLMs are)
- ~60% familiar with transformer architecture
- Comfortable with mathematical formalism

**Format**: 15-minute main talk + 15-minute Q&A  
**Style**: Interactive via Q&A and live Claude demonstrations  
**Goal**: Explain the mathematical principles behind few-shot learning

## Prerequisites for Talk Preparation

Required reading:
1. GPT-3 paper (Brown et al. 2020) - for benchmarks
2. "Transformers learn in-context by gradient descent" (von Oswald et al. 2022)
3. "Uncovering mesa-optimization algorithms" (von Oswald et al. 2023)
4. "What learning algorithm is in-context learning?" (Akyürek et al. 2022)
5. Anthropic interpretability papers (induction heads, superposition)

## Notation Standards

- **a** ∈ ℝ^d: activations
- **w**: weights
- **θ**: parameters  
- **K, Q, V**: Key, Query, Value matrices
- **ℓ**: layer index (ℓ = 1, ..., L)
- **t**: token index
- **d**: residual dimension
- Einstein summation with Σ signs

## Main Talk Structure (15 minutes)

### 1. Introduction: What is Few-Shot Learning? (2 minutes)

**Live demonstrations to show the phenomenon**:

1. **Pattern completion (induction heads)**:
   ```
   "The cat sat on the mat. The dog sat on the..."
   → Model outputs: "mat"
   ```

2. **Zero-shot failure, few-shot success**:
   ```
   Zero-shot: "Extrapolate: 51, 64, 78, 91, 104, ?"
   [Model struggles or fails]
   
   Few-shot: "Pattern: 13n-1
   13×4-1=51
   13×5-1=64
   Continue: 104, ?"
   [Model succeeds: 117]
   ```

3. **Learning notation from examples**:
   ```
   "In my notation:
   ∇[f] means gradient of f
   ⊕ means direct sum
   Now write: The gradient of the direct sum"
   → "∇[f ⊕ g]"
   ```

**Key message**: "Examples transform model behavior - but how?"

### 2. Benchmarks: Quantifying the Effect (2 minutes)

**Show key figures from papers**:

1. **GPT-3 LAMBADA graph** (Brown et al. 2020):
   - Zero-shot: 76%
   - Few-shot: 86.4%
   - Visual: Performance vs model size

2. **SuperGLUE comparison**:
   - GPT-3 (32-shot) beats fine-tuned BERT++
   - No gradient updates needed!

3. **Modern progression table**:
   | Model | Year | Zero-Shot | Few-Shot Gain |
   |-------|------|-----------|---------------|
   | GPT-2 | 2019 | ~30% | +20-30pp |
   | GPT-3 | 2020 | ~50% | +10-20pp |
   | GPT-4 | 2023 | ~80% | +2-8pp |
   | Current | 2024 | ~85% | +1-5pp |

**Transition**: "The effect is real and measurable. Now let's understand the mechanism."

### 3. Theory: Transformer Architecture & Information Flow (2.5 minutes)

**Blackboard-style diagram** (prepare clean visual):

```
Tokens → Embeddings → [Layer 1] → [Layer 2] → ... → [Layer L] → Output token
           ↓              ↓           ↓                ↓
         a₀ ∈ ℝᵈ      a₁ = f₁(a₀)   a₂ = f₂(a₁)      aₗ
                           ↑
                    Attention: Q·K^T·V
```

**Key architectural points**:
- Attention mechanism: `Attention(a) = Σₜ softmax(QₜKₜᵀ)·Vₜ`
- Residual stream: Information highway
- Autoregressive: Append one token at a time
- Causal masking: Only see past tokens

**Critical insight**: "Each layer can read from ALL previous tokens and write to residual stream"

**Show von Oswald equation**:
```
Linear Self-Attention = a + learning_rate · ∇Loss
```
"Attention literally computes gradients!"

### 4. Interpretability: What We've Found Inside (2.5 minutes)

**Key discoveries from mechanistic interpretability**:

1. **Induction Heads** (Anthropic):
   - Specialized circuits for pattern completion
   - Emerge around 2.5B tokens of training
   - Show actual attention pattern visualization

2. **Knowledge Retrieval Circuits**:
   - Early layers: Identify what to retrieve
   - Middle layers: Locate information
   - Late layers: Format output

3. **Function Vectors** (Todd et al. 2024):
   - Tasks encoded as directions in activation space
   - Can be extracted: `v_task = a_with_examples - a_without`
   - Arithmetic works: `v_translate + v_formal = v_formal_translation`

4. **Superposition** (Anthropic):
   - Models pack many "programs" into same weights
   - Sparse features → can fit more than dimensions allow
   - Examples select which "program" to run

**Show circuit diagram** from Anthropic papers if available

### 5. Mathematical Constructions & Limits (2 minutes)

**What we can prove transformers can do**:

1. **Gradient Descent** (von Oswald et al.):
   - Linear self-attention = one GD step (exact!)
   - Multi-layer = preconditioned GD

2. **Beyond GD** (Akyürek et al.):
   - Shallow: Gradient descent
   - Medium: Ridge regression
   - Deep: Bayesian inference (per SLT)
   - Phase transitions with depth

3. **Universal Computation**:
   - Transformers are Turing-complete (with hard attention)
   - Prompting is Turing-complete (2024 result)
   - "Any algorithm you can write, a transformer can learn"

**Limits**:
- Memory: Θ(n) for n examples
- Context window constraints
- Not all problems benefit equally

### 6. Mesa-Optimization: Inner vs Outer Optimizers (2.5 minutes)

**Two optimization loops** (key diagram):

```
OUTER LOOP (Training)          INNER LOOP (Inference)
SGD on parameters θ      →     Attention implements GD
Minimizes training loss  →     Minimizes in-context loss
Updates weights         →     Updates activations
Months of training      →     Single forward pass
```

**Mesa-optimization** (Hubinger et al. 2019):
- Base optimizer: SGD during training
- Mesa-optimizer: GD during inference
- Base objective: Training loss (next-token prediction)
- Mesa-objective: Whatever emerges from context (may differ!)

**Critical insight**: "The model learns HOW to learn, not just WHAT to predict"

**Emergence without design**:
- Never explicitly trained to do optimization
- Emerges from autoregressive training
- Mesa-objective ≠ base objective (alignment problem!)

### 7. Why Few-Shot Works: The Grad Student Analogy (1.5 minutes)

**Few-shot learning works like supervising grad students**:

1. **Examples provide new information**:
   - Not in training data (your specific notation)
   - Updates model's "beliefs" about current task

2. **Present information in computable format**:
   - Examples > descriptions
   - Shows input-output mapping explicitly
   - Model can literally run gradient descent on them

3. **Disambiguate task**:
   - Many valid continuations possible
   - Examples select which "mode" to operate in
   - Like saying "prove this like Bourbaki, not like Arnold"

4. **Trigger knowledge loading (push, not pull)**:
   - Examples activate relevant circuits
   - Function vectors get added to residual stream
   - Knowledge flows from weights → activations
   - Push system: examples determine what loads

**Closing insight**: "When you give examples, you're not teaching the model new facts - you're giving it training data for its internal optimizer to determine what you want."

### Conclusion (0.5 minutes)

"Few-shot learning works because transformers are computers that run learning algorithms. Your examples are the program. The forward pass is the execution. The output is the result of internal optimization. This isn't metaphorical - it's mathematically proven."

## Visual Materials Priority

### Must-Have Figures:
1. GPT-3 LAMBADA scaling graph
2. Token → Activation flow diagram (blackboard style)
3. von Oswald gradient descent equation
4. Inner vs Outer optimizer comparison
5. Anthropic induction head visualization

### Live Demos:
1. Series extrapolation (with/without pattern)
2. Notation learning example
3. Pattern completion demonstration

## Appendix Topics for Q&A

### A1. Detailed Mechanistic Interpretability
- Anthropic's full results on circuits
- Sparse autoencoders and superposition
- Detailed induction head mechanisms

### A2. Statistical Learning Theory Connection
- PAC bounds via algorithmic stability
- Rademacher complexity for transformers
- Why models don't overfit to examples

### A3. Test-Time Training
- Explicit gradient updates at inference
- Combines parametric and non-parametric learning
- Future direction for even better ICL

### A4. Prompt Engineering Theory
- Determinantal Point Processes for example selection
- Order effects (entropy ordering works best)
- Coverage vs similarity tradeoffs

### A5. Failure Modes and Limitations
- When few-shot doesn't help
- Adversarial examples in-context
- Context length limitations

## Key Takeaways

1. Few-shot learning = internal optimization
2. Examples are training data for mesa-optimizer
3. Transformers implement known algorithms (GD, ridge, OLS)
4. Knowledge flows from weights → activations via examples
5. This understanding can improve how we prompt models

## Preparation Checklist

- [ ] Download all paper figures (especially GPT-3, von Oswald, Anthropic)
- [ ] Prepare clean architecture diagram
- [ ] Test all live demos with Claude
- [ ] Create inner vs outer optimizer comparison visual
- [ ] Extract induction head visualizations
- [ ] Prepare backup slides for each appendix topic
- [ ] Time each section carefully
- [ ] Have papers ready to reference

## Success Metrics

✓ Audience understands ICL = optimization, not memorization  
✓ Can explain gradient descent in attention  
✓ Sees connection to their work with grad students  
✓ Knows how to use examples more effectively  
✓ Understands mesa-optimization concept

## Final Note

Remember: This audience will appreciate the mathematical rigor and the connection to optimization theory they already know. The grad student analogy will resonate. Focus on the "transformer as optimizer" narrative throughout - it's not just a model, it's a machine that runs learning algorithms.
