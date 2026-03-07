# Deep Dive 1: GNN Propagation Mechanisms

How Graph Neural Networks model the propagation process itself — addressing over-smoothing, adaptive kernels, and decoupled architectures.

---

## 1. The Core Problem: Over-Smoothing

As GNN layers increase, node embeddings converge to indistinguishable representations. This limits vanilla GCNs to 2-3 hop neighborhoods, making them **unable to model long-range propagation** — a critical limitation for impact propagation tasks where effects travel many hops.

### Why This Matters for Impact Propagation

- Influence cascades in social networks can span **10+ hops**
- Supply chain shocks propagate through **multi-tier supplier chains**
- Power grid failures cascade across **distant but connected components**

A GNN that cannot "see" beyond 2-3 hops fundamentally cannot model these phenomena.

### Solution Categories (from 2024 Survey: [Oversmoothing Alleviation Survey](https://arxiv.org/abs/2405.01663))

| Strategy | Mechanism | Examples |
|----------|-----------|----------|
| Residual/Dense connections | Preserve earlier layer information | ResGCN, JKNet |
| Normalization | Prevent signal collapse to 1D subspace | PairNorm, NodeNorm |
| Attention | Selectively aggregate relevant neighbors | GAT, Graph Transformer |
| Graph rewiring | Add/remove edges to control propagation speed | SDRF, FoSR |
| Decoupled propagation | Separate feature transform from propagation | **PPNP/APPNP**, **IP-GNN** |

---

## 2. PPNP / APPNP — Predict then Propagate

**Paper**: Klicpera, Bojchevski & Günnemann (ICLR 2019)
**Links**: [Paper](https://openreview.net/pdf?id=H1gL-2A9Ym) | [Code](https://github.com/gasteigerjo/ppnp)

### Key Insight

GCN entangles feature transformation and propagation in every layer. PPNP **decouples** them:

```
Step 1: Predict  →  f_θ(X)        # Neural network produces node predictions
Step 2: Propagate → Π_PPR · f_θ(X) # Personalized PageRank propagates predictions
```

This means:
- The neural network depth is **independent** of propagation range
- Propagation uses Personalized PageRank with teleport probability α
- Each node retains α fraction of its own prediction (prevents over-smoothing)

### Architecture Details

| Component | Specification |
|-----------|--------------|
| Prediction network | 2-layer MLP, 64 hidden units |
| Propagation | Personalized PageRank, α = 0.1 |
| APPNP approximation | K = 10 power iteration steps |
| Regularization | L2 (λ=0.005), dropout (0.5), adjacency dropout |
| Complexity | **O(K · |E|)** — linear in edges per iteration |

### Results (Semi-supervised Node Classification)

| Dataset | GCN | GAT | APPNP | Improvement |
|---------|-----|-----|-------|-------------|
| Cora-ML | 83.3% | 83.5% | **85.1%** | +1.6-1.8% |
| Citeseer | 71.1% | 71.4% | **71.9%** | +0.5-0.8% |
| Pubmed | 79.7% | 78.5% | **80.1%** | +0.4-1.6% |
| MS Academic | 92.6% | 92.3% | **93.2%** | +0.6-0.9% |

- Training time: **on par or faster** than GCN
- Parameters: **on par or fewer** than competitors
- Accuracy **increases and converges** as propagation steps → ∞ (unlike GCN which degrades)

### Why It Matters for Propagation

- Infinite-range propagation without over-smoothing
- The teleport mechanism models how real propagation **attenuates with distance** but doesn't hard-stop
- Direct connection to diffusion processes (PageRank ≈ random walk ≈ diffusion)

---

## 3. IP-GNN — Influence Propagation for Linear Threshold Model

**Paper**: Influence Propagation for Linear Threshold Model with Graph Neural Networks
**Link**: [Paper](https://par.nsf.gov/servlets/purl/10495965)

### Problem Setting

Given a network and a seed set, predict which nodes will be activated after T steps of the **Linear Threshold Model** (LTM):
- Each node has a threshold θ_v
- Node activates when the sum of influence from active neighbors exceeds θ_v
- Process runs for T steps

Traditional approach: Monte Carlo simulation (expensive). IP-GNN learns to predict the outcome directly.

### Architecture

```
Input: Graph G, seed set S, T steps
  ↓
[Adaptive Diffusion Kernel GNN]  ← overcomes 2-3 hop limit
  ↓
[Stack of Fully Connected Layers] ← predicts activation probability per node
  ↓
Output: Predicted set of activated nodes
```

**Adaptive Diffusion Kernel**: Unlike fixed neighborhood aggregation, the kernel adaptively learns the optimal diffusion range. This is critical because LTM propagation at step T requires information from T-hop neighborhoods.

### Training Process

1. Query LTM oracle to generate ground-truth activated node sets
2. Train IP-GNN to minimize prediction error (activated vs. not activated)
3. Use true positive / false positive rates and predicted vs. actual activation counts as metrics

### Results

| Metric | Performance |
|--------|------------|
| Datasets | 4 real-world networks |
| vs. Vanilla GCN | Significantly better (GCN limited to 2-3 hops) |
| Prediction quality | Strong correlation between predicted and actual activated node counts |
| Scalability | Faster than Monte Carlo simulation for large T |

### Why It Matters for Propagation

- **Directly models propagation dynamics** rather than just node classification
- Adaptive kernel automatically learns the right propagation range
- Can replace expensive Monte Carlo simulation for influence estimation

---

## 4. GraphSAP — Data-Driven Propagation Mechanism

**Paper**: Learning Data-Driven Propagation Mechanism for Graph Neural Network (2023)
**Link**: [Paper](https://www.mdpi.com/2079-9292/12/1/46)

### Key Insight

Instead of hand-designing how information flows between GNN layers, **learn the propagation mechanism from data**.

### Architecture

```
Layer 1: GCN + Identity Map → h₁  (1-hop info)
Layer 2: GCN + Identity Map → h₂  (2-hop info)
  ...
Layer L: GCN + Identity Map → h_L  (L-hop info)
  ↓
[Adaptive Layer Fusion]  ← learned weights for combining h₁...h_L
  ↓
Output: Optimally fused multi-scale representation
```

- **Identity map** at each layer: prevents over-smoothing in deep networks
- **Differentiable layer selection**: learns which layers (= which propagation distances) matter most
- Computational cost reduction via differentiable approach (avoids exhaustive search)

### Results

| Property | Performance |
|----------|------------|
| Benchmark datasets | 3 public + 4 additional datasets |
| vs. Baselines | Best on 1 public dataset, competitive on all |
| Deep networks | **Almost no performance degradation** as layers increase |
| Key advantage | Automatically discovers optimal propagation distance per dataset |

### Why It Matters for Propagation

- Different propagation phenomena have different natural ranges — GraphSAP **automatically finds the right range**
- No human tuning needed for propagation depth
- Identity maps preserve source signal, mimicking how real propagation attenuates but retains origin information

---

## 5. Cross-Method Comparison

| Aspect | PPNP/APPNP | IP-GNN | GraphSAP |
|--------|-----------|--------|----------|
| **Core idea** | Decouple predict & propagate via PageRank | Adaptive kernel for LTM simulation | Learn layer fusion weights |
| **Over-smoothing fix** | Teleport (α) preserves local info | Adaptive diffusion range | Identity map + layer selection |
| **Propagation range** | Infinite (PageRank converges) | T-step (matches LTM) | L layers (learned) |
| **Complexity** | O(K·\|E\|) linear | Depends on T | O(L·\|E\|) |
| **Task** | Node classification | Influence prediction | Node classification |
| **Propagation model** | Implicit (PageRank diffusion) | Explicit (LTM) | Implicit (learned) |
| **Code available** | Yes (PyTorch) | No | No |

---

## 6. Open Problems & Future Directions

1. **Dynamic graphs**: All three methods assume static topology. Real propagation networks evolve over time (new edges, node failures). Temporal GNNs (e.g., TGN, TGAT) need integration with these propagation mechanisms.

2. **Heterogeneous propagation**: Different edge types may propagate impacts differently (e.g., supply vs. demand in supply chains). Current methods treat all edges uniformly.

3. **Scalability to billion-node graphs**: APPNP's linear complexity helps, but real-world networks (global supply chains, social platforms) have billions of nodes. Mini-batch training with propagation-aware sampling remains challenging.

4. **Causal vs. correlational propagation**: Current GNNs learn correlational patterns. For intervention (e.g., "which node to protect?"), causal reasoning is needed.

5. **Combining explicit and learned propagation**: IP-GNN uses explicit LTM; PPNP uses implicit PageRank; GraphSAP is fully learned. Hybrid approaches (physics-informed + learned) are a promising direction (see Phase 5: supply chain PI-GNN).

---

## References

- Klicpera et al. (2019). Predict then Propagate: GNN meet Personalized PageRank. ICLR 2019. [Paper](https://openreview.net/pdf?id=H1gL-2A9Ym)
- IP-GNN: Influence Propagation for Linear Threshold Model with GNN. [Paper](https://par.nsf.gov/servlets/purl/10495965)
- GraphSAP: Learning Data-Driven Propagation Mechanism for GNN. Electronics 2023. [Paper](https://www.mdpi.com/2079-9292/12/1/46)
- Oversmoothing Alleviation Survey (2024). [Paper](https://arxiv.org/abs/2405.01663)
- Adaptive Diffusion in GNN. NeurIPS 2021. [Paper](https://keg.cs.tsinghua.edu.cn/jietang/publications/NeurIPS21-Zhao-et-al-ADC-GNN.pdf)
