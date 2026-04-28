# Data

## Dataset: Zachary's Karate Club (Primary)

Used directly from NetworkX — no download required:

```python
import networkx as nx
G = nx.karate_club_graph()
```

This is a canonical benchmark graph (34 nodes, 78 edges) with ground-truth community labels, used as the ground-truth-verified proxy throughout this project.

## Dataset: Facebook Social Circles (SNAP) — Target Dataset

The full-scale target dataset is not committed to this repo due to size.

- **Source:** [Stanford SNAP — ego-Facebook](https://snap.stanford.edu/data/ego-Facebook.html)
- **Download:** `wget https://snap.stanford.edu/data/facebook_combined.txt.gz`
- **Format:** Edge list, one `src dst` pair per line (undirected)
- **Size:** 4,039 nodes · 88,234 edges

To use in the notebook, place the extracted `facebook_combined.txt` in this `data/` folder and update the load path accordingly.

## Preprocessing

No external preprocessing scripts are required. All graph construction and feature engineering are done inline in `main_notebook.ipynb`.
