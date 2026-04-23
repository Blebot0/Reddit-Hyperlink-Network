# What Drives Conflict Between Reddit Communities?

Author: Keshav Kapur (UIN: 237007751)

## Main Deliverable

Start here: `main_notebook.ipynb`

Checkpoint progression notebooks:
- `checkpoints/237007751_checkpoint1.ipynb`
- `checkpoints/237007751_checkpoint2.ipynb`

Project video:
- [Project walkthrough video](https://youtu.be/nEsfS9ury3U)

## Project Overview

This CSCE 676 Data Mining project analyzes the SNAP Reddit Hyperlink Network to study inter-community conflict. The central theme is whether hostile cross-subreddit links can be predicted, and which factors are most informative: network structure, language features, or both.

The final notebook includes conflict-focused exploratory analysis, graph mining, association rule mining, and supervised learning with network plus LIWC-derived text features.

## Research Questions

1. How does subreddit network structure relate to hostile cross-community interactions?
2. Which subreddit pairs are frequently co-targeted in hostile contexts, and what conflict corridors emerge?
3. How accurately can hostile links be predicted using graph and linguistic features?

## Data and Preprocessing

Dataset source:
- [SNAP: Reddit Hyperlink Network](https://snap.stanford.edu/data/soc-RedditHyperlinks.html)

Primary files used:
- [soc-redditHyperlinks-body.tsv](https://snap.stanford.edu/data/soc-redditHyperlinks-body.tsv)
- [soc-redditHyperlinks-title.tsv](https://snap.stanford.edu/data/soc-redditHyperlinks-title.tsv)

Preprocessing in the notebook:
- Load raw TSV files
- Parse LIWC attributes from `PROPERTIES`
- Parse timestamps and sentiment labels
- Aggregate multi-edges into a directed graph representation
- Build analysis/modeling features from graph and language signals

If raw files are not already in `data/`, the notebook workflow creates the folder and downloads needed files.
The repository keeps `data/.gitkeep` so the directory is tracked even when large dataset files are not committed.

## Reproducibility

This project was developed in Colab-style notebook workflows and is runnable locally with Jupyter.

1. Install dependencies:

```bash
pip install -r requirements.txt
```

2. Run the final deliverable notebook:

```bash
jupyter notebook main_notebook.ipynb
```

3. Optional progression review:
- Open `checkpoints/237007751_checkpoint1.ipynb` first
- Then `checkpoints/237007751_checkpoint2.ipynb`
- Then `main_notebook.ipynb` (submission notebook copy)

## Key Dependencies and Versions

Python:
- Local runtime reference: `Python 3.14.0`

Core packages (pinned package list lives in `requirements.txt`):
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `scikit-learn`
- `mlxtend`
- `urllib3`
- `networkx`
- `scipy`

## Repository Structure

```text
Data-Mining-Project/
├── checkpoints/
│   ├── 237007751_checkpoint1.ipynb
│   └── 237007751_checkpoint2.ipynb
├── main_notebook.ipynb
├── requirements.txt
├── README.md
├── data/
│   └── .gitkeep
└── .gitignore
```

## Results Summary

The analysis finds measurable structure in hostile inter-subreddit linking behavior, including identifiable conflict corridors and graph-level patterns that align with cross-community hostility. Predictive models using combined network and LIWC linguistic features provide meaningful signal for hostile-link classification.
