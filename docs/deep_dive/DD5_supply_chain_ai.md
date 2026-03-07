# Deep Dive 5: Supply Chain Shock Propagation with AI

How AI models simulate, predict, and mitigate the propagation of shocks through supply chain networks.

---

## 1. Problem Definition

When a disruption hits one firm (natural disaster, factory fire, pandemic lockdown), the shock propagates through the supply chain:
- **Upstream**: firm can't get inputs → production drops
- **Downstream**: firm can't deliver outputs → customers are disrupted
- **Amplification**: indirect losses can be **20x larger** than direct damage (Inoue & Todo 2019)

### Why AI?

| Traditional Approach | Limitation |
|---------------------|-----------|
| Input-output models (Leontief) | Static, no firm-level dynamics |
| Agent-based models (ABM) | Hard to calibrate, slow to simulate |
| Econometric models | Linear assumptions, miss network effects |

AI enables: differentiable simulation for fast calibration, GNN for topology-aware prediction, physics constraints for realistic outputs.

---

## 2. Differentiable Supply Chain ABM in JAX (2025)

**Paper**: Hamid, Moran, Mungo, Quera-Bofarull & Towers
**Links**: [Paper](https://arxiv.org/abs/2511.05231) | [INET Oxford](https://www.inet.ox.ac.uk/publications/a-differentiable-model-of-supply-chain-shocks)

### Core Idea

Make a supply chain agent-based model **differentiable** using JAX, enabling gradient-based Bayesian calibration instead of brute-force search.

### Architecture

```
[1,000-Firm Production Network ABM]
  - Firms as agents with production functions
  - Supply/demand relationships as edges
  - Shock injection → propagation simulation
  ↓
[JAX Implementation]
  - Tensorized across firm agents (GPU parallelization)
  - Automatic differentiation through entire simulation
  ↓
[NumPyro Bayesian Inference]
  - Generalized variational inference
  - Posterior distributions over shock propagation parameters
  ↓
Output: Calibrated model with uncertainty estimates
```

### Key Technical Innovations

| Innovation | Detail |
|-----------|--------|
| **Tensorization** | All firm agents computed in parallel on GPU |
| **Autodiff through ABM** | JAX traces computation graph through time steps |
| **Bayesian calibration** | NumPyro provides posterior distributions, not point estimates |
| **Differentiable economics** | Production functions, inventory, pricing all differentiable |

### Results

| Metric | Performance |
|--------|------------|
| Speed vs. non-differentiable | **>1,000x speed-up** for ABM calibration |
| Scalability | 1,000 firms (extensible) |
| Calibration quality | Efficient Bayesian inference of propagation parameters |

### Why It's Significant

Traditional ABMs are the most realistic supply chain models but nearly impossible to calibrate (requires millions of simulation runs). This work makes calibration tractable, bridging the gap between realistic modeling and practical usability.

---

## 3. Physics-Informed GNN for Supply Chain Disruption (2024)

**Paper**: PI-GNN for Supply Chain Disruption Prediction and Mitigation
**Link**: [Paper](https://www.researchgate.net/publication/399504875)

### Core Idea

Embed **physical laws of supply chains** (conservation of flow, capacity limits, lead times) directly into GNN training via custom loss functions.

### Architecture

```
[Supply Chain Graph]
  Nodes = firms/warehouses
  Edges = supply relationships
  ↓
[Physics-Informed GNN]
  Standard GNN message passing
    +
  Physics constraint losses:
  ├── Conservation of flow: Σ(inflow) = Σ(outflow) + Δinventory
  ├── Capacity constraints: flow ≤ max_capacity
  └── Lead time dependencies: output_t depends on input_{t-τ}
  ↓
[Curriculum Learning]
  Constraint weights increase exponentially during training
  (prevents instability from strict constraints early on)
  ↓
Output: Disruption probability + severity per node + mitigation recommendations
```

### Key Design: Physics Constraints as Loss Terms

```
L_total = L_prediction + λ₁·L_conservation + λ₂·L_capacity + λ₃·L_leadtime

where λ_i increase over training via: λ_i(t) = λ₀ · exp(t/τ)
```

This ensures the model starts by learning patterns freely, then gradually enforces physical consistency.

### Results

| Metric | Standard GNN | PI-GNN | Improvement |
|--------|-------------|--------|-------------|
| AUC-ROC | 0.81 | **0.93** | +15% |
| Disruption detection | baseline | **+21% more detections** | — |
| False alarms | baseline | **-19% fewer** | — |
| Severity F1 (4-class) | 0.68 | **0.84** | +24% |
| Conservation error | baseline | **-87.3%** | — |
| Constraint violations | baseline | **-74.6%** | — |
| Convergence speed | baseline | **2.4x faster** | — |

### Why It's Significant

Standard GNNs can predict disruptions but may output physically impossible results (e.g., more output than input). PI-GNN guarantees physical consistency, which is critical for trust and adoption in supply chain management.

---

## 4. Learning Production Functions with Temporal GNN (AAAI 2025)

**Paper**: Stanford / Leskovec group
**Links**: [Paper](https://arxiv.org/abs/2407.18772) | [AAAI](https://ojs.aaai.org/index.php/AAAI/article/view/35004)

### Core Idea

Supply chains are **temporal production graphs (TPGs)**: firms receive inputs, transform them via production functions, and sell outputs. Learn these production functions from transaction data using temporal GNNs.

### Architecture

```
[Temporal Production Graph]
  Nodes = firms
  Edges = transactions (with timestamps, quantities, products)
  ↓
[SC-TGN (Supply Chain Temporal Graph Network)]
  Extended TGN with:
  ├── Inventory module: tracks material accumulation/depletion
  ├── Production function learning: attention weights encode input→output ratios
  └── Special loss: enforces production function consistency
  ↓
Output:
  1. Inferred production functions per firm
  2. Future transaction forecasts
  3. Shock propagation simulation
```

### Key Innovation: Inventory Module

Standard temporal GNNs don't understand that products accumulate (inventory). SC-TGN adds an explicit inventory state that:
- Increases when inputs arrive
- Decreases when outputs are produced
- Captures the delay between receiving inputs and producing outputs

### Results

| Task | SC-TGN vs. Best Baseline |
|------|-------------------------|
| Production function inference | **6-50% improvement** across datasets |
| Transaction forecasting | **11-62% improvement** across datasets |
| Shock simulation | Generates realistic disruption cascades |

### Open-Source Simulator

**SupplySim**: generates realistic supply chain data with controllable parameters (shock magnitude, network topology, substitutability). Available for benchmarking.

### Why It's Significant

First model to **learn production functions** (the core economic mechanism of supply chains) from data using GNNs. This enables understanding **why** shocks propagate (production dependencies), not just **that** they propagate.

---

## 5. GNN in Supply Chain Analytics (2024 Survey)

**Paper**: arXiv
**Link**: [Paper](https://arxiv.org/html/2411.08550v1)

### Scope

Comprehensive review of GNN applications across supply chain management:

| Application | GNN Role |
|------------|---------|
| Disruption detection | Classify fluctuations from price hikes, supply issues |
| Demand forecasting | Capture spatial dependencies between locations |
| Link prediction | Predict hidden/future supply relationships |
| Network optimization | Route optimization, inventory placement |
| Risk assessment | Identify vulnerable nodes/edges |

### Key Insight

Supply chains are **natural graphs** (firms = nodes, transactions = edges), making GNNs the ideal architecture. But static GNN misses temporal dynamics — temporal GNNs and dynamic graph models are the frontier.

---

## 6. Cross-Method Comparison

| Aspect | Differentiable ABM | PI-GNN | SC-TGN (AAAI) |
|--------|-------------------|--------|----------------|
| **Year** | 2025 | 2024 | 2025 |
| **Approach** | Differentiable simulation | Physics-constrained GNN | Temporal GNN + inventory |
| **Scale** | 1,000 firms | Varies | Varies |
| **Physics** | Production functions (explicit) | Conservation laws (loss terms) | Production functions (learned) |
| **Calibration** | Bayesian (NumPyro) | Supervised + curriculum | Supervised |
| **Speed** | 1,000x vs. non-diff | 2.4x vs. standard GNN | Standard GNN speed |
| **Output** | Parameter posteriors | Disruption + severity | Transactions + production functions |
| **Interpretability** | High (economic model) | High (physics constraints) | High (attention = production ratios) |
| **Code** | Not yet | Not yet | SupplySim (open-source) |

### Complementary Strengths

These three approaches address **different stages** of the supply chain shock problem:

```
SC-TGN: Learn how the supply chain works (production functions)
  ↓
PI-GNN: Predict where disruptions will hit (with physical constraints)
  ↓
Differentiable ABM: Simulate and calibrate full shock propagation scenarios
```

---

## 7. Open Problems & Future Directions

1. **Real-world data scarcity**: Supply chain transaction data is proprietary. SupplySim helps but synthetic data may not capture real complexity. Federated learning across firms is a potential solution.

2. **Multi-product, multi-tier**: Current models simplify to single products or few tiers. Real supply chains have thousands of products and 5-10+ tiers.

3. **Substitution modeling**: When a supplier fails, firms seek alternatives. Modeling this dynamic substitution behavior is critical but underexplored in GNN approaches.

4. **Integration with optimization**: Prediction alone isn't enough. Combining disruption prediction with inventory/routing optimization (predict-then-optimize paradigm) is the practical frontier.

5. **Climate-driven disruptions**: Climate change is increasing disaster frequency. Models need to handle non-stationary shock distributions and correlated multi-region events.

6. **Policy evaluation**: "What if we mandate 2-week inventory buffers?" requires causal/counterfactual reasoning beyond current prediction models. The differentiable ABM is closest to enabling this.

---

## References

- Hamid et al. (2025). Differentiable Supply Chain ABM. [Paper](https://arxiv.org/abs/2511.05231)
- PI-GNN (2024). [Paper](https://www.researchgate.net/publication/399504875)
- SC-TGN (AAAI 2025). [Paper](https://arxiv.org/abs/2407.18772) | [SupplySim](https://cs.stanford.edu/people/jure/pubs/supplychain-gnn-aaai25.pdf)
- GNN Supply Chain Survey (2024). [Paper](https://arxiv.org/html/2411.08550v1)
- Inoue & Todo (2019). Nature Sustainability. [Paper](https://www.nature.com/articles/s41893-019-0351-x)
- Otto et al. (2017). Acclimate. [Paper](https://www.sciencedirect.com/science/article/abs/pii/S0165188917301744) | [Code](https://github.com/acclimate/acclimate)
