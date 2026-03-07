# Deep Dive 6: Theoretical Foundations of AI Marketing

Cross-disciplinary synthesis of the theoretical frameworks underlying AI marketing — and what they tell us about where AI should focus next.

---

## 1. The Unifying Observation

Despite surface differences across recommendation, segmentation, churn, influencer marketing, attribution, and MMM, **the same small set of theoretical frameworks** underlies all of them:

| Marketing decision | Theoretical framework |
|--------------------|------------------------|
| "What should I recommend?" | **Representation learning** on user–item graph + **ranking** under exploration–exploitation |
| "Which customer segment?" | **Unsupervised / supervised representation** + **classification** |
| "Who will churn?" | **Supervised prediction** over sequences |
| "Who to treat to prevent churn?" | **Causal inference** (uplift, double ML) |
| "Who are the influencers?" | **Graph representation learning** + **causal identification** |
| "Which touchpoint drove conversion?" | **Counterfactual reasoning** over sequences |
| "How to allocate spend across channels?" | **Bayesian inference** + **causal identification** on aggregate data |
| "Which bid to place?" | **Sequential decision making** (RL) under budget |
| "Which offer to show?" | **Contextual bandits** (one-step RL) |

**Common pattern**: every marketing problem reduces to **a decision made under uncertainty using historical data**, which is the core of **decision theory + causal inference + machine learning**.

---

## 2. Four Foundational Frameworks and Their Cross-Domain Mapping

### 2.1 Bayesian Inference

**Core mechanism**: Prior belief × likelihood → posterior belief. Every decision uses the full posterior distribution, not just point estimates.

**Cross-mapping**:

| Marketing area | How Bayesian inference applies | Deep dive |
|----------------|---------------------------------|-----------|
| MMM | Priors encode domain knowledge (adstock half-life, ROI range); posterior quantifies uncertainty in spend allocation | DD5 (PyMC-Marketing, Robyn, Meridian) |
| Customer segmentation | Bayesian mixture models for soft cluster assignment | DD DD4 §4 (hybrid RFM + DNN) |
| Churn | Bayesian priors on churn hazard; posterior credible intervals for retention-team decisions | DD4 |
| Bandits | Thompson sampling = Bayesian decision-making under uncertainty | DD2 §4 |

**Key insight for AI**: Marketing decisions have **high stakes + small data** (one observation per week for MMM, a few thousand retention experiments). Bayesian methods dominate when data is scarce relative to the question. Non-Bayesian deep learning dominates when data is abundant.

### 2.2 Causal Inference

**Core mechanism**: Identify interventions whose effect can be estimated from observational / experimental data without confounding. The workhorses are randomized experiments, regression discontinuity, instrumental variables, difference-in-differences, and — increasingly — ML-based methods (double ML, causal forests, meta-learners).

**Cross-mapping**:

| Marketing area | Causal question | Method | Deep dive |
|----------------|-----------------|--------|-----------|
| Retention | "Which customer will *respond* to the offer?" | Uplift modeling (T-learner, X-learner, uplift trees) | DD4 §7 |
| Attribution | "Which touchpoint *caused* conversion?" | Counterfactual sequence models (CAMTA) | DD5 §4 |
| MMM | "What *caused* the revenue change — spend or market drift?" | Bayesian causal MMM with incrementality calibration | DD5 §3 |
| Social influence | "Did my neighbor *cause* me to adopt, or are we just similar?" | Aral's randomized contagion experiments | DD3 §6 |
| Personalization | "Which treatment is *best* for this user type?" | Contextual bandit with off-policy evaluation | DD2 §4 |

**Foundational paper**: Chernozhukov et al. (2018), "Double/Debiased Machine Learning for Treatment and Structural Parameters" ([paper](https://arxiv.org/abs/1608.00060)). Shows how to combine flexible ML with classical causal identification to obtain valid inference for treatment effects — the theoretical bridge between modern ML and causal marketing analytics.

**Practical library**: [DoubleML](https://docs.doubleml.org/) — Python and R implementation of Chernozhukov's framework.

### 2.3 Reinforcement Learning (Online + Offline)

**Core mechanism**: A policy interacts with (or is trained on logged data from) an environment, receives rewards, and updates to maximize long-term cumulative reward.

**Cross-mapping**:

| Marketing area | RL framing | Deep dive |
|----------------|------------|-----------|
| Influence maximization | Sequential seed selection as MDP; DQN over graph embeddings | DD2 §2 |
| Real-time bidding | Budget-constrained MDP over auction stream | DD2 §3 |
| Personalized offers | Contextual bandit (one-step RL) | DD2 §4 |
| Long-term retention | Sequential retention actions over customer lifecycle | DD4 open problem |
| Dynamic pricing | MDP over demand response | Not covered in detail; adjacent area |

**Foundational paper**: Levine, Kumar, Tucker & Fu (2020). "Offline Reinforcement Learning: Tutorial, Review, and Perspectives on Open Problems." [Paper](https://arxiv.org/abs/2005.01643). The definitive treatment of **learning RL policies from logged data without further exploration** — the regime all production marketing RL actually operates in.

**Why offline RL matters for marketing**: Online RL exploration in marketing means sending genuinely bad treatments to real customers to learn. That's rarely acceptable. Offline RL lets you learn from logged experience — decade-old email campaigns, historical bid logs, ancient A/B tests — without new risky exploration.

### 2.4 Representation Learning

**Core mechanism**: Map raw high-dimensional input (user behavior, item metadata, text, images, graphs) into dense vectors that make downstream prediction / decision tractable.

**Cross-mapping**:

| Marketing area | What is embedded? | Method | Deep dive |
|----------------|-------------------|--------|-----------|
| Recommendation | Users, items | GNN (PinSage, LightGCN) | DD1 |
| Segmentation | Customers | Deep embedding + clustering (DEC, RFM-Net) | DD4 §1, DD segmentation survey |
| Churn | Customer sequences | BiLSTM, Transformer embeddings (CCP-Net) | DD4 §2 |
| Influence | Ego-networks | GNN (DeepInf, HetInf) | DD3 §2–4 |
| Content | Post images, captions, video | CLIP, vision-language models | DD3 §5 (emerging) |

**Key insight for AI**: Representation learning is the "universal substrate" that enables every other framework. Bayesian inference on raw pixel data is hopeless; on a 256-dim embedding it is tractable. RL in action-space-of-text is hopeless; in an embedding space it is tractable.

---

## 3. Simple vs. Complex Marketing Decisions

A fundamental distinction that cuts across all domains:

| Property | Simple Decision | Complex Decision |
|----------|-----------------|-------------------|
| Horizon | 1 step | Many steps |
| Example | "Show this email subject line?" | "Offer discount → upsell → cross-sell over 6 months" |
| Right framework | **Contextual bandit** | **Full RL / causal dynamic treatment regime** |
| Data needed | Historical pairs (context, treatment, reward) | Logged sequences |
| Common failure | Treating context as static when it evolves | Treating long horizon as a single decision |
| Off-policy evaluation | Inverse propensity scoring (IPS), doubly robust | Doubly robust IS, fitted Q evaluation, model-based OPE |

### Implications for AI

- **Simple decisions** (email A/B, single offer, ranking) are already well-served by contextual bandits and uplift modeling.
- **Complex decisions** (lifecycle journeys, multi-campaign cadence) are the hard frontier. Offline RL + counterfactual reasoning is the theoretically correct approach but production-ready methods are sparse.

---

## 4. Off-Policy Evaluation — The Quiet Core of Every System

**Off-policy evaluation (OPE)**: estimate how a new candidate policy would perform using data collected under an old policy.

OPE is the **single most important operational question in AI marketing** and is hidden inside every deployment:

| Area | What OPE does |
|------|----------------|
| Recommendation | "Would swapping LightGCN for LightGCN+KG improve Recall@20?" |
| Uplift / retention | "Would using this new uplift model improve retention under the same budget?" |
| Bandit | "Would this new policy beat the current one on historical logs?" |
| RL bidding | "Would this new bid policy increase ROAS without exceeding budget?" |
| MMM | "Would re-allocating 10% from TV to paid search change revenue?" |

**Foundational methods**:
- **Inverse Propensity Scoring (IPS)** — Horvitz–Thompson estimator for treatment effects
- **Doubly Robust (DR)** estimator — combines model + IPS, robust to specification error in either
- **Self-Normalized IPS (SNIPS)** — reduces variance
- **Fitted-Q Evaluation** — for long-horizon RL
- **Model-based OPE** — simulate the candidate policy in a learned model of the environment

### The Connection

OPE is where **causal inference + ML + RL converge**. Every well-run marketing ML system does OPE under the hood, even if it's called "offline A/B" or "counterfactual analysis."

---

## 5. Where Each Theoretical Insight Maps to AI Research

| Theoretical insight | AI research area | Relevant deep dive |
|---------------------|------------------|-------------------|
| High-order graph connectivity | GNN for recommendation | DD1 (NGCF, LightGCN, PinSage) |
| Ego-network sufficiency | Local GNN for influence | DD3 (DeepInf) |
| Submodular influence maximization | Deep RL + GNN for seed selection | DD2 (DGN, BiGDN, HEDRL-IM) |
| Contextual bandits | Personalized offer, news, email | DD2 §4 (LinUCB, Thompson, BanditLP) |
| Adstock / saturation (Jin 2017) | Bayesian MMM | DD5 (PyMC-Marketing, Robyn, Meridian) |
| Counterfactual reasoning | Causal MTA, uplift | DD4 §7, DD5 §4 (CAMTA) |
| Temporal dependencies | Sequence models (BiLSTM, Transformer) | DD4 §2 (CCP-Net) |
| Multi-modal content | Vision-language models + GNN | DD3 §5 (emerging) |
| Social contagion causality | Randomized experiments + diffusion models | DD3 §6 (Aral), DD4 §6 (Ferreira-Telang) |
| Off-policy evaluation | Doubly robust, fitted-Q evaluation | Cross-cutting, open problem |

---

## 6. The Gaps: What Theory Demands but AI Hasn't Delivered

### Gap 1: Causal ML in Recommendation

**Theory says**: The relevance of a recommended item should be the **causal effect** of showing it on user behavior — not the correlation between showing it and user behavior.

**AI does**: NGCF / LightGCN / PinSage learn correlational ranking objectives. The top-ranked item may be the one the user would have found anyway.

**What's missing**: Production causal ranking objectives. Some research exists (e.g., causal embeddings) but is not widely deployed.

### Gap 2: Fair ML Under Causal Constraints

**Theory says**: Treatment assignment should be **counterfactually fair** — two otherwise-identical customers with different protected attributes should receive the same treatment in expectation.

**AI does**: Fair-ML classification metrics (equal opportunity, demographic parity) are applied, but rarely at the causal level.

**What's missing**: Counterfactually fair uplift and bandit algorithms for marketing treatment assignment.

### Gap 3: Non-Stationarity

**Theory says**: Consumer tastes, competitors, and platform algorithms drift continuously. Stationary-environment assumptions break.

**AI does**: Mostly trains on the last N weeks and periodically retrains.

**What's missing**: Principled change-point detection + continual learning for MMM, bandits, and churn. Meta-RL for adaptation rate is nascent.

### Gap 4: Long-Horizon Credit Assignment

**Theory says**: Brand building, customer education, and lifecycle engagement play out over months or years. Single-step optimization cannot capture this.

**AI does**: Most production systems treat each action independently.

**What's missing**: Production-ready offline RL with safety constraints for long-horizon marketing. Current work is mostly research-grade.

### Gap 5: Joint Content Generation + Targeting

**Theory says**: LLMs and diffusion models can generate creatives, subject lines, ad copy. Bandits and causal ML decide when to deploy them. These are usually two separate systems.

**AI does**: Integration is ad-hoc.

**What's missing**: Joint optimization of content generation and targeting policy — a rapidly emerging frontier as generative AI meets bandits.

### Gap 6: Privacy-Preserving Causal ML

**Theory says**: Causal inference requires treatment, context, and outcome. Privacy regulation restricts all three (especially for user-level MTA and cross-device personalization).

**AI does**: Aggregate MMM (Meridian) handles this, but user-level causal estimation under strong privacy is an open problem.

**What's missing**: Federated causal ML, differentially private causal inference, and aggregate-only attribution that retains user-level decision relevance.

---

## 7. Towards a Unified AI Marketing Framework

Based on the theoretical synthesis, a mature AI marketing system would combine:

```
[Input]
  Customer graph + content + campaign history + aggregate KPIs
    ↓
[Representation Layer]
  GNN over user-item graph + transformer over sequences + vision-language over content
    ↓
[Prediction Layer]
  Engagement, churn, conversion, revenue — per customer, per touchpoint
    ↓
[Causal Layer]
  Uplift estimation, counterfactual attribution, Bayesian MMM
  (double ML, causal forests, uplift trees, Bayesian hierarchical models)
    ↓
[Decision Layer]
  Contextual bandits (one-step) + offline RL (sequential)
  Under safety, fairness, budget, cadence constraints
    ↓
[Off-Policy Evaluation Layer]
  Doubly robust IPS, fitted-Q, model-based OPE
  Plus periodic incrementality tests for ground-truth calibration
    ↓
[Output]
  Per-customer treatment + per-channel allocation + uncertainty quantification
```

Every DD in this project is a **component** of this stack. The stack does not yet exist as a unified system in any production deployment — it is the research frontier.

---

## 8. Summary: Cross-Framework Mapping

```
                    Bayesian Inference           Causal Inference
                    (uncertainty + priors)       (intervention + counterfactuals)
                              |                            |
                    ┌─────────┴──────────┐      ┌─────────┴──────────┐
                    |                    |      |                    |
               MMM (DD5)           Uplift (DD4) MTA (DD5)        Influence Experiments (DD3)
                    |                    |      |                    |
                    └──────────┬─────────┴──────┘
                               |
                    Off-Policy Evaluation
                    (doubly robust, fitted-Q, model-based)
                               |
                               |
                    Contextual Bandits    Deep RL        Representation Learning
                    (DD2 §4)              (DD2 §2–3)     (DD1, DD3, DD4)
                               |
                               ↓
                    Unified AI Marketing Framework
                    (future work)
```

The arrows are not one-way: Bayesian inference feeds priors into RL; representation learning provides the substrate for causal inference; OPE validates every component.

---

## 9. References

### Foundational Texts and Papers
- Chernozhukov et al. (2018). Double/Debiased Machine Learning for Treatment and Structural Parameters. Econometrics Journal. [Paper](https://arxiv.org/abs/1608.00060) | [DoubleML Library](https://docs.doubleml.org/)
- Levine, Kumar, Tucker, Fu (2020). Offline Reinforcement Learning: Tutorial, Review, and Perspectives. [Paper](https://arxiv.org/abs/2005.01643) | [NeurIPS Tutorial](https://sites.google.com/view/offlinerltutorial-neurips2020/home)
- Kempe, Kleinberg, Tardos (2003). Maximizing the Spread of Influence through a Social Network. KDD. [Paper](https://www.cs.cornell.edu/home/kleinber/kdd03-inf.pdf)
- Li, Chu, Langford, Schapire (2010). A Contextual-Bandit Approach to Personalized News Article Recommendation. WWW.
- Jin et al. (2017). Bayesian Methods for Media Mix Modeling with Carryover and Shape Effects. Google Research. [Paper](https://research.google/pubs/bayesian-methods-for-media-mix-modeling-with-carryover-and-shape-effects/)
- Gutierrez & Gerardy (2017). Causal Inference and Uplift Modeling: Literature Review. PMLR. [Paper](https://proceedings.mlr.press/v67/gutierrez17a/gutierrez17a.pdf)

### Survey Papers
- Wu et al. (2022). Graph Neural Networks in Recommender Systems: A Survey. ACM Computing Surveys. [Paper](https://dl.acm.org/doi/10.1145/3535101)

### Causal Marketing Practice
- [CausalML (Uber)](https://github.com/uber/causalml) — uplift and meta-learners
- [DoubleML](https://docs.doubleml.org/) — double machine learning in Python and R
- [awesome-marketing-machine-learning](https://github.com/station-10/awesome-marketing-machine-learning)

### Cross-References to Other Deep Dives
- DD1: GNN for recommender systems (representation learning layer)
- DD2: Deep RL for viral / paid marketing (decision layer)
- DD3: Influencer marketing (representation + causal identification)
- DD4: Churn prediction & churn cascade (prediction + causal treatment)
- DD5: MMM and attribution (Bayesian + causal aggregate)
