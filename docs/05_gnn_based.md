# GNN-based Propagation Modeling (General Methods)

General-purpose Graph Neural Network methods for learning and predicting propagation dynamics, applicable across all domains.

---

## IP-GNN - Influence Propagation for Linear Threshold Model with GNN

- **Source**: NSF ([paper](https://par.nsf.gov/servlets/purl/10495965))
- **What it does**: Simulates T-step influence propagation of the Linear Threshold Model using a GNN with adaptive diffusion kernel. Overcomes GCN's over-smoothing problem (limited to 2-3 hops).
- **Results**:
  - Effective on **4 real-world datasets**.
  - Learns propagation beyond the **2-3 hop neighborhood limit** of vanilla GCN.

---

## Klicpera et al. (2019) - Predict then Propagate (PPNP / APPNP)

- **Source**: ICLR 2019 ([paper](https://arxiv.org/abs/1810.05997)) | [Code](https://github.com/gasteigerjo/ppnp)
- **What it does**: Decouples prediction (neural network) from propagation (Personalized PageRank). Key insight: use the GCN–PageRank connection to derive a better propagation scheme.
- **Results**:
  - **Outperforms GCN-based models** on semi-supervised classification across multiple datasets.
  - Training time: **equal or faster**. Parameters: **equal or fewer**.
  - APPNP achieves **linear computational complexity** via power iteration.

---

## GraphSAP - Data-Driven Propagation Mechanism (2023)

- **Source**: Electronics, MDPI ([paper](https://www.mdpi.com/2079-9292/12/1/46))
- **What it does**: Learns the propagation mechanism itself from data. Adaptively fuses low-order local structure and high-order neighborhood information across layers.

---

## Maximizing Influence with GNN (2024)

- **Source**: HAL ([paper](https://hal.science/hal-04368762/document))
- **What it does**: Applies GNN to the influence maximization problem for scalable seed selection under classical diffusion models.

---

## Comprehensive Review: Propagation Models from Deterministic to Deep Learning (2024)

- **Source**: arXiv ([paper](https://arxiv.org/html/2410.02118v1))
- **What it does**: Categorizes propagation modeling methods into model-based (SIR, SIS, threshold) and model-free (GNN-based). Establishes that GNNs have achieved **breakthrough results** in large-scale complex network propagation.
