# Segment Studio — Sample Data & Results 🚗

This folder contains sample files demonstrating a full run of **Segment Studio** on the classic [Auto MPG dataset](https://archive.ics.uci.edu/dataset/9/auto+mpg), a well-known benchmark dataset of fuel efficiency measurements for cars from model years 1970–1982.

---

## Files

### `mpg.csv`
The input file fed into Segment Studio.  
398 rows × 9 columns covering numeric performance metrics, origin, and model name.

| Column | Type | Description |
|---|---|---|
| `mpg` | float | Fuel efficiency (miles per gallon) |
| `cylinders` | int | Number of engine cylinders (3–8) |
| `displacement` | float | Engine displacement (cubic inches) |
| `horsepower` | str | Engine horsepower (contains some missing values as `?`) |
| `weight` | int | Vehicle weight (lbs) |
| `acceleration` | float | 0–60 mph time (seconds) |
| `model_year` | int | Model year (70–82, i.e. 1970–1982) |
| `origin` | int | Manufacturer origin: 1 = American, 2 = European, 3 = Japanese |
| `name` | str | Vehicle make and model |

---

### `mpg_clustered.csv`
The exported output from Step 5 of Segment Studio.  
Same 398 rows as the input, with one column added:

| Column | Description |
|---|---|
| *(all original columns)* | Preserved from `mpg.csv` |
| `cluster_name` | AI-generated cluster name assigned to each row |

> ⚠️ **Note:** 61 rows show `cluster_name = "API Error"` — the LLaMA API returned a 503 error for cluster 4 during generation. See `conclusions.csv` for details.

---

### `conclusions.csv`
The cluster summary table generated in Step 4 of Segment Studio.  
8 clusters were identified (k=8), named and described by LLaMA.

| cluster_id | count | name | description |
|---|---|---|---|
| 0 | 59 | Classic European Sedans | Older, smaller European sedans focused on fuel efficiency and moderate performance |
| 1 | 40 | Classic American Muscle Cars | American cars from the 1970s with high horsepower, displacement, and weight |
| 2 | 58 | Classic American Economy Cars | American-made economy cars from the 1970s–80s focused on fuel efficiency |
| 3 | 45 | Japanese Compact Sedans | Japanese compact sedans including Toyota Corolla, Mazda 626, and Honda Accord |
| 4 | 61 | *(API Error)* | LLaMA API was unavailable (503) during generation — cluster was not named |
| 5 | 74 | American Compact Cars | American compact cars from the 1970s including Ford Maverick and AMC Gremlin |
| 6 | 32 | Classic European Economy Cars | European economy cars from the 1970s including Ford Pinto and Peugeot 504 |
| 7 | 29 | Early Economy Cars | Early economy models with lower horsepower, mixed Japanese and American brands |

---

## How These Files Were Generated

1. `mpg.csv` was uploaded to Segment Studio
2. WCSS (Elbow method) was run to determine the optimal k
3. k = 8 was selected based on the elbow plot
4. Clusters were created and named via LLaMA (`meta-llama/Meta-Llama-3-8B-Instruct`)
5. The clustered CSV was exported → `mpg_clustered.csv`
6. The cluster summary table was saved → `conclusions.csv`

---

## Notes

- The `horsepower` column contains `?` for missing values (originally 6 rows) — handled automatically by Segment Studio's preprocessing step.
- The `origin` column is encoded as integers (1/2/3). Segment Studio treats it as numeric; results may differ if it is re-encoded as a categorical variable.
- Cluster 4 failed to receive a name due to a temporary Hugging Face API outage during generation. Re-running Step 4 should resolve this.
- The Auto MPG dataset is originally from the UCI Machine Learning Repository.
