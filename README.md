# TripAdvisor Recommendation System

A content-based recommendation system that suggests similar travel experiences (hotels, restaurants, attractions) using **only user reviews** — no metadata used as input.

> **Hypothesis**: similar experiences are described in similar ways by users. Reviews alone contain enough signal to recommend comparable places.

---

## Methodology

### Data Preparation
- **Language filtering**: English reviews only (`langue == 'en'`)
- **Aggregation**: up to 50 reviews per place to reduce size discrepancy
- **Preprocessing**: lowercase conversion, punctuation removal
- **Train/test split**: 50% query / 50% index (random split by place)

> All metadata was strictly reserved for evaluation and never used as model input.

### Models

| Model | Description |
|---|---|
| **BM25** (baseline) | Classical probabilistic ranking function |
| **TF-IDF + Cosine Similarity** (improved) | Weighted term frequency, ignores stop words |

### Evaluation — Ranking Error Metric

Returns the position `(n-1)` of the first similar place found:

- **Level 1**: same category (Hotel, Restaurant, Attraction, Attraction Product)
- **Level 2**: same sub-category (cuisine type, price range, attraction sub-type — at least one match)

*Lower is better.*

## Results

| Model | Mean Ranking Error L1 | Mean Ranking Error L2 |
|---|---|---|
| BM25 (baseline) | 0.6947 | 6.3961 |
| TF-IDF (improved) | 0.8779 | 6.3575 |

TF-IDF performs slightly better at the fine-grained level (L2), suggesting it captures more specific vocabulary. BM25 achieves a lower L1 error, indicating it is more reliable at retrieving the correct general category.

## Authors

Gabriel Matar & Octave Pedergnana — March 2026
