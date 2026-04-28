# Graph Mining: Uncovering Community Structure in Social Networks

**CSCE 676 — Data Mining | Texas A&M University | Spring 2026**  
**Student:** Zhuofeng Li

---

## Overview

Every major social platform depends on one question: *who belongs with whom?* This project investigates how to automatically discover community structure in social networks using three complementary approaches — classic graph partitioning, supervised classification on hand-crafted structural features, and neural graph embeddings via Node2Vec.

The target dataset is the **Facebook Social Circles** network from Stanford SNAP (4,039 nodes, 88,234 edges). Zachary's Karate Club is used as a ground-truth-verified proxy throughout, enabling rigorous quantitative evaluation that is not possible on the full Facebook graph.

👉 **Start here: [main_notebook.ipynb](main_notebook.ipynb)**

---

## Project Video

🎥 **[Watch the 2-minute project walkthrough](#)** *(https://www.youtube.com/watch?v=D78wGRhHHi0)*

---

## Research Questions

| # | Question | Approach | Key Algorithms | Metric |
|---|----------|----------|---------------|--------|
| **RQ1** | Which community detection algorithm most faithfully recovers ground-truth social circles? | Unsupervised graph partitioning | Louvain, Label Propagation, Greedy Modularity | NMI, ARI |
| **RQ2** | How accurately can hand-crafted structural features predict community membership, and where do they fail? | Supervised classification | Logistic Regression, Random Forest | Macro F1, ROC-AUC |
| **RQ3** | Can Node2Vec graph embeddings outperform structural features, and which (p, q) walk strategy works best? | Representation learning | Node2Vec + grid search | Macro F1, Silhouette |

---

## Key Results

| Method | Type | Score | Metric |
|--------|------|-------|--------|
| Majority-class baseline | Baseline | 0.49 | F1 Macro |
| Label Propagation | RQ1 — Course | 0.36 | NMI |
| Greedy Modularity | RQ1 — Course | 0.56 | NMI |
| **Louvain** | **RQ1 — Course** | **0.60** | **NMI** |
| Logistic Regression (struct. features) | RQ2 — Course | 0.84 | F1 Macro |
| Random Forest (struct. features) | RQ2 — Course | 0.84 | F1 Macro |
| **Node2Vec + Logistic Regression** | **RQ3 — Beyond** | **0.97** | **F1 Macro** |

**Big takeaway:** Modularity-optimizing algorithms (Louvain, Greedy Modularity) decisively outperform Label Propagation for community recovery. Node2Vec embeddings break through the structural-feature ceiling by encoding multi-hop patterns that no hand-crafted feature can capture — lifting F1 from 0.84 to 0.97.

---

## Data

### Zachary's Karate Club (primary — no download needed)
Available directly from NetworkX:
```python
import networkx as nx
G = nx.karate_club_graph()   # 34 nodes, 78 edges, ground-truth labels included
```

### Facebook Social Circles (target dataset)
- **Source:** [Stanford SNAP](https://snap.stanford.edu/data/ego-Facebook.html)
- **Size:** 4,039 nodes · 88,234 edges
- Too large to commit — see [`data/README.md`](data/README.md) for download instructions.

---

## Repo Structure

```
graph-mining-community-detection/
├── main_notebook.ipynb          ← curated final project notebook (start here)
├── requirements.txt             ← pinned dependencies
├── .gitignore
├── README.md
├── checkpoints/
│   ├── checkpoint_1.ipynb       ← dataset selection & EDA (Feb 2026)
│   └── checkpoint_2.ipynb       ← research question formation (Mar 2026)
└── data/
    └── README.md                ← dataset download instructions
```

---

## How to Reproduce

This project was developed locally with Python 3.12. All analysis runs in a single notebook with no external scripts.

```bash
# 1. Clone the repo
git clone https://github.com/Zhuofeng-Li/graph-mining-community-detection.git
cd graph-mining-community-detection

# 2. Create a virtual environment and install dependencies
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# 3. Launch Jupyter and open the main notebook
jupyter notebook main_notebook.ipynb
```

The Karate Club graph loads automatically from NetworkX — no data download is needed to run the full notebook.

---

## Key Dependencies

| Package | Version |
|---------|---------|
| Python | 3.12.9 |
| networkx | 3.6.1 |
| node2vec | 0.5.0 |
| gensim | 4.4.0 |
| scikit-learn | 1.8.0 |
| numpy | 1.26.4 |
| pandas | 3.0.0 |
| matplotlib | 3.10.8 |

Full pinned list: [`requirements.txt`](requirements.txt)

---

## References

1. McAuley, J., & Leskovec, J. (2012). Learning to Discover Social Circles in Ego Networks. *NeurIPS*.
2. Grover, A., & Leskovec, J. (2016). node2vec: Scalable Feature Learning for Networks. *KDD*.
3. Zachary, W. W. (1977). An information flow model for conflict and fission in small groups. *Journal of Anthropological Research, 33*(4), 452–473.
4. Blondel et al. (2008). Fast unfolding of communities in large networks. *Journal of Statistical Mechanics*.
