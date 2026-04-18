# What Drives Conflict Between Reddit Communities?

## 📖 Overview

This **Data Mining Course (CSCE 676)** project (**`237007751_checkpoint2.ipynb`**) analyzes the **Reddit Hyperlink Network** (SNAP) to ask: **can we predict hostile cross-subreddit links, and do network structure or post language drive inter-community conflict?** It includes:

- **Conflict-focused EDA**: Sentiment skew, temporal patterns, hubs vs. high-hostility-rate targets, degree distributions.
- **Graph mining (course)**: Louvain community detection, PageRank, betweenness centrality — cross-community vs. within-community hostility, influential vs. controversial subreddits.
- **Frequent itemsets / association rules (course)**: Apriori on hostile co-targeting “baskets” to find **conflict corridors**.
- **Supervised learning (course + external)**: Gradient boosted decision trees plus **L1-regularized logistic regression (Lasso)** for prediction and sparse feature selection, using **network features** and **86 LIWC** linguistic features per post.

Earlier work in `237007751_checkpoint1.ipynb` covers dataset comparison, selection, and initial EDA; **the full research analysis and final deliverable live in Checkpoint 2.**

**Author:** Keshav Kapur | **UIN:** 237007751

---

## 📦 Installation

Clone this repository and install dependencies:

```bash
git clone https://github.com/<your-username>/Data-Mining-Project.git
cd Data-Mining-Project
pip install -r requirements.txt
```

**Dependencies** (see `requirements.txt`): `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `mlxtend`, `urllib3`, `networkx`.

For a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate  
pip install -r requirements.txt
```

---

## ⚡ Quick Start

### 1. Add Reddit Hyperlink Data

The notebook downloads the **Reddit Hyperlink Network** (SNAP) automatically if not present:

- **Body links**: [soc-redditHyperlinks-body.tsv](https://snap.stanford.edu/data/soc-redditHyperlinks-body.tsv) (~319 MB)
- **Title links**: [soc-redditHyperlinks-title.tsv](https://snap.stanford.edu/data/soc-redditHyperlinks-title.tsv) (~369 MB)

Place them in `data/` or run the notebook; it will create `data/` and download when needed.

### 2. Run the Notebook

Open and run all cells in **`237007751_checkpoint2.ipynb`** (main project):

```bash
jupyter notebook 237007751_checkpoint2.ipynb
# or
jupyter lab 237007751_checkpoint2.ipynb
```

The notebook uses **body** links as the primary dataset (more substantive than title-only links). Use `237007751_checkpoint1.ipynb` only for the earlier dataset-comparison and baseline EDA checkpoint.

### 3. Main workflow (Checkpoint 2)

| Phase | Description |
|--------|-------------|
| **Setup** | Load TSVs → parse LIWC `PROPERTIES` → build aggregated directed graph |
| **Conflict EDA** | Sentiment distribution, time, top targets by volume vs. hostility rate, degree distributions |
| **RQ1 — Graph mining** | Louvain, PageRank, betweenness; cross-community vs. within-community hostility |
| **RQ2 — Association rules** | Apriori on hostile co-target baskets; conflict vs. friendly corridors |
| **RQ3 — Prediction** | GDBT + Lasso; network + LIWC features; ROC-AUC, precision/recall, sparsity |
---

## 📊 Example Output

**Graph summary (body links):**

| Metric | Value |
|--------|--------|
| Nodes (subreddits) | 35,776 |
| Unique directed edges | 137,821 |
| Total hyperlinks (multi-edges) | 286,561 |
| Density | ~0.0001 |
| Time range | 2013-12-31 → 2017-04-30 |

**Core columns (after preparation):**

| Column | Description |
|--------|-------------|
| `SOURCE_SUBREDDIT` | Subreddit that posts the link |
| `TARGET_SUBREDDIT` | Subreddit being linked to |
| `POST_ID` | Reddit post ID |
| `TIMESTAMP` | When the link was posted |
| `POST_LABEL` | Link sentiment: +1 (positive) or -1 (negative) |

**Sample frequent 2-itemsets (co-linked subreddit pairs):**

- `askreddit` + `iama`, `askreddit` + `pics`, `askreddit` + `todayilearned`, …
- Association rules (e.g. `mhocpress` → `mhoc`) with confidence and lift.

---

## 🧩 Key Features

- **Deterministic data pipeline**: Load body TSVs → rename columns → **parse 86 LIWC features** from `PROPERTIES` → parse timestamps → aggregate multi-edges (weight, average sentiment).
- **Directed signed graph**: NetworkX `DiGraph` with edge attributes for centrality, Louvain, and structural features for classification.
- **Graph statistics & centrality**: Degree distributions, PageRank, approximate betweenness, community labels for cross-community features.
- **Visualizations**: Conflict EDA, centrality vs. hostility scatter, corridor comparisons, model evaluation curves.
- **Community detection**: Louvain partitions for cross-community vs. within-community analysis.
- **Association rules**: Hostile co-target baskets; Apriori + confidence/lift for **conflict corridors** vs. friendly patterns.
- **Supervised models**: GDBT (course) + L1 logistic regression (external) for interpretable feature selection on high-dimensional LIWC + network inputs.

---

## 📝 Notes

- **Data**: Reddit Hyperlink Network from [SNAP (Stanford)](https://snap.stanford.edu/data/soc-RedditHyperlinks.html). Research/academic use; data derived from public Reddit posts.
- **Bias**: English-language and popular subreddits dominate; sentiment labels are crowdsourced. See the bias and ethics discussion in Checkpoint 1 / early sections of Checkpoint 2.
- **Scale**: ~35K nodes and ~138K unique edges (body) fit in memory; NetworkX and mlxtend run on a typical laptop.
- Data files are not committed (too large); the notebook downloads them when needed.

---

## ✨ Citation

If you use this dataset or build on this code, please cite the Reddit Hyperlink Network paper:

```bibtex
@inproceedings{kumar2018community,
  title={Community Interaction and Conflict on the Web},
  author={Kumar, Srijan and Hamilton, William L. and Leskovec, Jure and Jurafsky, Daniel},
  booktitle={Proceedings of the 2018 World Wide Web Conference (WWW 2018)},
  year={2018},
}
```

Dataset: [SNAP – Reddit Hyperlink Network](https://snap.stanford.edu/data/soc-RedditHyperlinks.html).
