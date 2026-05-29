# Segment Studio — Examples

This folder contains three end-to-end examples demonstrating **Segment Studio** on well-known public datasets. Each example includes the original input CSV, the clustered output CSV, a cluster summary table, and its own dedicated README.

---

## Examples

### 🌸 Iris — [`iris/`](./iris/)
Clustering the classic Iris flower dataset (150 rows, 4 numeric features) with species labels removed. Demonstrates Segment Studio on a clean, purely numeric dataset with known ground-truth structure.

- **Input:** `iris_no_label.csv` — 150 rows × 4 features
- **k selected:** 6
- **Highlights:** Over-segmentation of 3 species into 6 sub-groups; all clusters named successfully

---

### 🚗 Auto MPG — [`mpg/`](./mpg/)
Clustering a dataset of car fuel efficiency measurements (398 rows, 9 columns) spanning model years 1970–1982. Demonstrates Segment Studio on a mixed dataset with numeric, categorical, and missing-value columns.

- **Input:** `mpg.csv` — 398 rows × 9 features
- **k selected:** 8
- **Highlights:** Mixed numeric/categorical data; `horsepower` contains missing values handled automatically; 1 cluster (61 rows) received an API Error due to a temporary Hugging Face outage

---

### 🍽️ Tips — [`tips/`](./tips/)
Clustering a restaurant tipping dataset (244 rows, 11 columns) covering bill amounts, tips, and diner demographics. Demonstrates Segment Studio on behavioral/transactional data with categorical features dominating the segmentation.

- **Input:** `tips.csv` — 244 rows × 11 features
- **k selected:** 7
- **Highlights:** Segmentation driven by gender, day, and meal time; synthetic PII columns included for demonstration; all clusters named successfully

---

## Folder Structure

```
examples/
├── README.md                          ← this file
│
├── iris/
│   ├── README.md
│   ├── iris_no_label.csv
│   ├── iris_no_label_clustered.csv
│   └── conclusions.csv
│
├── mpg/
│   ├── README.md
│   ├── mpg.csv
│   ├── mpg_clustered.csv
│   └── conclusions.csv
│
└── tips/
    ├── README.md
    ├── tips.csv
    ├── tips_clustered.csv
    └── conclusions.csv
```

---

## Common File Conventions

Across all examples, three file types appear consistently:

| File | Description |
|---|---|
| `<dataset>.csv` | Original input file uploaded to Segment Studio |
| `<dataset>_clustered.csv` | Input file with an added `cluster_name` column |
| `conclusions.csv` | Cluster summary table: `cluster_id`, `count`, `name`, `description` |

Each example's `README.md` documents the full column schema, cluster table, generation steps, and dataset-specific notes.
