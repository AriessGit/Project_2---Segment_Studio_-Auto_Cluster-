# Segment Studio — Sample Data & Results 🌸

This folder contains sample files demonstrating a full run of **Segment Studio** on the classic [Iris dataset](https://en.wikipedia.org/wiki/Iris_flower_data_set), stripped of its species labels.

---

## Files

### `iris_no_label.csv`
The input file fed into Segment Studio.  
150 rows × 4 numeric features — species labels intentionally removed.

| Column | Description |
|---|---|
| `sepal_length` | Sepal length in cm |
| `sepal_width` | Sepal width in cm |
| `petal_length` | Petal length in cm |
| `petal_width` | Petal width in cm |

---

### `iris_no_label_clustered.csv`
The exported output from Step 5 of Segment Studio.  
Same 150 rows as the input, with one column added:

| Column | Description |
|---|---|
| `sepal_length` | *(original)* |
| `sepal_width` | *(original)* |
| `petal_length` | *(original)* |
| `petal_width` | *(original)* |
| `cluster_name` | AI-generated cluster name assigned to each row |

---

### `conclusions.csv`
The cluster summary table generated in Step 4 of Segment Studio.  
6 clusters were identified (k=6), each named and described by LLaMA.

| cluster_id | count | name | description |
|---|---|---|---|
| 0 | 34 | Small Petal Width | Characterized by small petal widths and moderate sepal and petal lengths |
| 1 | 27 | Small Petal Species | Relatively small petal lengths and widths, moderate sepal dimensions |
| 2 | 23 | Small Petal Clusters | Small petal lengths and widths, moderate sepal lengths and widths |
| 3 | 16 | Small Petal Clusters | Small sepal and petal lengths, average values below the overall mean |
| 4 | 28 | Small Petal Width Group | Small petal widths averaging 2.17, moderate sepal and petal lengths |
| 5 | 22 | Small Petal Width | Small petal width and moderate sepal dimensions |

---

## How These Files Were Generated

1. `iris_no_label.csv` was uploaded to Segment Studio
2. WCSS (Elbow method) was run for k = 2–10
3. k = 6 was selected based on the elbow plot
4. Clusters were created and named via LLaMA (`meta-llama/Meta-Llama-3-8B-Instruct`)
5. The clustered CSV was exported → `iris_no_label_clustered.csv`
6. The cluster summary table was saved → `conclusions.csv`

---

## Notes

- The Iris dataset originally has 3 species (setosa, versicolor, virginica). Using k=6 over-segments the data relative to the ground truth, but demonstrates the tool's ability to find sub-group structure.
- Cluster names were generated automatically by LLaMA based on statistical summaries — not ground-truth labels.
- To reproduce these results, run Segment Studio with `iris_no_label.csv` and select k=6.
