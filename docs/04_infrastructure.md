# Infrastructure Cascading Failure Prediction & Mitigation

How AI predicts and prevents cascading failures in infrastructure networks like power grids.

---

## AI-based Approaches

### Hyperparametric Diffusion Model for Cascading Failure Prediction (KDD 2024)

- **Source**: KDD 2024 ([paper](https://arxiv.org/abs/2406.08522))
- **What it does**: Models cascading failures in power grids as an information diffusion process. Uses a stochastic hyperparametric IC model that correlates diffusion weights with physics-based contagion probabilities between transmission lines.
- **Results**:
  - Learns failure propagation patterns from historical cascade traces.
  - Can predict diffusion in **unseen grid configurations** (where existing methods fail due to lack of training data).
  - Provides actionable guidance to **strengthen grids** and reduce large-scale cascade risk.
  - Improved sample complexity bounds over existing methods.

### GNN for Power Failure Cascade Prediction (2024)

- **Source**: IEEE / arXiv ([paper](https://arxiv.org/abs/2404.16134))
- **What it does**: Flow-free GNN model that predicts grid states at every generation of a cascade, given an initial contingency and power injection values.
- **Results**:
  - **Outperforms** multiple influence-model baselines across loading profiles.
  - Computational time reduced by **~100x** vs. physics-based simulation.
  - Predicts failure size, final grid state, and failure time steps per branch.

### Cascading Blackout Severity Prediction with GNN (2024)

- **Source**: Electric Power Systems Research ([paper](https://www.sciencedirect.com/science/article/abs/pii/S0378779624006242))
- **What it does**: Statistically-augmented GNN for predicting cascading blackout severity.
- **Results**: Classification accuracy of **98%**, precision of **96%** (4% false positive rate).

### ML for Cascading Failure Prediction in Power Systems (2025)

- **Source**: arXiv ([paper](https://arxiv.org/html/2503.00567v1))
- **What it does**: Surveys ML techniques (SVM, Random Forest, Neural Networks, Deep Learning) applied to cascading failure prediction in power grids.

### Hybrid Learning for Fault Prediction and Cascading Failure Mitigation (2025)

- **Source**: Scientific Reports ([paper](https://www.nature.com/articles/s41598-025-10304-7))
- **What it does**: Couples adversarial learning with graph-structured predictive models. Generative networks synthesize fault evolution patterns; graph neural architectures capture spatiotemporal correlations.

### Cascading Failure Prediction via Causal Inference (2024)

- **Source**: arXiv ([paper](https://arxiv.org/html/2410.19179v1))
- **What it does**: Uses causal inference methods to predict cascading failures, moving beyond correlation-based approaches.

---

## Domain Background

### Motter & Lai (2002) - Cascade-based Attacks on Complex Networks

- **Source**: Physical Review E ([paper](https://www.semanticscholar.org/paper/Cascade-based-attacks-on-complex-networks.-Motter-Lai/8d8c8bcb08ef27b860ae08aae205abc274862b2c))
- **Key result**: A **single high-load node** removal can collapse an entire heterogeneous network.

### Smolyak et al. (2020) - Mitigation of Cascading Failures

- **Source**: Scientific Reports ([paper](https://www.nature.com/articles/s41598-020-72771-4))
- **Key result**: Local-structure-based node protection outperforms standard mitigation techniques.

### Cascading Failures in Complex Networks (2020 Review)

- **Source**: Journal of Complex Networks ([paper](https://academic.oup.com/comnet/article/8/2/cnaa013/5849333))
- **Summary**: Comprehensive review of cascade models (threshold, load redistribution, sandpile).
