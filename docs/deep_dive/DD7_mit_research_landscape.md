# Deep Dive 7: MIT Research Landscape — Impact Propagation

A comprehensive survey of impact propagation research conducted at MIT, organized by lab, lead researcher, and key publications.

---

## 1. Overview

MIT has been at the forefront of impact propagation research across nearly every domain — network economics, power grid cascading failures, supply chain shock propagation, social network information diffusion, and GNN theory. MIT's contributions are particularly notable in **theoretical foundations** (Acemoglu-Ozdaglar's network economics) and **methodological innovations** (GIN, Social Physics, differentiable simulation).

### MIT Contribution Map by Research Area

| Research Area | MIT Lab | Lead Researchers | Related Project Doc |
|---------------|---------|------------------|---------------------|
| Network economics & cascade theory | Economics, LIDS, IDSS | Acemoglu, Ozdaglar, Tahbaz-Salehi | DD6 (Theoretical foundations) |
| Power grid cascading failures | LIDS, Lincoln Lab, EESG | Dahleh, Ilic | DD4 (Power grids) |
| Supply chain resilience | CTL, ORC | Sheffi, Winkenbach | DD5 (Supply chains) |
| Social network propagation | Media Lab, Sloan, IDE | Roy, Aral, Pentland | DD3 (Social influence) |
| GNN theory & expressiveness | CSAIL | Jegelka, Xu, Jaakkola | DD1 (GNN mechanisms) |
| Network inference | LIDS, ORC, SDSC | Shah, Jadbabaie | DD6 (Theoretical synthesis) |
| Systemic risk & stability | IDSS, LIDS | Dahleh, Ozdaglar | DD6 |

---

## 2. Network Economics and Cascade Theory

### 2.1 Acemoglu-Ozdaglar-Tahbaz-Salehi Research Program

**Lab**: MIT Economics, LIDS, IDSS
**Lead Researchers**:
- **Daron Acemoglu** — MIT Economics, Institute Professor (2024 Nobel Prize in Economics)
- **Asuman Ozdaglar** — MIT EECS, MathWorks Professor, LIDS member, former EECS Department Head
- **Alireza Tahbaz-Salehi** — Kellogg School (MIT collaborator)

This research program constitutes one of **the core theoretical foundations of this project**, mathematically characterizing how microeconomic shocks propagate through network structures to produce macroeconomic effects.

#### Key Paper Series

| Paper | Venue | Key Contribution |
|-------|-------|-----------------|
| **The Network Origins of Aggregate Fluctuations** | Econometrica, 2012 | Proves that asymmetry in input-output networks amplifies micro shocks into macro fluctuations |
| **Cascades in Networks and Aggregate Volatility** | NBER WP 16516, 2010 | Mathematical relationship between network cascades and aggregate volatility |
| **Microeconomic Origins of Macroeconomic Tail Risks** | AER, 2017 | Network structure creates extreme macro risks (tail risks) |
| **The Network Origins of Large Economic Downturns** | MIT Working Paper | Network origins of large-scale economic downturns |
| **Systemic Risk and Stability in Financial Networks** | AER, 2015 | How a single bank default cascades into systemic chain defaults through financial networks |
| **Network Security and Contagion** | JET, 2016 | Network connectivity induces underinvestment in security and cascading failures (Acemoglu, Malekian, Ozdaglar) |

#### Theoretical Core

```
[Microeconomic shock (individual firm/sector)]
    | input-output linkage
    v
[First-order propagation: direct downstream customers affected]
    | higher-order interconnections
    v
[Cascade effect: indirect propagation to entire economy]
    | network asymmetry (hub structure)
    v
[Macroeconomic fluctuation: large aggregate-level variation]
```

**Key findings**:
- Sizable aggregate volatility arises from sectoral shocks **only if** there is significant **asymmetry** in supplier roles
- "Sparseness" of the input-output matrix is unrelated to the nature of aggregate fluctuations
- **Phase transitions** exist: the character of fluctuations changes qualitatively depending on network structure

#### Connection to This Project

- DD5 (Supply Chain AI): Acemoglu's model provides the theoretical foundation for AI-based supply chain shock propagation
- DD6 (Theoretical Synthesis): Included as one of the four foundational models

---

### 2.2 Ozdaglar — Mathematical Models of Cascades

**Additional research**:

| Paper | Co-authors | Key Content |
|-------|-----------|-------------|
| **A Simple Model of Cascades in Networks** | Yongwhan Lim, Ozdaglar | Simplified mathematical model of network cascades with analytical solutions |

Ozdaglar works at the intersection of optimization, game theory, and network economics, continuously extending the theoretical foundations of cascade propagation.

---

## 3. Cascading Failures in Power Grids

### 3.1 MIT LIDS — Cascade Prediction and Quantification

**Lab**: Laboratory for Information and Decision Systems (LIDS)
**Lead Researcher**:
- **Munther Dahleh** — MIT EECS, William A. Coolidge Professor, founding director of IDSS (2015–2023), LIDS member

#### Dahleh Research Group — Cascading Failures in Network Flows

| Research Topic | Key Content |
|---------------|-------------|
| **Robust Network Routing under Cascading Failures** | Dynamical model for cascading failures in single-commodity network flows |
| **Transportation congestion models** | Dynamic congestion models under disruptions; fragility dependence on network topology |
| **Systemic risk detection and mitigation** | Fundamental limits of systemic risk in interconnected network systems |
| **Decision-making under uncertainty** | Fundamental limits of real-time decision-making in finance, transportation, power grids, and digital platforms |

**LIDS Seminar Series** (directly relevant to this project):
- *"Quantifying Cascading Failure Propagation in Blackouts of Electrical Transmission Networks"* — Quantifying cascade propagation in power transmission blackouts, extending risk analysis
- *"Predicting Failure Cascades in Large Scale Power Systems via the Influence Model Framework"* — Predicting and screening failure cascades in large-scale DC/AC power systems using the influence model framework

### 3.2 MIT EESG & Lincoln Lab — Power System Resilience

**Lab**: Electric Energy Systems Group (EESG), MIT Lincoln Laboratory
**Lead Researcher**:
- **Marija Ilic** — LIDS Senior Research Scientist, IDSS Affiliate, Lincoln Lab Energy Systems Group Senior Staff, Carnegie Mellon Professor Emerita, IEEE Life Fellow, National Academy of Engineering member

#### Key Research

| Research Topic | Key Content |
|---------------|-------------|
| **Corrective actions for cascade prevention** | Minimizing transmission line failure effects through generation and load dispatch |
| **Advisory Tool for Managing Failure Cascades** | Failure cascade management tool for wind power systems |
| **Statistical cascade minimization** | Combining Monte Carlo + convex dynamic programming + adaptive selection |
| **Puerto Rico power grid redesign** | Cascading blackout prevention architecture using AC OPF (Lincoln Lab project) |
| **DyMonDS framework** | Hierarchical power system treatment; introduction of interaction variables |

**Three loss functions**: grid-centric, consumer-centric, and influence localization — for statistically evaluating the criticality of initial contingent failures.

#### Connection to This Project

- DD4 (Power Grid Cascading Failures): Ilic's statistical methods provide the physical foundation for GNN-based prediction covered in DD4
- Dahleh's network flow model provides the theoretical framework for load redistribution cascades

---

## 4. Supply Chain Shock Propagation

### 4.1 MIT CTL — Supply Chain AI and Resilience

**Lab**: Center for Transportation and Logistics (CTL)
**Lead Researchers**:
- **Yossi Sheffi** — MIT CTL Director, MIT SCALE Network Director, expert in systems optimization, risk analysis, and supply chain management
- **Matthias Winkenbach** — MIT CTL Research Director

#### Sheffi's Supply Chain Resilience Research

| Publication | Year | Key Content |
|------------|------|-------------|
| **The Resilient Enterprise** | MIT Press, 2005 | Building flexibility into five core supply chain elements (supplier, conversion, distribution, control, culture) |
| **The Power of Resilience** | MIT Press, 2015 | Pre-disruption choices matter more than mid-disruption responses; resilience benefits firms daily |
| **Global Supply Chain Vulnerability** | Ongoing | Ripple effects from global economic interconnectedness |

#### MIT CTL Recent Research (2024–2025)

| Research/Event | Key Content |
|---------------|-------------|
| **Intelligent Logistics Systems Lab (ILS)** | Logistics innovation at the intersection of OR, AI, ML (Mecalux-supported, launched 2024) |
| **eJournal: AI in Supply Chains** (Vol.1 No.3, 2025.12) | Special issue on AI for predictive analytics, inventory management, agility under uncertainty |
| **Generative AI for Supply Chain Resilience** | Generative AI for supply chain resilience (Winkenbach, featured in MIT Tech Review) |

### 4.2 MIT ORC — Supply Chain Risk Optimization

**Lab**: Operations Research Center (ORC)
**Lead Researchers**: ORC faculty

| Research | Key Content |
|----------|-------------|
| **Kevin Hu PhD Thesis** (Sept. 2024) | *"Predicting Risk and Optimizing Resilience of Digital and Physical Supply Chains"* |
| ORC research areas | Supply chain management, enterprise resilience, risk management, logistics optimization |

#### Connection to This Project

- DD5 (Supply Chain AI): Sheffi's resilience framework provides the practical motivation for AI-based supply chain research
- Theory-practice-technology triangle: Acemoglu model (§2.1) → Sheffi's practical perspective (§4.1) → AI models (DD5)

---

## 5. Social Network Information Propagation

### 5.1 Vosoughi-Roy-Aral — The Science of Misinformation Spread

**Lab**: MIT Media Lab (Social Machines Group), MIT Sloan, MIT IDE
**Lead Researchers**:
- **Soroush Vosoughi** — MIT Media Lab PhD (now Dartmouth professor)
- **Deb Roy** — MIT Media Lab Professor, Center for Constructive Communication (CCC) Director, founding director of Laboratory for Social Machines
- **Sinan Aral** — MIT Sloan David Austin Professor, MIT IDE Director

#### Landmark Paper: "The Spread of True and False News Online" (Science, 2018)

This paper is a **landmark in information cascade research**, analyzing information propagation mechanisms in social networks with large-scale empirical data:

| Item | Content |
|------|---------|
| **Data** | 2006–2017 Twitter data, ~126,000 news stories, ~3M users, ~4.5M tweets |
| **Verification** | 6 independent fact-checking organizations (95–98% agreement) |
| **Key finding** | False news spreads **significantly farther, faster, deeper, and more broadly** than truth |
| **Quantitative results** | False news is 70% more likely to be retweeted; reaches 1,500 people 6x faster than truth |
| **Causal analysis** | Higher "novelty" of false news → increased sharing motivation; evokes fear, disgust, surprise |
| **Bots vs. humans** | Bots spread true and false news at equal rates → **humans are the primary cause** of false news spread |

**Science cover story** (2018) — selected as one of the most influential academic publications of the year.

### 5.2 Sinan Aral — Experimental Studies of Social Contagion

**Lab**: MIT Sloan, MIT Initiative on the Digital Economy (IDE)

#### Key Paper Series

| Paper | Venue | Key Content |
|-------|-------|-------------|
| **Creating Social Contagion Through Viral Product Design** | Management Science, 2011 | 1.4M-user randomized experiment: passive-broadcast messaging generates **246% contagion increase**, active-personalized adds 98% |
| **Identifying Influential and Susceptible Members** | Science, 2012 | 1.3M Facebook user experiment: younger users more susceptible, men more influential, married individuals least susceptible |
| **Exercise Contagion in a Global Social Network** | Nature Communications, 2017 | Empirical proof that exercise behavior propagates through social networks at scale |
| **Tie Strength, Embeddedness, and Social Influence** | Management Science, 2014 | Large-scale experiment on the relationship between tie strength and social influence |

### 5.3 Alex "Sandy" Pentland — Social Physics

**Lab**: MIT Media Lab, Human Dynamics Laboratory
**Lead Researcher**:
- **Alex "Sandy" Pentland** — MIT Media Lab Toshiba Professor, Human Dynamics Lab Director

#### Social Physics Framework

Pentland studies how **idea flow** propagates through social networks and transforms into behaviors:

| Concept | Description |
|---------|-------------|
| **Exploring** | Exposure to novel ideas (information propagation through weak ties) |
| **Engagement** | Face-to-face social interaction (role of nonverbal communication) |
| **Network productivity** | Network productivity can be predicted from information exchange patterns alone (content-agnostic) |

**Major publication**: *Social Physics: How Good Ideas Spread — The Lessons from a New Science* (Penguin, 2014)

**Key findings**:
- eToro investment network: members with access to diverse strategies earned **30% higher returns**
- Increasing face-to-face interaction opportunities → **productivity gains** in banks, military, IT consulting

### 5.4 Deb Roy — Laboratory for Social Machines

**Lab**: MIT Media Lab → MIT Center for Constructive Communication (CCC)

| Research | Key Content |
|----------|-------------|
| **Laboratory for Social Machines (LSM)** | Founded 2014 with $10M Twitter investment; full Twitter data access |
| **Beat the Virus** | COVID-19 response — science-based public health guidance via social media influencers, **600M+ media impressions** |
| **Center for Constructive Communication** | Designing human-AI systems that foster dialogue, listening, and deliberation |

#### Connection to This Project

- DD3 (Social Influence Prediction): Aral's experimental research provides empirical grounding for AI models like DeepInf
- Vosoughi-Roy-Aral's false news study provides key evidence for **asymmetric propagation** in information cascades
- Pentland's Social Physics offers the social science framework for influence propagation

---

## 6. GNN Theory and Graph Learning

### 6.1 Xu-Jegelka — GNN Expressiveness Theory

**Lab**: MIT CSAIL
**Lead Researchers**:
- **Stefanie Jegelka** — MIT EECS Professor (now TU Munich, Alexander von Humboldt Professorship)
- **Keyulu Xu** — MIT EECS PhD (advised by Jegelka)

#### Key Papers

| Paper | Venue | Key Content |
|-------|-------|-------------|
| **How Powerful are Graph Neural Networks?** | ICLR 2019 | Theoretical limits of GNN expressiveness characterized via Weisfeiler-Lehman test; proposes **Graph Isomorphism Network (GIN)** |
| **Theory of Graph Neural Networks: Representation and Learning** | ICM 2022 Survey | Comprehensive theory of GNN approximation, generalization, and extrapolation properties |

#### "How Powerful are Graph Neural Networks?" Key Results

```
[Message Passing GNN Expressiveness Hierarchy]

GIN (Graph Isomorphism Network)
  <- Maximum expressiveness, equivalent to WL test
  <- Injective aggregation + sum pooling

GraphSAGE (mean pooling)
  <- Weaker than GIN
  <- Cannot distinguish certain simple graph structures

GCN (mean aggregation)
  <- Weakest expressiveness
  <- Greater structural information loss
```

**Impact**: This paper establishes the theoretical foundation for GNN propagation mechanisms covered in DD1. It sets **fundamental limits** on how well GNNs can capture propagation patterns.

### 6.2 Tommi Jaakkola — Message Passing and Graph Inference

**Lab**: MIT CSAIL
**Lead Researcher**:
- **Tommi Jaakkola** — MIT EECS Professor, CSAIL member

| Research Topic | Key Content |
|---------------|-------------|
| **GNN limitations proof** | Shortest/longest cycles, diameter, certain motifs cannot be computed by GNNs relying solely on local information |
| **Belief Propagation analysis** | Tree-based parameterization framework for analyzing BP and related algorithms |
| **Convergent propagation algorithms** | Max-product convergent message passing; convergent propagation via oriented trees |

### 6.3 Connection to This Project

- DD1 (GNN Propagation Mechanisms): GIN's expressiveness limits → motivation for improvements like PPNP, IP-GNN
- DD6 (Theoretical Synthesis): GNN theory forms the methodological foundation for cross-domain unified frameworks
- Jaakkola's message passing theory provides the theoretical basis for why GNNs mimic physical propagation processes

---

## 7. Network Inference and Systems Science

### 7.1 Devavrat Shah — Network Inference and Causal Inference

**Lab**: LIDS, ORC, Statistics and Data Science Center (SDSC)
**Lead Researcher**:
- **Devavrat Shah** — MIT EECS Professor, SDSC Director, 2025 ACM SIGMETRICS Achievement Award recipient

| Research Topic | Key Content |
|---------------|-------------|
| **Large-scale complex network theory** | Network algorithms, stochastic networks, large-scale statistical inference |
| **Patient-Zero identification** | Statistical methods for detecting the origin of contagion/cascades — cascade backtracking |
| **Graph-based inference** | Representing data as graphs; inference through inter-node correlations |
| **Causal inference** | Identifying causal relationships using observational and experimental data |

**Cascade research relevance**: Shah's Patient-Zero identification addresses the cascade backward problem — "Where did this cascade originate?" This directly connects to DD4 (power grid root cause analysis) and DD3 (influence propagation source tracking).

### 7.2 Ali Jadbabaie — Network Science and Collective Behavior

**Lab**: LIDS, IDSS, CEE
**Lead Researcher**:
- **Ali Jadbabaie** — MIT CEE Department Head, JR East Professor of Engineering, LIDS PI

| Research Topic | Key Content |
|---------------|-------------|
| **Network science** | Graph topology and community recovery from observing snapshots of independent network processes |
| **Spreading processes** | Theory of propagation processes in social networks |
| **Collective decision-making** | Dynamics of collective behavior and decision-making in socio-technical systems |
| **Multi-agent consensus** | Optimization-based control, multi-agent coordination and consensus |
| **MURI project** | DoD-funded "The Evolution of Cultural Norms and Dynamics of Sociopolitical Change" |

### 7.3 Connection to This Project

- Shah's cascade source detection → complementary to DD4's root cause analysis (causal inference)
- Jadbabaie's spreading process theory → theoretical foundation for DD3, DD6
- Both researchers are LIDS members, covering theory and methodology axes of network inference

---

## 8. MIT AI Risk Repository

**Lab**: MIT FutureTech
**URL**: https://airisk.mit.edu/

The MIT AI Risk Repository systematically classifies AI system risks, including categories relevant to this project:
- **Cascading failures** in multi-agent interactions
- Selection pressures, security vulnerabilities, information deficits and trust erosion
- Propagation effects between AI systems

---

## 9. Comprehensive Researcher and Lab Mapping

### 9.1 Key Researcher Profiles

| Researcher | Affiliation | Position | Key Contribution | Related DD |
|-----------|-------------|----------|------------------|------------|
| **Daron Acemoglu** | Economics | Institute Professor | Network economics, shock propagation theory | DD5, DD6 |
| **Asuman Ozdaglar** | EECS, LIDS | MathWorks Professor | Cascade mathematical models, network security | DD6 |
| **Munther Dahleh** | EECS, LIDS, IDSS | Coolidge Professor | Cascading failure dynamics, systemic risk | DD4, DD6 |
| **Marija Ilic** | LIDS, Lincoln Lab, EESG | Senior Research Scientist | Power system cascade prevention | DD4 |
| **Yossi Sheffi** | CTL | Director | Supply chain resilience | DD5 |
| **Sinan Aral** | Sloan, IDE | David Austin Professor | Experimental social contagion research | DD3 |
| **Deb Roy** | Media Lab, CCC | Professor | Misinformation spread, Social Machines | DD3 |
| **Alex Pentland** | Media Lab | Toshiba Professor | Social Physics, idea flow | DD3 |
| **Devavrat Shah** | EECS, LIDS, SDSC | Professor | Network inference, cascade source detection | DD6 |
| **Ali Jadbabaie** | CEE, LIDS, IDSS | JR East Professor | Network science, spreading process theory | DD3, DD6 |
| **Stefanie Jegelka** | EECS, CSAIL | Professor (now TUM) | GNN expressiveness theory (GIN) | DD1 |
| **Keyulu Xu** | EECS, CSAIL | PhD Student | GIN, WL test connection | DD1 |
| **Tommi Jaakkola** | EECS, CSAIL | Professor | GNN limitations, message passing theory | DD1, DD6 |

### 9.2 Lab-Level Summary

| Lab | Abbreviation | Key Research Topics | Lead Faculty |
|-----|-------------|---------------------|-------------|
| **Laboratory for Information and Decision Systems** | LIDS | Network dynamics, cascading failures, systemic risk, network inference | Dahleh, Shah, Jadbabaie, Ozdaglar |
| **Institute for Data, Systems, and Society** | IDSS | Systemic risk, financial networks, socio-technical systems | Dahleh (founding director), Jadbabaie |
| **Computer Science and AI Laboratory** | CSAIL | GNN theory, message passing, graph learning | Jegelka, Jaakkola |
| **Center for Transportation and Logistics** | CTL | Supply chain resilience, AI in supply chains | Sheffi, Winkenbach |
| **Operations Research Center** | ORC | Supply chain risk optimization, network algorithms | Shah (joint), multiple faculty |
| **Media Lab** | — | Social network propagation, misinformation, Social Physics | Roy, Pentland |
| **MIT Sloan / IDE** | — | Social contagion experiments, digital economy | Aral |
| **Economics Department** | — | Network economics, macroeconomic shock propagation | Acemoglu |
| **Electric Energy Systems Group** | EESG | Power system cascades, resilience | Ilic |
| **Lincoln Laboratory** | LL | Infrastructure resilience, power grid redesign | Ilic (joint) |

---

## 10. Integrated Perspective on MIT Research

### 10.1 Theory → Methodology → Application Pipeline

```
[Theoretical Foundations (Layer 1)]
Acemoglu-Ozdaglar: Network economics
Dahleh: Network flow dynamics
Pentland: Social Physics
  |
  v
[Methodological Innovations (Layer 2)]
Xu-Jegelka: GNN expressiveness theory (GIN)
Jaakkola: Message passing limitations
Shah: Cascade source detection
Jadbabaie: Spreading process recovery
  |
  v
[Empirical Validation (Layer 3)]
Vosoughi-Roy-Aral: False news spread (126K stories, 3M users)
Aral: Social contagion randomized experiments (1.3M+ users)
  |
  v
[Domain Applications (Layer 4)]
Sheffi-CTL: Supply chain resilience
Ilic-EESG: Power grid cascade prevention
ORC: Supply chain risk optimization
```

### 10.2 Distinctive Strengths of MIT Research

| Strength | Description |
|----------|-------------|
| **Theory-empirics integration** | Mathematical theory (Acemoglu) and large-scale experiments (Aral) conducted at the same institution |
| **Multidisciplinary collaboration** | Natural intersection of Economics + EECS + Media Lab + Sloan + CEE |
| **Scale of data** | Full Twitter dataset (Roy), 1.3M Facebook users (Aral), and other large-scale empirical studies |
| **Theoretical depth** | From fundamental GNN expressiveness limits (Xu-Jegelka) to mathematical foundations of network economics (Acemoglu) |
| **Practical connection** | CTL industry partnerships, Lincoln Lab real infrastructure projects |

### 10.3 Implications for This Project

1. **Strengthening theoretical foundations**: Acemoglu-Ozdaglar models are core to DD5 (supply chains) and DD6 (theoretical synthesis), but deserve deeper treatment (especially *Microeconomic Origins of Macroeconomic Tail Risks*)
2. **GNN limitation awareness**: The fundamental GNN limits shown by Xu-Jegelka's GIN paper directly connect to DD1's over-smoothing problem
3. **Empirical evidence reinforcement**: Aral's social contagion experiment results can be used to validate AI models in DD3
4. **Cascade source detection**: Shah's Patient-Zero research provides theoretical complement to DD4 (power grid root cause analysis)
5. **Misinformation propagation**: Vosoughi-Roy-Aral's study offers a new perspective on **asymmetric propagation** in information cascades

---

## 11. References

### Network Economics and Cascade Theory
- Acemoglu, Carvalho, Ozdaglar, Tahbaz-Salehi. [The Network Origins of Aggregate Fluctuations](https://economics.mit.edu/sites/default/files/publications/The%20Network%20Origins%20of%20Aggregate%20Fluctuations.pdf). Econometrica, 2012.
- Acemoglu, Ozdaglar, Tahbaz-Salehi. [Cascades in Networks and Aggregate Volatility](https://www.nber.org/system/files/working_papers/w16516/w16516.pdf). NBER WP 16516, 2010.
- Acemoglu, Ozdaglar, Tahbaz-Salehi. [Systemic Risk and Stability in Financial Networks](https://economics.mit.edu/sites/default/files/publications/Systemic%20Risk%20and%20Stability%20in%20Financial%20Networks..pdf). AER, 2015.
- Acemoglu, Ozdaglar, Tahbaz-Salehi. Microeconomic Origins of Macroeconomic Tail Risks. AER, 2017.
- Acemoglu, Malekian, Ozdaglar. [Network Security and Contagion](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2285816). JET, 2016.
- Lim, Ozdaglar. [A Simple Model of Cascades in Networks](http://t8el.com/wp-content/uploads/2015/08/SimpleCascades.pdf).

### Power Grid Cascading Failures
- LIDS Seminar. [Predicting Failure Cascades in Large Scale Power Systems via the Influence Model Framework](https://lids.mit.edu/news-and-events/events/predicting-failure-cascades-large-scale-power-systems-influence-model).
- LIDS Seminar. [Quantifying Cascading Failure Propagation in Blackouts](https://lids.mit.edu/news-and-events/events/quantifying-cascading-failure-propagation-blackouts-electrical-transmission).
- Dahleh et al. [Robust Network Routing under Cascading Failures](https://dspace.mit.edu/bitstream/handle/1721.1/99950/Dahleh_Robust%20network.pdf).
- Ilic et al. [Advisory Tool for Managing Failure Cascades in Systems with Wind Power](https://arxiv.org/abs/2211.15957).
- Ilic et al. [Towards Statistical Methods for Minimizing Effects of Failure Cascades](https://www.researchgate.net/publication/365091195).

### Social Network Propagation
- Vosoughi, Roy, Aral. [The Spread of True and False News Online](https://www.science.org/doi/10.1126/science.aap9559). Science, 2018.
- Aral, Walker. [Creating Social Contagion Through Viral Product Design](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1564856). Management Science, 2011.
- Aral, Walker. [Identifying Influential and Susceptible Members of Social Networks](https://www.science.org/cms/asset/eff8876a-1565-45d1-b8d1-11ab8680834e/pap.pdf). Science, 2012.
- Aral, Nicolaides. [Exercise Contagion in a Global Social Network](https://www.nature.com/articles/ncomms14753). Nature Communications, 2017.
- Pentland. Social Physics: How Good Ideas Spread. Penguin, 2014.

### GNN Theory
- Xu, Hu, Leskovec, Jegelka. [How Powerful are Graph Neural Networks?](https://arxiv.org/abs/1810.00826). ICLR, 2019.
- Jegelka. [Theory of Graph Neural Networks: Representation and Learning](https://arxiv.org/abs/2204.07697). ICM, 2022.

### Supply Chain Resilience
- Sheffi. The Resilient Enterprise. MIT Press, 2005.
- Sheffi. [The Power of Resilience](https://sheffi.mit.edu/book/power-resilience). MIT Press, 2015.
- MIT CTL. [eJournal: AI in Supply Chains](https://ctl.mit.edu/publications/ejournal-issue-ai-supply-chains-vol-1-no-3-december-2025). Vol.1 No.3, 2025.

### Network Inference
- Shah. [Networks of Probability](https://news.mit.edu/2013/devavrat-shah-networks-probability-0207). MIT News, 2013.
- Jadbabaie. [Network Science Research](https://jadbabaie.mit.edu/research/network-science/).
