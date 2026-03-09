# ai4-impact-propagation

Research survey on **using AI to model, predict, and mitigate Impact Propagation** — how changes, shocks, and failures spread through networks and amplify beyond their origin.

## Motivation

A localized change in a network (e.g., a factory shutdown, a node failure, a viral post) can propagate through connections and produce effects far larger than the initial event. Traditional analytical models struggle with the scale and complexity of real-world networks. **AI approaches (GNN, Deep RL, differentiable simulation)** are enabling breakthroughs in predicting and controlling these propagation dynamics.

## Project Structure

```
docs/
├── 01_cascade_models.md        # Theoretical foundations (threshold, influence maximization)
├── 02_economic_supply_chain.md  # AI for supply chain shock propagation
├── 03_social_network.md         # AI for social influence/information diffusion
├── 04_infrastructure.md         # AI for cascading failure prediction in power grids
├── 05_gnn_based.md              # General GNN methods for propagation modeling
└── deep_dive/
    ├── DD7_mit_research_landscape.md  # MIT research landscape survey
    └── DD8_mit_sdm_research.md        # MIT SDM program related research
```

## Key AI Approaches by Domain

| Domain | AI Method | Key Result | Paper |
|--------|-----------|------------|-------|
| **Supply Chain** | Differentiable ABM (JAX) | **1,000x speed-up** for shock simulation calibration | [Hamid et al. 2025](https://arxiv.org/abs/2511.05231) |
| **Supply Chain** | Physics-Informed GNN | Disruption detection **78% acc** (vs. 52% standard GNN) | [PI-GNN 2024](https://www.researchgate.net/publication/399504875) |
| **Social Network** | GNN + Graph Attention | Influence prediction **outperforms** all feature-engineering baselines | [DeepInf, KDD 2018](https://arxiv.org/abs/1807.05560) |
| **Social Network** | Deep RL + GNN | Seed selection **matches/surpasses SOTA** on large-scale networks | [DGN 2024](https://link.springer.com/article/10.1007/s11227-024-06621-9) |
| **Power Grid** | Hyperparametric Diffusion | Predicts cascades in **unseen grid configurations** | [KDD 2024](https://arxiv.org/abs/2406.08522) |
| **Power Grid** | GNN | Cascade prediction **100x faster** than physics simulation, **98% accuracy** | [GNN 2024](https://arxiv.org/abs/2404.16134) |
| **General** | GNN + PageRank (PPNP) | **Outperforms GCN** with linear complexity | [ICLR 2019](https://arxiv.org/abs/1810.05997) |

## Why AI?

The core propagation problems are:
- **NP-hard** (influence maximization) → AI provides scalable approximations
- **High-dimensional** (millions of nodes/edges) → GNNs naturally encode graph structure
- **Dynamic** (time-evolving networks) → Deep RL adapts to changing topologies
- **Hard to calibrate** (agent-based models) → Differentiable programming enables gradient-based fitting

## Search Keywords

| Concept | Keywords |
|---------|----------|
| AI + Propagation | `graph neural network propagation`, `deep learning cascade prediction` |
| Influence Spread | `influence maximization deep reinforcement learning` |
| Supply Chain | `GNN supply chain disruption`, `differentiable supply chain model` |
| Infrastructure | `cascading failure prediction machine learning`, `GNN power grid` |
| General | `network contagion`, `social contagion`, `shock propagation` |
