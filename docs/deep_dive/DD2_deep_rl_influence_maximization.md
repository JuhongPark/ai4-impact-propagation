# Deep Dive 2: Deep Reinforcement Learning for Influence Maximization

How RL agents learn to select seed nodes that maximize the spread of influence (impact) through a network.

---

## 1. Problem Formulation

**Influence Maximization (IM)**: Given a network G and a budget k, find k seed nodes whose activation maximizes the total number of eventually activated nodes under a diffusion model (IC or LTM).

- Classical result: NP-hard (Kempe et al. 2003), greedy gives 63% approximation but is **too slow** for large networks (requires many Monte Carlo simulations per candidate).
- **Why Deep RL?** RL naturally handles sequential selection (pick one seed at a time), and GNNs encode graph structure — together they provide **scalable, adaptive** seed selection.

### MDP Formulation

| MDP Component | Design |
|---------------|--------|
| **State** | Current graph with node embeddings + already selected seeds |
| **Action** | Select next seed node from remaining candidates |
| **Reward** | Marginal influence gain from adding this seed (or final total spread) |
| **Episode** | Terminates after k seeds are selected |
| **Policy** | GNN encodes graph → Q-network or policy network outputs node scores |

Key challenge: reward is **expensive to compute** (requires diffusion simulation) and **sparse** (only meaningful after full seed set is selected or after simulation).

---

## 2. DGN — Dual Graph Neural Network (2024)

**Paper**: Wang & Cao, Journal of Supercomputing, 2024
**Link**: [Paper](https://link.springer.com/article/10.1007/s11227-024-06621-9)

### Architecture

```
Input Graph
  ↓
[Dual Coupled GNNs]  ← two GNNs capturing different structural views
  ↓
Node Embeddings (context-rich vector representations)
  ↓
[Deep Q-Network (DQN)]  ← approximates Q(state, action)
  ↓
Sequential Seed Selection (greedy over Q-values)
```

- **Dual GNNs**: Two coupled graph neural networks explore topology AND node attributes simultaneously, producing richer embeddings than single-GNN approaches.
- **DQN**: Learns Q-function without prior knowledge of network properties. Adaptively selects optimal strategy based on current state.
- **No supervision needed**: Unlike supervised methods, DGN learns entirely from interaction with the diffusion simulator.

### Results

| Metric | DGN Performance |
|--------|----------------|
| vs. ToupleGDD (SOTA) | **Matches or surpasses** influence spread |
| Robustness | **Better robustness** on dense, complex networks |
| vs. Traditional (Degree, K-shell, Genetic, PSO) | Significantly higher influence with much lower execution time |
| Scalability | Suitable for large-scale dense social networks |

### Key Contribution
First to demonstrate that dual-GNN architecture + DQN can achieve SOTA performance while being more robust to network density variations.

---

## 3. BiGDN — Bidirectional Graph Deep Network (2025)

**Paper**: Expert Systems with Applications, 2025
**Links**: [Paper](https://www.sciencedirect.com/science/article/abs/pii/S0957417425000065) | [Code](https://github.com/zwl1985/BiGDN)

### Architecture

```
[Pre-training Phase]
  Influence prediction regression task → initial node embeddings
  ↓
[Node Encoder (NE)]
  GNN + Bidirectional Neighborhood Aggregation
  ↓
  Structural + influence feature embeddings
  ↓
[Q-Network (QN)]
  DRL-based sequential seed selection
  ↓
  Seed set S (|S| = k)
```

- **Bidirectional aggregation**: Captures both incoming and outgoing influence patterns (critical for directed networks where influence flows asymmetrically).
- **Pre-training**: Initializes embeddings via influence prediction regression, giving the RL agent a warm start.
- **BiGDNs (simplified)**: Knowledge distillation variant for faster inference on very large networks.

### Results (9 Real-world Datasets)

| Comparison | Result |
|-----------|--------|
| vs. IMM (traditional) | **Comparable effectiveness**, significantly better efficiency |
| vs. Other DRL methods | **Superior results** on most datasets |
| Generalization | Adapts across different network sizes and structures |
| BiGDNs | Maintains quality with improved efficiency via distillation |

### Key Contribution
Bidirectional aggregation + pre-training + knowledge distillation = end-to-end framework that balances quality, speed, and generalization.

---

## 4. BIM-DRL — Balanced Influence Maximization (2024)

**Paper**: Neural Networks, 2024
**Link**: [Paper](https://www.sciencedirect.com/science/article/abs/pii/S0893608023005841)

### Motivation

Standard IM maximizes **total** influence but may concentrate spread in one community while ignoring others. BIM-DRL ensures **balanced** influence across communities/entities.

### Architecture

```
[Entity Correlation Evaluation Module]
  Users' historical behavior sequences → entity correlation scores
  ↓
[Balanced Seed Selection Module]
  DRL agent optimizes: max balanced_influence(S)
  where balanced_influence considers spread across ALL communities
  ↓
  Seed set with fair/balanced propagation
```

- **Entity correlation**: Models how influence on one entity affects others (e.g., promoting product A may reduce interest in product B).
- **Balanced objective**: Reward function penalizes uneven spread across communities.

### Results (6 Real-world Datasets)

| Metric | BIM-DRL Performance |
|--------|-------------------|
| Balanced influence spread | **Superior** to all baselines |
| Balanced propagation accuracy | **Best** across datasets |
| vs. Standard IM methods | Achieves balance without major sacrifice in total spread |

### Key Contribution
First to address **fairness in propagation** via DRL. Important for applications where equitable impact distribution matters (public health, policy).

---

## 5. HEDRL-IM — Evolutionary DRL for Hypergraph IM (2024)

**Paper**: Information Sciences, 2024
**Links**: [Paper](https://www.sciencedirect.com/science/article/abs/pii/S0020025524016785) | [Code](https://github.com/1873177187/HEDRL-IM)

### Motivation

Standard graphs use pairwise edges. But real influence often involves **group interactions** (a meeting activates everyone present, a group chat reaches all members). **Hypergraphs** model these higher-order relationships where a single hyperedge connects multiple nodes simultaneously.

### Architecture

```
[Hypergraph Linear Threshold Model]  ← propagation on hyperedges
  ↓
[DQN]  ← models node influence scores
  ↓
[Dynamic MDP]  ← sequential seed selection
  ↓
[Evolutionary Algorithm]  ← optimizes DQN weights (avoids local optima)
```

- **Hyperedge propagation**: When a hyperedge's active fraction exceeds a threshold, ALL remaining nodes in that hyperedge activate simultaneously.
- **Evolutionary + RL hybrid**: Evolutionary algorithm explores DQN weight space globally, while RL fine-tunes locally. Overcomes DRL's tendency to get stuck in local optima.
- **Estimated influence feature**: Addresses the sparse reward problem in hypergraph LTM.
- **Simulation optimization**: Reduces redundant fitness simulations for efficiency.

### Results (16 Synthetic + 9 Real-world Hypergraphs)

| Metric | HEDRL-IM Performance |
|--------|---------------------|
| vs. SOTA methods | **0.3% to 30% improvement** in influence spread |
| Effectiveness | Best seed selection across hypergraph datasets |
| Higher-order propagation | Successfully captures group-level activation dynamics |

### Key Contribution
First DRL method for influence maximization on hypergraphs. Demonstrates that ignoring higher-order interactions leads to suboptimal seed selection.

---

## 6. Cross-Method Comparison

| Aspect | DGN | BiGDN | BIM-DRL | HEDRL-IM |
|--------|-----|-------|---------|----------|
| **Year** | 2024 | 2025 | 2024 | 2024 |
| **Network type** | Undirected/directed graphs | Directed graphs | Graphs with communities | Hypergraphs |
| **RL method** | DQN | DQN + pre-training | DRL | DQN + evolutionary |
| **GNN design** | Dual coupled GNNs | Bidirectional aggregation | Entity correlation module | Hypergraph-aware |
| **Unique feature** | Robustness on dense nets | Knowledge distillation | Fairness/balance | Higher-order interactions |
| **Code available** | No | Yes | No | Yes |
| **Scalability** | Large-scale | Very large (distilled) | Medium | Medium (evolutionary cost) |

### Evolution of the Field

```
Kempe 2003 (Greedy, 63% approx)
  ↓
CELF / CELF++ (lazy evaluation speedup)
  ↓
ToupleGDD 2023 (first competitive DRL)
  ↓
DGN 2024 (dual GNN, matches SOTA)
BiGDN 2025 (bidirectional, scalable)
BIM-DRL 2024 (fairness-aware)
HEDRL-IM 2024 (hypergraph extension)
```

---

## 7. Open Problems & Future Directions

1. **Scalability to billion-node networks**: Even DRL methods struggle at web-scale. BiGDN's distillation approach is promising but not yet tested at billions of nodes.

2. **Dynamic networks**: All current methods assume static topology. Real social networks have evolving edges. Temporal RL (e.g., integrating TGN with DQN) is unexplored.

3. **Multi-diffusion competition**: Real platforms have competing campaigns. Multi-agent RL for competitive influence maximization is an open frontier.

4. **Reward efficiency**: Diffusion simulation for reward computation is the bottleneck. Learned reward models (surrogate models) could dramatically speed up training.

5. **Transfer across networks**: Training on one network and deploying on another. BiGDN shows some generalization, but principled transfer learning for IM remains open.

6. **Negative propagation**: Current methods focus on positive influence spread. Modeling and mitigating negative cascade (misinformation, failure) via RL is emerging but underdeveloped.

---

## References

- DGN: Wang & Cao (2024). Journal of Supercomputing. [Paper](https://link.springer.com/article/10.1007/s11227-024-06621-9)
- BiGDN (2025). Expert Systems with Applications. [Paper](https://www.sciencedirect.com/science/article/abs/pii/S0957417425000065) | [Code](https://github.com/zwl1985/BiGDN)
- BIM-DRL (2024). Neural Networks. [Paper](https://www.sciencedirect.com/science/article/abs/pii/S0893608023005841)
- HEDRL-IM (2024). Information Sciences. [Paper](https://www.sciencedirect.com/science/article/abs/pii/S0020025524016785) | [Code](https://github.com/1873177187/HEDRL-IM)
- ToupleGDD (2023). [Paper](https://www.researchgate.net/publication/370786286)
- Kempe, Kleinberg & Tardos (2003). KDD. [Paper](https://www.cs.cornell.edu/home/kleinber/kdd03-inf.pdf)
