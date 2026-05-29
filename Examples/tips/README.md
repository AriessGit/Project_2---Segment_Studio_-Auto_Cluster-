# Segment Studio — Sample Data & Results 🍽️

This folder contains sample files demonstrating a full run of **Segment Studio** on the classic [Tips dataset](https://github.com/mwaskom/seaborn-data/blob/master/tips.csv), a well-known dataset of restaurant tipping behavior collected from a single restaurant over several months.

---

## Files

### `tips.csv`
The input file fed into Segment Studio.  
244 rows × 11 columns covering bill amounts, tips, and diner demographics.

| Column | Type | Description |
|---|---|---|
| `total_bill` | float | Total bill amount (USD, range: $3.07–$50.81) |
| `tip` | float | Tip amount (USD, range: $1.00–$10.00) |
| `sex` | str | Diner's sex: `Male` (157) or `Female` (87) |
| `smoker` | str | Smoking section: `Yes` (93) or `No` (151) |
| `day` | str | Day of visit: `Sat` (87), `Sun` (76), `Thur` (62), `Fri` (19) |
| `time` | str | Meal time: `Dinner` (176) or `Lunch` (68) |
| `size` | int | Party size (1–6) |
| `price_per_person` | float | `total_bill / size` |
| `Payer Name` | str | Name of the person who paid |
| `CC Number` | int | Credit card number of the payer |
| `Payment ID` | str | Unique payment identifier |

> ⚠️ **Note:** `Payer Name`, `CC Number`, and `Payment ID` are synthetic PII columns added to the original dataset for demonstration purposes. Do not treat them as real personal data.

---

### `tips_clustered.csv`
The exported output from Step 5 of Segment Studio.  
Same 244 rows as the input, with one column added:

| Column | Description |
|---|---|
| *(all original columns)* | Preserved from `tips.csv` |
| `cluster_name` | AI-generated cluster name assigned to each row |

---

### `conclusions.csv`
The cluster summary table generated in Step 4 of Segment Studio.  
7 clusters were identified (k=7), each named and described by LLaMA.

| cluster_id | count | name | description |
|---|---|---|---|
| 0 | 28 | Male Diners on Weekends | Mostly male, weekend diners with a preference for dinner and a moderate bill |
| 1 | 34 | Male Diners on Sunday | Mostly male, Sunday diners with a high average total bill and tip |
| 2 | 21 | Male Diners on Weekends | Mostly male, weekend dinner diners who predominantly pay with credit cards |
| 3 | 48 | Male Diners on Saturday | Male Saturday diners, mix of smokers and non-smokers, preference for dinner |
| 4 | 27 | Female Lunchtime Diners | Mostly female lunchtime diners |
| 5 | 57 | Male Diners on Sundays | Male Sunday diners, higher proportion of non-smokers, moderate average bill |
| 6 | 29 | Female Lunchtime Diners | Mostly female, non-smoking lunchtime diners with a median bill of ~$14 |

---

## How These Files Were Generated

1. `tips.csv` was uploaded to Segment Studio
2. WCSS (Elbow method) was run to determine the optimal k
3. k = 7 was selected based on the elbow plot
4. Clusters were created and named via LLaMA (`meta-llama/Meta-Llama-3-8B-Instruct`)
5. The clustered CSV was exported → `tips_clustered.csv`
6. The cluster summary table was saved → `conclusions.csv`

---

## Notes

- The Tips dataset originates from Bryant & Smith (1995) and is widely used in data visualization and statistics education.
- The dominant segmentation axis found by the model is **day + gender + meal time**, reflecting the strongest statistical patterns in the data.
- Clusters 4 and 6 both received the name "Female Lunchtime Diners" — they represent two distinct sub-groups within the female lunch segment, differentiated by bill size and smoking habits.
- All 7 clusters were successfully named with no API errors.
