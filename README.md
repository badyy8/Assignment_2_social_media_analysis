# COSC 2671 / COSC 3047 — Assignment 2
## Bitcoin Twitter Discourse Analysis

**Dataset:** Bitcoin Tweets 2025–2026 (Kaggle) https://www.kaggle.com/datasets/pokeash/bitcoin-tweets-dataset-20252026
**Cleaned dataset size:** 632,179 tweets

---

## Repo Structure

| Notebook | Owner | Description |
|---|---|---|
| `data_cleaning.ipynb` | Batbilegt | Filtering pipeline |
| `01_data_network.ipynb` | Batbilegt | EDA, Network analysis |
| `02_sentiment.ipynb` | Jack | Sentiment analysis |
| `03_word_frequency_topic_modeling.ipynb` | Ashwin | Word & bigram frequency |
| `04_topic_modelling.ipynb` | Ashwin | TF-IDF + NMF topic modelling |

---

## Setup

```bash
pip install -r requirements.txt
```

Place the dataset at:

```text
data/bitcoin_tweet.parquet
```

*(Not included in repo since it's too large. Representative sample of the data will be included in the zipped file upon submission.)*

---

## Run Order

```text
01_data_network.ipynb
02_sentiment.ipynb
03_word_frequency_topic_modeling.ipynb
04_topic_modelling.ipynb
```

Notebooks all load from `data/bitcoin_tweet.parquet`.

---