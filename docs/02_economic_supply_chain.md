# Economic / Supply Chain Shock Propagation

How shocks propagate through supply chains, and how AI is used to model, predict, and mitigate these effects.

---

## Domain Background

### Acemoglu et al. (2012) - The Network Origins of Aggregate Fluctuations

- **Source**: Econometrica ([paper](https://onlinelibrary.wiley.com/doi/abs/10.3982/ECTA9623))
- **What it does**: Shows how micro-level sector shocks become macro-level fluctuations through input-output network structure.
- **Results**: Aggregate volatility depends on **network asymmetry** — sectors with disproportionate supplier roles amplify shocks.

### Inoue & Todo (2019) - Firm-level Propagation of Shocks through Supply-chain Networks

- **Source**: Nature Sustainability ([paper](https://www.nature.com/articles/s41893-019-0351-x))
- **What it does**: Agent-based simulation on ~1M Japanese firms' supply chains for earthquake scenarios.
- **Results**: Indirect propagation damage = **10.6% of GDP** vs. direct damage = **0.5%** (~20x larger).

### Kashiwagi et al. (2021) - Propagation of Economic Shocks through Global Supply Chains

- **Source**: Review of International Economics ([paper](https://onlinelibrary.wiley.com/doi/10.1111/roie.12541))
- **What it does**: Tests Hurricane Sandy shock propagation internationally via firm-level data.
- **Results**: Domestic propagation is significant; international propagation is dampened by **supplier substitution**.

---

## AI-based Approaches

### Hamid et al. (2025) - A Differentiable Model of Supply-Chain Shocks

- **Source**: arXiv / INET Oxford ([paper](https://arxiv.org/abs/2511.05231))
- **What it does**: Implements a 1,000-firm supply chain ABM in **JAX** for GPU-accelerated differentiable simulation. Uses automatic differentiation + Numpyro for Bayesian calibration.
- **Results**:
  - **>1,000x speed-up** over non-differentiable baselines for ABM calibration.
  - Enables efficient Bayesian inference of shock propagation parameters.
- **Significance**: Makes large-scale supply chain shock simulation tractable for ML pipelines.

### Physics-Informed GNN for Supply Chain Disruption Prediction (2024)

- **Source**: ResearchGate ([paper](https://www.researchgate.net/publication/399504875_Physics-Informed_Graph_Neural_Networks_for_Supply_Chain_Disruption_Prediction_and_Mitigation))
- **What it does**: Embeds physical laws (conservation of flow, capacity constraints, lead time) into GNN training for disruption prediction and mitigation.
- **Results**:
  - Prediction error reduced by **23%** vs. standard models.
  - Disruption detection accuracy: **78%** (vs. 52% for standard GNN).
  - Conservation error reduced by **87.3%**, constraint violations by **74.6%**.
  - **2.4x faster convergence**.

### GNN in Supply Chain Analytics (2024 Survey)

- **Source**: arXiv ([paper](https://arxiv.org/html/2411.08550v1))
- **What it does**: Comprehensive review of GNN applications in supply chain analytics — disruption detection, demand forecasting, link prediction, and optimization.
- **Key finding**: GNNs naturally fit supply chains (firms = nodes, transactions = edges) and capture propagation dynamics that static models miss.

### Learning Production Functions for Supply Chains with GNN (AAAI 2025)

- **Source**: arXiv ([paper](https://arxiv.org/html/2407.18772v1))
- **What it does**: Uses GNN to learn production functions and generate future transactions under supply chain shocks.
- **Key finding**: Static models miss the dynamic propagation of shocks; GNN captures these temporal dynamics.

### Otto et al. (2017) - Acclimate: Agent-Based Loss Propagation Model

- **Source**: Journal of Economic Dynamics and Control ([paper](https://www.sciencedirect.com/science/article/abs/pii/S0165188917301744))
- **What it does**: Open-source ABM simulating cascading economic losses in the global supply network.
- **Results**: Indirect losses ≈ direct losses; mitigated by warehousing and idle capacity.
- **Code**: [GitHub](https://github.com/acclimate/acclimate)
