# Elasticsearch Precision-Recall Evaluation

This repository contains a complete pipeline to evaluate the performance of an Elasticsearch index using precision and recall metrics. The process involves cleaning raw data, indexing it into Elasticsearch, defining ground truth mappings, and computing precision and recall scores for search queries.

---

## Prerequisites

1. **Python**: Make sure Python 3.x is installed on your system.
2. **Elasticsearch**: Install and run an Elasticsearch server (locally or in the cloud).
3. **Dependencies**: Install the required Python libraries:
   ```bash
   pip install pandas elasticsearch
   ```

---

## Directory Structure

```
├── data_cleaning.py         # Script to clean and preprocess raw data
├── indexing.py              # Script to index data into Elasticsearch
├── ground_truth.py          # Script to create ground truth mapping
├── precision_recall.py      # Script to evaluate precision and recall
├── testing_sample_10000.csv # Example dataset (raw data)
```

---

## Step-by-Step Instructions

### 1. Data Cleaning

The raw dataset (`testing_sample_10000.csv`) contains duplicate entries that need to be removed.

- Run the `data_cleaning.py` script:
  ```bash
  python data_cleaning.py
  ```
- This script will:
  - Remove duplicates based on the `parent_asin` column.
  - Save the cleaned dataset as `testing_sample_10000_unique.csv`.
- Output:
  - `testing_sample_10000_unique.csv` (cleaned dataset ready for indexing).

---

### 2. Data Indexing in Elasticsearch

Prepare Elasticsearch to store and retrieve your dataset.

- Run the `indexing.py` script:
  ```bash
  python indexing.py
  ```
- This script will:
  - Create an Elasticsearch index with the name `products_index`.
  - Define index mappings to structure the data fields.
  - Index the cleaned data (`testing_sample_10000_unique.csv`) into Elasticsearch.
- Replace the `username` and `password` in the script with your Elasticsearch credentials if required.

---

### 3. Creating Ground Truth Mapping

Generate a mapping of search queries to relevant results (`parent_asin`) for evaluation purposes.

- Run the `ground_truth.py` script:
  ```bash
  python ground_truth.py
  ```
- This script will:
  - Group queries and their associated `parent_asin` values from the raw dataset.
  - Save the mapping as `ground_truth.json`.
- Output:
  - `ground_truth.json` (used for precision and recall evaluation).

---

### 4. Precision and Recall Evaluation

Evaluate Elasticsearch search results using precision and recall metrics.

- Run the `precision_recall.py` script:
  ```bash
  python precision_recall.py
  ```
- This script will:
  - Query Elasticsearch using the search queries from `ground_truth.json`.
  - Compute Precision@10 and Recall@10 for each query.
  - Display the metrics for each query and overall averages.
- Replace the `username` and `password` in the script with your Elasticsearch credentials if required.

---

## Outputs

1. **Data Cleaning**:
   - `testing_sample_10000_unique.csv`: Cleaned dataset without duplicates.
2. **Ground Truth Mapping**:
   - `ground_truth.json`: Query-to-relevant-results mapping for evaluation.
3. **Evaluation Metrics**:
   - Precision@10 and Recall@10 for each query, along with overall averages printed to the console.

---

## Notes

- Update the `index_name` variable in `indexing.py` and `precision_recall.py` if you are using a different Elasticsearch index name.
- Ensure Elasticsearch is running and accessible at `http://127.0.0.1:9200` or update the script URLs as necessary.
- Example dataset (`testing_sample_10000.csv`) should be placed in the same directory as the scripts.

---



