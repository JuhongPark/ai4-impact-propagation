# Cascade Models (Theoretical Foundations)

Foundational theories on how a small initial change triggers chain reactions across networks. These serve as the **domain knowledge base** that AI approaches build upon.

---

## Watts (2002) - A Simple Model of Global Cascades on Random Networks

- **Source**: PNAS ([paper](https://www.pnas.org/doi/10.1073/pnas.082090499))
- **What it does**: Models how agents on a sparse random network, following a simple threshold rule, produce global cascades from a tiny initial seed.
- **Results**:
  - Two cascade regimes: **power-law** (connectivity-limited) vs. **bimodal** (highly connected — all or nothing).
  - Heterogeneous thresholds → more vulnerable; heterogeneous degree → more robust.
  - Even **random nodes** (not just influencers) can trigger global cascades.
- **Why it matters for AI**: Defines the propagation dynamics that AI models aim to learn and predict.

---

## Kempe, Kleinberg & Tardos (2003) - Maximizing the Spread of Influence through a Social Network

- **Source**: KDD 2003 ([paper](https://www.cs.cornell.edu/home/kleinber/kdd03-inf.pdf))
- **What it does**: Formalizes the Influence Maximization problem under Independent Cascade Model (ICM) and Linear Threshold Model (LTM).
- **Results**:
  - Optimal seed selection is **NP-hard**.
  - Greedy algorithm guarantees **≥63%** of optimal via submodularity.
- **Why it matters for AI**: NP-hardness motivates the use of AI (GNN, RL) to approximate solutions at scale.

---

## Easley & Kleinberg - Chapter 19: Cascading Behavior in Networks

- **Source**: Networks, Crowds, and Markets textbook ([chapter PDF](https://www.cs.cornell.edu/home/kleinber/networks-book/networks-book-ch19.pdf))
- **What it does**: Textbook-level treatment of cascade dynamics, threshold models, and network diffusion.
- **Why it matters for AI**: Provides the conceptual vocabulary (thresholds, contagion, tipping points) used across all AI propagation models.
