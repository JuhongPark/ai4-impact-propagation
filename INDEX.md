# ai4-marketing Research Index

Quick navigation across every document in this project. For paper-level lookup, see `docs/CATALOG.md`.

---

## Document Map

### Root

| File | Purpose |
|------|---------|
| `README.md` | Project overview, key approaches table, search keywords |
| `INDEX.md` | This document — topic-based navigation |
| `docs/CATALOG.md` | All cited papers / tools, grouped by method or domain |

### Domain Surveys (`docs/`)

Short, breadth-first surveys of each marketing AI domain. Read these first for context.

| File | Topic | Primary AI Methods |
|------|-------|---------------------|
| `docs/01_customer_segmentation.md` | Customer segmentation and targeting | Deep clustering, RFM-Net, LRFMS, XAI |
| `docs/02_recommendation_systems.md` | GNN-based recommenders | PinSage, LightGCN, NGCF, KGAT, SR-GNN |
| `docs/03_influencer_marketing.md` | Influence prediction and viral spread | DeepInf, Deep RL for IM, Aral experiments |
| `docs/04_churn_prediction.md` | Customer churn prediction and retention | CCP-Net, Random Forest, hybrid DL, RFM |
| `docs/05_marketing_mix_modeling.md` | MMM and multi-touch attribution | PyMC-Marketing, Robyn, Meridian, DNAMTA, CAMTA |

### Deep Dives (`docs/deep_dive/`)

Long-form treatments: architectures, quantitative results, open problems. Read these after the domain surveys.

| File | Topic | Core References |
|------|-------|------------------|
| `docs/deep_dive/DD1_gnn_recommender_systems.md` | GNN for recommendation | GraphSAGE (2017), PinSage (2018), NGCF (2019), LightGCN (2020), KGAT (2019), SR-GNN (2019) |
| `docs/deep_dive/DD2_deep_rl_viral_marketing.md` | Deep RL for viral, paid, personalized marketing | DGN, BiGDN, HEDRL-IM, BIM-DRL; RLB-DP, SS-RTB; LinUCB, Thompson, BanditLP |
| `docs/deep_dive/DD3_influencer_marketing.md` | Social influence and influencer marketing | DeepInf, HetInf, DeepPP; Aral/MIT Sloan experiments; ML for Instagram |
| `docs/deep_dive/DD4_customer_churn_cascade.md` | Customer churn prediction, contagion, uplift | CCP-Net, classical ML; Ferreira-Telang churn contagion; CausalML uplift |
| `docs/deep_dive/DD5_marketing_mix_modeling.md` | Bayesian MMM and causal attribution | Jin 2017, PyMC-Marketing, Robyn, Meridian; DNAMTA, CAMTA, Amazon MTA |
| `docs/deep_dive/DD6_ai_marketing_foundations.md` | Theoretical foundations synthesis | Bayesian + causal + RL + representation learning; off-policy evaluation |
| `docs/deep_dive/DD7_mit_marketing_research.md` | MIT research landscape on AI marketing | Tucker, Eckles, Aral, Simester, Perakis, Bertsimas, Roy, Pentland, Barzilay, Jaakkola |
| `docs/deep_dive/DD8_mit_sdm_marketing.md` | MIT SDM program research on AI marketing | Dao (2025) multi-agent thesis, MoT theses, SDM system architecture methodology |

### Frontier Research (`docs/frontier/`)

Post-2023 topics not yet covered in the main deep dives. Read these for the current edge of the field.

| File | Topic | Core References |
|------|-------|------------------|
| `docs/frontier/generative_ai_and_llms_in_marketing.md` | LLMs and diffusion models for creative, personalization, conversational commerce | Stable Diffusion CTR pipeline, Retail-GPT, Amazon RAG, consumer sentiment research |
| `docs/frontier/llm_enhanced_recommenders.md` | LLM-based recommenders | P5 (2022), TALLRec (2023), LLaRA (2024), E4SRec, LLM-SRec, instance-wise LoRA |
| `docs/frontier/agentic_ai_marketing.md` | Autonomous agents, multi-agent coordination, RAG commerce | Deloitte/Gartner agentic stats, Dao (2025) topology analysis, RAG for commerce |

---

## Topic Index (Keyword-Based Discovery)

### By AI Method

| Method | Primary documents |
|--------|---------------------|
| **Graph Neural Networks (CF)** | DD1, docs/02, frontier/llm_enhanced_recommenders (hybrid) |
| **Deep Reinforcement Learning** | DD2, DD6 (theory) |
| **Contextual Bandits** | DD2, DD6 |
| **Bayesian Inference / Bayesian MMM** | DD5, DD6, docs/05 |
| **Causal Inference / Double ML** | DD4 (uplift), DD5 (attribution), DD6 (theory) |
| **Uplift Modeling** | DD4 §7, DD6 §4 |
| **Offline RL / Off-Policy Evaluation** | DD6 |
| **Large Language Models** | frontier/generative_ai_and_llms_in_marketing, frontier/llm_enhanced_recommenders, frontier/agentic_ai_marketing |
| **Diffusion Models** | frontier/generative_ai_and_llms_in_marketing |
| **Retrieval-Augmented Generation (RAG)** | frontier/generative_ai_and_llms_in_marketing §5, frontier/agentic_ai_marketing §2 |
| **Deep Learning (general)** | DD4 (churn), docs/01 (segmentation) |
| **Hybrid ML + classical models** | DD4, DD5, frontier/llm_enhanced_recommenders |

### By Marketing Domain

| Domain | Documents |
|--------|-----------|
| **Recommendation** | DD1, docs/02, frontier/llm_enhanced_recommenders |
| **Customer Segmentation** | docs/01 |
| **Influencer Marketing / Viral** | DD2, DD3, docs/03 |
| **Customer Churn / Retention** | DD4, docs/04 |
| **Marketing Mix Modeling** | DD5, docs/05 |
| **Multi-Touch Attribution** | DD5, docs/05 |
| **Real-Time Bidding (Programmatic)** | DD2 §3 |
| **Personalized Offers / Treatments** | DD2 §4 (bandits), DD4 §7 (uplift) |
| **Creative / Copy Generation** | frontier/generative_ai_and_llms_in_marketing |
| **Conversational Commerce** | frontier/generative_ai_and_llms_in_marketing §5, frontier/agentic_ai_marketing |
| **Agentic Marketing Workflows** | frontier/agentic_ai_marketing |

### By Research Institution

| Institution | Primary document |
|-------------|---------------------|
| **MIT Sloan (Marketing Group)** | DD7 §2 |
| **MIT ORC (Operations Research Center)** | DD7 §3 |
| **MIT IDE** | DD7 §4 |
| **MIT IDSS** | DD7 §5 |
| **MIT Media Lab** | DD7 §6 |
| **MIT CSAIL** | DD7 §7 |
| **MIT SDM Program** | DD8 |
| **Google Research (MMM)** | DD5 §2, §3.3 (Meridian) |
| **Meta (Robyn MMM)** | DD5 §3.2 |
| **Amazon Science (RAG, MTA)** | DD5 §4.3, frontier/generative_ai_and_llms_in_marketing §5 |
| **Stanford (GNN)** | DD1 (Leskovec group) |
| **Pinterest (PinSage)** | DD1 §3 |

### By Challenge / Problem Type

| Problem | Where to look |
|---------|---------------|
| **Cold start** | DD1 §2 (GraphSAGE), frontier/llm_enhanced_recommenders |
| **Long customer journey / lifetime** | DD4 (retention), DD5 (attribution), frontier/agentic_ai_marketing |
| **Privacy / post-cookie** | DD5 (Meridian, MMM), DD7 (Tucker), frontier/generative_ai_and_llms_in_marketing |
| **Fairness / balanced spread** | DD2 §2.5 (BIM-DRL) |
| **Scalability to web scale** | DD1 §3 (PinSage), frontier/llm_enhanced_recommenders §7 |
| **Interpretability / XAI for marketing** | DD6 gap 2, docs/01 |
| **Causal identification** | DD4 §7, DD5 §4, DD6 |
| **Off-policy evaluation** | DD6 §4 |
| **Brand safety under AI generation** | frontier/generative_ai_and_llms_in_marketing §4, frontier/agentic_ai_marketing §4 |

---

## How to Find What You Need

**Looking for a specific paper by title or author?**
→ `docs/CATALOG.md` — search by title or author; each entry lists the documents where it is discussed.

**Looking for a method (e.g., "contextual bandits", "Bayesian MMM")?**
→ Use the "By AI Method" table above.

**Looking for research in a specific marketing domain (e.g., churn, attribution)?**
→ Use the "By Marketing Domain" table above.

**Looking for MIT-specific research?**
→ DD7 (faculty landscape) and DD8 (SDM theses and adjacent programs).

**Looking for the current state of the art (2024-2026)?**
→ `docs/frontier/` — three documents cover generative AI, LLM recommenders, and agentic marketing.

**Looking for theoretical foundations?**
→ DD6 — synthesizes Bayesian, causal, RL, and representation-learning frameworks.

**Looking for a strong baseline to beat?**
→ DD1 for recommendation (LightGCN), DD4 for churn (Random Forest), DD5 for MMM (Bayesian adstock+saturation).

---

## Reading Paths

### Path A: "I'm new to AI marketing and want the full landscape"

1. `README.md`
2. Each `docs/01_*` through `docs/05_*` for breadth
3. `docs/deep_dive/DD6_ai_marketing_foundations.md` for the theoretical synthesis
4. `docs/frontier/*` for 2024-2026 developments
5. `docs/CATALOG.md` to build a targeted reading list

### Path B: "I need to decide whether to use method X for problem Y"

1. Use "By AI Method" or "By Marketing Domain" table to find the right DD
2. Read the relevant DD's cross-method comparison section
3. Check "Open Problems" section of that DD for known limitations
4. Look up candidate papers in `docs/CATALOG.md` for details

### Path C: "I'm a PhD student / researcher surveying the area"

1. `docs/CATALOG.md` — scan all paper entries
2. DD6 for the unifying theoretical view
3. Each DD1-DD5 for methodology depth
4. DD7 and DD8 for MIT-specific research groups
5. `docs/frontier/*` for current research gaps
6. Cross-reference with curated GitHub lists linked in DD1, DD2, DD4, DD5, frontier

### Path D: "I'm a practitioner building an AI marketing stack"

1. `README.md` key approaches table — pick the relevant cell
2. Read the referenced paper directly via `docs/CATALOG.md`
3. Read the relevant DD section for production considerations
4. Check `docs/frontier/agentic_ai_marketing.md` §4 for deployment pitfalls
5. Use open-source tools linked in DD5 (PyMC-Marketing, Robyn, Meridian), DD4 (CausalML), frontier/llm_enhanced_recommenders (LLM4Rec curated lists)

---

## Maintenance Notes

This index should be updated whenever a new document is added to `docs/`. Each new document should:

1. Be listed in the Document Map section above.
2. Have its key methods added to the "By AI Method" table.
3. Have its domain added to the "By Marketing Domain" table if new.
4. Have its cited papers added to `docs/CATALOG.md` with a "Discussed in" back-reference.

Keeping both `INDEX.md` (topic navigation) and `docs/CATALOG.md` (paper-level lookup) in sync is the core discipline for keeping the project searchable as it grows.
