# Deep Dive 8: MIT SDM Research Related to Impact Propagation

A survey of research from MIT's System Design and Management (SDM) program relevant to impact propagation, cascading failures, network resilience, and related topics.

---

## 1. About MIT SDM

The **System Design and Management (SDM)** program is a joint offering of the MIT School of Engineering and MIT Sloan School of Management, leading to a Master of Science in Engineering and Management. SDM is not a traditional research lab but an interdisciplinary professional master's program focused on:

- **Systems thinking** and system architecture
- **Complex system design** and management
- **Agent-based modeling** of socio-technical systems

SDM does not operate as a single research group with a dedicated impact propagation focus. Instead, its contributions come through student theses supervised by faculty across MIT, and through its core teaching of system architecture and systems thinking methodologies.

### Key SDM Faculty

| Faculty | Role | Relevant Expertise |
|---------|------|-------------------|
| **Bryan Moser** | Academic Director, Senior Lecturer | Agent-based modeling of socio-technical systems, teamwork dynamics, complex systems |
| **Bruce Cameron** | Director, System Architecture Group | System architecture, platform strategy, technology strategy |
| **Ed Crawley** | Ford Professor of Engineering | Architecture, design, and optimization of complex technical systems |

---

## 2. Directly Related SDM Research

### 2.1 Dao (2025) — Cascading Failures in Multi-Agent Systems

**This is the most directly relevant SDM thesis to this project.**

| Field | Detail |
|-------|--------|
| **Title** | Designing Generative Multi-Agent Systems for Collective Intelligence and Resilience |
| **Author** | Nguyen Luc Dao |
| **Degree** | SM, System Design and Management Program |
| **Date** | May 2025 |
| **Advisor** | Bryan R. Moser |
| **Links** | [DSpace](https://dspace.mit.edu/handle/1721.1/162506) · [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1877050925025311) |
| **Award** | Best Student Paper, CAS 2025 ([SDM announcement](https://sdm.mit.edu/research-practice/dao-best-paper-cas-2025/)) |

#### Problem

Multi-agent LLM systems can exhibit **cascading failures** when malicious or faulty agents inject incorrect information that propagates through the collaboration topology, deteriorating collective decisions and causing systemic failure.

#### Key Findings

| Variable | Effect on Resilience |
|----------|---------------------|
| **Group size** | Increasing group size improves accuracy and resilience, at the cost of more tokens |
| **Step-back abstraction prompting** | Enhances accuracy and mitigates hallucinations induced by malicious agents |
| **Group Chat topology** | Highly vulnerable to malicious interference |
| **Reflexion topology** | Offers safeguards against adversarial risks |
| **Crowdsourcing topology** | Offers safeguards against adversarial risks |
| **Blackboard topology** | Offers safeguards against adversarial risks |

#### Architecture

```
[Multi-Agent LLM System]
  - N agents with individual reasoning capabilities
  - Collaboration topology defines information flow
  - Malicious agents inject adversarial content
  |
  v
[Propagation Mechanism]
  - Incorrect information spreads through topology
  - Downstream agents incorporate corrupted inputs
  - Collective decision quality degrades
  |
  v
[Resilience Analysis]
  - Measure accuracy under varying adversarial fractions
  - Compare topologies: Group Chat vs. Reflexion vs. Crowdsourcing vs. Blackboard
  - Trade-off: performance vs. cost vs. resilience vs. accountability
```

#### Connection to This Project

This thesis maps directly onto the project's core framework:

| Project Concept | Dao (2025) Equivalent |
|----------------|----------------------|
| Network topology determines cascade behavior (DD6) | Collaboration topology determines vulnerability to adversarial cascading |
| Threshold models — node activates when neighbors exceed threshold (DD6 §2.1) | Agent incorporates incorrect information when malicious neighbor input exceeds trust threshold |
| Phase transitions in cascade behavior (DD6 §2.1) | Transition from resilient to fragile depending on group size and topology |
| GNN message passing (DD1) | Message passing between LLM agents in collaboration topology |
| Influence maximization (DD2) | Malicious agent placement ≈ inverse influence maximization |

---

### 2.2 Chen (2021) — Cybersecurity Risk Management

| Field | Detail |
|-------|--------|
| **Title** | A Systematic Approach for Cybersecurity Risk Management |
| **Author** | Kristin YiJie Chen |
| **Degree** | SM, System Design and Management Program |
| **Date** | September 2021 |
| **Advisor** | Michael D. Siegel |
| **Link** | [DSpace](https://dspace.mit.edu/handle/1721.1/139995) |

#### Key Content

Proposes the **Cyber Risk Cube (CRC)** tool examining three fundamental pairings: Internal/External, Measurement/Management, and Qualitative/Quantitative. The CRC provides a standardized organizational framework for cyber risk management.

#### Connection to This Project

- Cyber attacks can trigger **cascading failures** in infrastructure networks (DD4)
- Risk management frameworks help identify propagation pathways before incidents occur
- Indirect relevance: risk assessment methodology applicable to infrastructure vulnerability analysis

---

### 2.3 Anastos (2025) — Grid Enhancing Technologies

| Field | Detail |
|-------|--------|
| **Title** | Grid Enhancing Technologies: Optimization and Benefit for Distribution Grids |
| **Author** | Daniel Anastos |
| **Degree** | SM, System Design and Management Program |
| **Date** | May 2025 |
| **Advisors** | Pablo Duenas Martinez (MIT Energy Initiative), Sungho Shin (Chemical Engineering) |
| **Link** | [DSpace](https://dspace.mit.edu/bitstream/handle/1721.1/162526/anastos-daniel55-sm-sdm-2025-thesis.pdf) |

#### Connection to This Project

- Grid enhancing technologies directly address **distribution grid resilience** (DD4)
- Optimization of grid infrastructure relates to mitigating cascading failure propagation pathways
- Indirect relevance: infrastructure hardening as a cascade prevention strategy

---

### 2.4 Kalra (2023) — ML for Cyberattack Detection on Industrial Control Systems

| Field | Detail |
|-------|--------|
| **Title** | Machine Learning for Detection of Cyberattacks on Industrial Control Systems |
| **Author** | Geet Kalra |
| **Degree** | SM, System Design and Management Program |
| **Date** | 2023 |
| **Link** | [DSpace](https://dspace.mit.edu/bitstream/handle/1721.1/150269/kalra-geet-sm-sdm-2023-thesis.pdf) |

#### Connection to This Project

- Cyberattacks on ICS can trigger **cascading physical failures** in infrastructure
- ML-based detection is an early warning system for preventing cascade initiation
- Relevant to DD4 (cascading failure prediction) from the detection/prevention angle

---

## 3. Related Research from SDM-Adjacent Programs

SDM shares faculty, coursework, and research infrastructure with several MIT programs. The following theses are not from SDM itself but come from programs that closely interact with SDM:

### 3.1 Supply Chain Resilience (SCM / SCALE Network)

| Thesis | Author | Year | Program | Key Content |
|--------|--------|------|---------|-------------|
| **A Supply Network Resiliency Assessment Framework** | Siu & Stephen | 2015 | SCM (SCALE) | Balanced Scorecard of Resiliency (BSR) combining quantitative and qualitative assessment for supply chain nodes |
| **Robustness of Complex Supply Chain Networks to Targeted Attacks** | — | 2018 | ESD | Network science perspective on supply chain robustness; simulating targeted attacks on nodes and edges |
| **LNG Supply Chain Resilience** | Falaiye & Chiam | 2018 | SCM | Holistic network-level (vs. hub-level) approach to LNG supply chain disruption resilience |
| **Resilient by Design: A Supply Chain Digitalization Journey** | — | 2024 | SCM | Digital tools for stress testing and response evaluation across supply chain disruption scenarios |

### 3.2 Network Resilience and Cascading Failures (EECS / CEE)

| Thesis | Author | Year | Program | Advisor | Key Content |
|--------|--------|------|---------|---------|-------------|
| **Understanding Resilience in Large Networks** | Tuhin Sarkar | 2016 | EECS | Munther Dahleh | Quantitative resilience measure for large interconnected networks; applied to economic production networks, vehicular platoons, consensus systems |
| **On Control and Optimization of Cascading Phenomena in Dynamic Networks** | — | 2015 | EECS | — | Resilience enhancement through pre-disturbance reactance tweaking to prevent cascading failures |
| **Modeling and Mitigating Cascading Failures in Interdependent Power Grids and Communication Networks** | — | 2016 | EECS | — | Cross-infrastructure cascade modeling: power failures → communication failures → cascading power failures |
| **Strategic Inspection Operations for Critical Infrastructure Resilience** | Mathieu Dahan | 2019 | CEE | Saurabh Amin | Combinatorial inspection problems for adversarial failure detection, network security game theory |

---

## 4. SDM's Methodological Contributions

While SDM has limited direct research on impact propagation, its **methodological toolkit** is relevant:

### 4.1 System Architecture Analysis

SDM's core curriculum teaches system architecture methods (Crawley, Cameron, Selva) that can be applied to cascade analysis:

- **Decomposition**: Breaking complex systems into interacting components — directly maps to network node/edge decomposition
- **Interface analysis**: Understanding how components interact — maps to understanding propagation pathways
- **Architecture evaluation**: Assessing robustness of candidate architectures — Potts et al. (2020) applied this to cascading failure analysis

**Reference**: Potts, Sartor, Johnson, Bullock. [A Network Perspective on Assessing System Architectures: Robustness to Cascading Failure](https://incose.onlinelibrary.wiley.com/doi/10.1002/sys.21551). *Systems Engineering*, 2020.
- Applied graph-theoretic methods to two real-world system architectures (military communications, search and rescue)
- Found architectures robust to random vertex removal but vulnerable to targeted removal
- Evaluated cascading failure susceptibility using threshold models and hardening strategies

### 4.2 Agent-Based Modeling of Socio-Technical Systems

Bryan Moser teaches agent-based modeling in SDM, which directly connects to:

- **Supply chain ABM** (DD5): Firms as agents, disruptions propagate through agent interactions
- **Social influence models** (DD3): Agents adopt behaviors based on neighbor states
- **Multi-agent cascade dynamics**: Dao (2025) is a direct application of this approach

**Reference**: Moser. [Agent-Based Modelling of Socio-Technical Systems](https://link.springer.com/book/10.1007/978-94-007-4933-7).

### 4.3 Systems Thinking for Risk Propagation

SDM's systems thinking curriculum provides frameworks for understanding how risks propagate through complex systems:

- Feedback loops and unintended consequences
- System dynamics modeling of disruption propagation
- Holistic assessment vs. component-level analysis

---

## 5. Summary Assessment

### What SDM Covers

| Strength | Description | Relevance |
|----------|-------------|-----------|
| **Multi-agent cascade dynamics** | Dao (2025) directly studies cascading failures in agent collaboration topologies | High — DD1, DD6 |
| **System architecture for robustness** | Crawley-Cameron framework for analyzing system decomposition and interface vulnerability | Medium — DD4, DD6 |
| **Agent-based modeling** | Moser's ABM methodology applicable to propagation simulation | Medium — DD5 |
| **Cybersecurity risk propagation** | Chen (2021), Kalra (2023) on risk management and detection for infrastructure | Low-Medium — DD4 |
| **Grid infrastructure** | Anastos (2025) on distribution grid optimization | Low-Medium — DD4 |

### What SDM Does Not Cover

SDM does not have significant research in:

- **Graph Neural Networks** for propagation modeling → covered by CSAIL (Xu-Jegelka, Jaakkola)
- **Deep RL for influence maximization** → covered by external groups
- **Network economics and macro-level shock propagation** → covered by Economics (Acemoglu-Ozdaglar)
- **Large-scale social contagion experiments** → covered by Sloan/IDE (Aral) and Media Lab (Roy, Pentland)
- **Power grid physics-based cascade modeling** → covered by LIDS (Dahleh) and EESG (Ilic)

### SDM's Unique Niche

SDM's contribution to impact propagation is at the **system architecture and design level** — not in developing new AI methods or physical models, but in providing frameworks for:

1. **Architecting resilient systems** that are robust to cascading failures by design
2. **Modeling socio-technical interactions** where human and technical agent behaviors co-create cascade dynamics
3. **Bridging engineering and management** perspectives on risk propagation

Dao (2025) exemplifies this niche: it does not develop a new GNN architecture but applies systems thinking to understand how **collaboration topology** determines cascade resilience — a perspective that complements the more technical approaches surveyed in DD1–DD6.

---

## 6. References

### SDM Theses
- Dao, N.L. [Designing Generative Multi-Agent Systems for Collective Intelligence and Resilience](https://dspace.mit.edu/handle/1721.1/162506). SM Thesis, MIT SDM, 2025.
- Chen, K.Y. [A Systematic Approach for Cybersecurity Risk Management](https://dspace.mit.edu/handle/1721.1/139995). SM Thesis, MIT SDM, 2021.
- Anastos, D. Grid Enhancing Technologies: Optimization and Benefit for Distribution Grids. SM Thesis, MIT SDM, 2025.
- Kalra, G. Machine Learning for Detection of Cyberattacks on Industrial Control Systems. SM Thesis, MIT SDM, 2023.

### SDM-Adjacent Theses
- Sarkar, T. [Understanding Resilience in Large Networks](https://dspace.mit.edu/handle/1721.1/107374). SM Thesis, MIT EECS, 2016. Advisor: Munther Dahleh.
- Dahan, M. [Strategic and Analytics-Driven Inspection Operations for Critical Infrastructure Resilience](https://dspace.mit.edu/handle/1721.1/123226). PhD Thesis, MIT CEE, 2019. Advisor: Saurabh Amin.
- Siu, J.; Stephen, S. [A Supply Network Resiliency Assessment Framework](https://dspace.mit.edu/handle/1721.1/100086). Capstone, MIT SCM, 2015.

### Related Publications
- Potts, Sartor, Johnson, Bullock. [A Network Perspective on Assessing System Architectures: Robustness to Cascading Failure](https://incose.onlinelibrary.wiley.com/doi/10.1002/sys.21551). Systems Engineering, 2020.
- Dao, N.L. [Designing Generative Multi-Agent Systems for Resilience](https://www.sciencedirect.com/science/article/pii/S1877050925025311). ScienceDirect, 2025.
- Crawley, Cameron, Selva. Systems Architecture: Strategy and Product Development for Complex Systems. Pearson, 2015.
- Moser et al. [Agent-Based Modelling of Socio-Technical Systems](https://link.springer.com/book/10.1007/978-94-007-4933-7). Springer, 2012.

### SDM Program
- [MIT SDM Research & Practice Archive](https://sdm.mit.edu/research-practice/)
- [MIT SDM Thesis Archives (DSpace)](https://sdm.mit.edu/practice-category/research-output/student-thesis-dspace/)
- [MIT System Architecture Group](http://systemarchitect.mit.edu/people.php)
