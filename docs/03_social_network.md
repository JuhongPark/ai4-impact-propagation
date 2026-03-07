# Social Network Influence / Information Propagation

How AI models learn to predict and optimize the spread of information, influence, and behavior through social networks.

---

## AI-based Approaches

### DeepInf (KDD 2018) - Social Influence Prediction with Deep Learning

- **Source**: KDD 2018 ([paper](https://arxiv.org/abs/1807.05560)) | [Code](https://github.com/xptree/DeepInf)
- **What it does**: End-to-end framework that takes a user's local network as input to a GNN (graph attention network) to learn latent social representations for predicting whether a user will perform a specific action.
- **Results**:
  - **Significantly outperforms** traditional feature engineering approaches on Open Academic Graph, Twitter, Weibo, and Digg.
  - DeepInf-GAT achieves best AUC and F1 scores across all datasets.
- **Significance**: First major demonstration that deep representation learning works for social influence prediction.

### DeepPP (2022) - Personalized Propagation for COVID-19 Social Influence

- **Source**: World Wide Web Journal ([paper](https://arxiv.org/abs/2207.13016))
- **What it does**: Extends DeepInf with personalized propagation via PageRank transition probabilities to predict COVID-19 social influence.
- **Results**: Improved prediction of influence spread for pandemic-related information.

### HetInf (2021) - Social Influence Prediction with Heterogeneous GNN

- **Source**: Frontiers in Physics ([paper](https://www.frontiersin.org/journals/physics/articles/10.3389/fphy.2021.787185/full))
- **What it does**: Applies heterogeneous graph neural networks to predict user-level influence in social networks with multiple node/edge types.
- **Results**: Captures dynamic propagation patterns in heterogeneous networks better than homogeneous GNN baselines.

### Deep RL for Influence Maximization (2024-2025)

- **DGN** ([paper](https://link.springer.com/article/10.1007/s11227-024-06621-9)): Dual Graph Neural Network + Deep RL for seed selection. Performance matches or **surpasses state-of-the-art** (ToupleGDD) with better robustness on large-scale dense networks.
- **BiGDN** ([paper](https://www.sciencedirect.com/science/article/abs/pii/S0957417425000065)): End-to-end DRL + GNN framework. Significant improvements in computational efficiency; scales to large networks.
- **BIM-DRL** ([paper](https://www.sciencedirect.com/science/article/abs/pii/S0893608023005841)): Balanced Influence Maximization via DRL for fair influence spread across network communities.
- **HEDRL-IM** ([paper](https://www.sciencedirect.com/science/article/abs/pii/S0020025524016785)): Evolutionary DRL for influence maximization in **hypergraphs**, considering higher-order propagation in hyperedges.

---

## Domain Background

### Independent Cascade Model Survey (2024)

- **Source**: arXiv ([paper](https://arxiv.org/html/2405.10322v1))
- **Summary**: Comprehensive survey of ICM from origin to modern variants (negative opinions, competitive diffusion, time-decay).

### Comprehensive Review of Propagation Models (2024)

- **Source**: arXiv ([paper](https://arxiv.org/html/2410.02118v1))
- **Summary**: Reviews models from deterministic (SIR, SIS, threshold) to deep learning (GNN). GNNs achieve **breakthrough performance** on large-scale networks.

### Higher-order Network Propagation (2024)

- **Source**: Physics Letters A ([paper](https://www.sciencedirect.com/science/article/abs/pii/S0375960124006637))
- **Summary**: Higher-order interactions (simplicial complexes) significantly amplify propagation speed and reach.
