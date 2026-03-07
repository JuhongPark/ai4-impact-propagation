# Deep Dive 3: Social Influence Prediction with Deep Learning

How deep learning models predict whether a user will be influenced (take an action) based on their social network neighborhood.

---

## 1. Problem Definition

**Social Influence Prediction**: Given a user v and their local network neighborhood, predict whether v will perform a specific action (e.g., adopt a product, share a post, get vaccinated) based on the actions of their neighbors.

This differs from **Influence Maximization** (Phase 2):
- IM asks: "Which seeds maximize total spread?" (optimization)
- Influence Prediction asks: "Will this specific user be activated?" (prediction)

Prediction is a building block for maximization — better prediction enables better seed selection.

---

## 2. DeepInf — Social Influence Prediction with Deep Learning (KDD 2018)

**Paper**: Qiu, Tang, Ma, Dong, Wang & Tang
**Links**: [Paper](https://arxiv.org/abs/1807.05560) | [Code](https://github.com/xptree/DeepInf)

### The Foundational Work

DeepInf is the first major deep learning framework for social influence prediction. It showed that **learned representations outperform hand-crafted features** across multiple social platforms.

### Architecture (Layer by Layer)

```
1. [Ego Network Sampling]
   Random walk with restart from user v → sample n-node local subgraph

2. [Embedding Layer]
   Map each user to D-dimensional representation

3. [Instance Normalization]
   Normalize embeddings (zero mean, unit variance per instance)

4. [Input Concatenation]
   Network embedding + action status indicator + ego indicator + vertex features

5. [Graph Neural Network]  ← interchangeable: GCN or GAT
   Multiple layers of neighborhood aggregation

6. [Output Layer]
   Binary prediction: will user v take the action? (yes/no)
```

### Key Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Input scope | Local ego network (not full graph) | Influence is primarily local; full graph is too expensive |
| Sampling | Random walk with restart | Captures multi-hop neighborhood with locality bias |
| Features | Embedding + action status + ego flag | Minimal but sufficient signal for influence prediction |
| GNN variant | GAT (best) vs. GCN | Attention weights capture heterogeneous edge importance |

### Results (4 Datasets)

| Dataset | Domain | DeepInf-GAT vs. Best Baseline |
|---------|--------|-------------------------------|
| OAG | Academic citation | Significant improvement in AUC and F1 |
| Twitter | Microblogging | Significant improvement in AUC and F1 |
| Weibo | Chinese social media | Significant improvement in AUC and F1 |
| Digg | News aggregation | Significant improvement in AUC and F1 |

- **GAT is critical**: The attention mechanism handles heterogeneous edge types (different relationship strengths) better than uniform GCN.
- **Outperforms**: Feature engineering approaches that use hand-crafted network statistics (degree, clustering coefficient, PageRank, etc.).

### Why It Matters

- Established that **representation learning > feature engineering** for social influence
- The ego-network sampling approach makes it scalable to large networks
- Architecture is modular: swap GCN/GAT, add features, change sampling

---

## 3. HetInf — Heterogeneous Graph Neural Network (2021)

**Paper**: Gao, Wang et al., Frontiers in Physics
**Link**: [Paper](https://www.frontiersin.org/journals/physics/articles/10.3389/fphy.2021.787185/full)

### Motivation

DeepInf treats all nodes and edges as the same type (homogeneous). Real social networks have **multiple node types** (users, events, posts) and **multiple edge types** (follow, like, share, comment). HetInf models this heterogeneity.

### Architecture (3-Module Design)

```
Step 1: Construct heterogeneous relational network
  - User nodes + Event nodes
  - Multiple edge types (user-user, user-event)

Step 2: Sample r-heterogeneous neighbor subgraph
  - Type-aware sampling preserving node/edge diversity

Step 3: Heterogeneous GNN (3 neural modules)
  ├── NN-1: Bi-LSTM       → aggregates temporal/semantic features
  ├── NN-2: GCN            → aggregates heterogeneous node attributes
  └── NN-3: GAT            → learns interaction weights between node types
  ↓
  Influence prediction for target user
```

### Key Innovation

The combination of three specialized modules:
- **Bi-LSTM**: Captures temporal ordering of events (which actions happened first matters)
- **GCN**: Handles multi-type node attributes uniformly
- **GAT**: Learns that different edge types carry different influence weights

### Results

| Dataset | Metric | HetInf vs. DeepInf |
|---------|--------|-------------------|
| Weibo | F1 | **+17.9%** improvement |
| Weibo | Precision | **+35.7%** improvement |
| Digg | F1 | Significant improvement |
| Digg | Precision | Significant improvement |

### Key Insight

Ignoring event-level heterogeneity causes homogeneous models to miss critical influence signals. Users are influenced by **events** (not just other users), and different event types have different influence dynamics.

---

## 4. DeepPP — Personalized Propagation for COVID-19 (2022)

**Paper**: World Wide Web Journal
**Link**: [Paper](https://arxiv.org/abs/2207.13016)

### Motivation

During COVID-19, understanding how pandemic information spreads through social networks became critical. DeepPP extends DeepInf by incorporating **Personalized PageRank propagation** (from PPNP, see DD1) for more accurate influence modeling.

### Architecture

```
DeepInf framework
  +
PPNP/APPNP propagation scheme (PageRank transition probabilities)
  =
DeepPP: Personalized social influence prediction
```

- Uses PageRank transition matrix to weight influence from different neighbors
- Infinite propagation steps without over-smoothing (inherited from PPNP)
- Applied specifically to COVID-19 information diffusion

### Results (6 Datasets)

| Dataset Type | DeepPP Performance |
|-------------|-------------------|
| 4 general social networks | Improved prediction accuracy vs. DeepInf |
| 2 COVID-19 specific datasets | Effective at predicting pandemic information influence |

### Key Insight

Combining DeepInf's local ego-network approach with PPNP's infinite-range personalized propagation creates a model that captures both **local influence dynamics** and **long-range propagation patterns**.

---

## 5. Evolution of Social Influence Prediction

```
Hand-crafted features (degree, PageRank, clustering)
  ↓
Network embedding (DeepWalk, Node2Vec) + classifier
  ↓
DeepInf (2018): End-to-end GNN, GAT attention
  ↓
HetInf (2021): Heterogeneous graphs (users + events)
  ↓
DeepPP (2022): Personalized PageRank propagation
  ↓
Current frontier: Temporal dynamics + multi-platform propagation
```

### Cross-Model Comparison

| Aspect | DeepInf | HetInf | DeepPP |
|--------|---------|--------|--------|
| **Year** | 2018 | 2021 | 2022 |
| **Graph type** | Homogeneous | Heterogeneous (users + events) | Homogeneous + PageRank |
| **GNN core** | GCN / GAT | Bi-LSTM + GCN + GAT | GAT + PPNP |
| **Propagation** | Fixed K-hop | Fixed K-hop | Infinite (PageRank) |
| **Temporal** | No | Yes (Bi-LSTM) | No |
| **Key advance** | First DL approach | Multi-type nodes/edges | Long-range propagation |
| **Code** | Yes | No | No |

---

## 6. Open Problems & Future Directions

1. **Temporal dynamics**: Influence changes over time. When a neighbor acted matters as much as whether they acted. HetInf's Bi-LSTM is a start, but temporal graph networks (TGN, TGAT) offer more principled solutions.

2. **Multi-platform propagation**: Users exist on multiple platforms (Twitter, Reddit, YouTube). Cross-platform influence prediction requires heterogeneous multi-graph models.

3. **Content-aware influence**: Current models focus on network structure. Integrating content features (text, images, sentiment) with graph structure could significantly improve prediction, especially for misinformation.

4. **Causal influence vs. correlation**: A user's neighbors acting similarly doesn't prove influence — it could be homophily (similar people connect). Causal inference methods are needed to distinguish genuine influence from confounding.

5. **Privacy-preserving prediction**: Influence prediction requires access to social graph data, raising privacy concerns. Federated learning approaches for influence prediction are unexplored.

6. **Negative influence / resistance**: Current models predict adoption. Modeling resistance to influence (why some users don't adopt despite heavy exposure) is equally important for understanding propagation barriers.

---

## References

- DeepInf: Qiu et al. (2018). KDD. [Paper](https://arxiv.org/abs/1807.05560) | [Code](https://github.com/xptree/DeepInf)
- HetInf: Gao et al. (2021). Frontiers in Physics. [Paper](https://www.frontiersin.org/journals/physics/articles/10.3389/fphy.2021.787185/full)
- DeepPP (2022). World Wide Web. [Paper](https://arxiv.org/abs/2207.13016)
- PPNP/APPNP: Klicpera et al. (2019). ICLR. [Paper](https://arxiv.org/abs/1810.05997)
