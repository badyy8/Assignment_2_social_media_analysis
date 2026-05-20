# Text Analysis Component — Word Frequency and Topic Modelling

## Assignment Context

This README documents the **text analysis component** completed for Assignment 2 of Social Media and Network Analysis.  
This section focuses only on the individual contribution covering:

- Word frequency analysis
- Bigram frequency analysis
- Topic modelling using TF-IDF and NMF
- Exported tables and figures for the final report

The dataset used for this component is the cleaned Bitcoin tweet dataset.

---

## Files Related to This Component

| File / Folder | Description |
|---|---|
| `03_word_frequency_topic_modelling.ipynb` | Notebook used for word frequency and bigram frequency analysis. |
| `04_topic_modelling.ipynb` | Notebook used for TF-IDF vectorisation and NMF topic modelling. |
| `data/bitcoin_tweet.parquet` | Cleaned Bitcoin tweet dataset used for the analysis. This file is not uploaded to GitHub due to file size limits. |
| `outputs_text_analysis/` | Folder containing exported charts and tables from the text analysis. |

---

## Dataset Note

The dataset file is not included in the GitHub repository because it is large.  
To run the notebooks, place the dataset in the following path:

```text
data/bitcoin_tweet.parquet
```

Expected project structure:

```text
Assignment_2_social_media_analysis/
│
├── 03_word_frequency_topic_modelling.ipynb
├── 04_topic_modelling.ipynb
│
├── data/
│   └── bitcoin_tweet.parquet
│
└── outputs_text_analysis/
```

The loaded dataset used in this component had:

```text
Rows: 632,179
Columns: 13
Text column used: text
```

---

## Python Environment

The analysis was run using Python in VS Code with a virtual environment.

Required packages:

```bash
python -m pip install pandas numpy matplotlib scikit-learn pyarrow notebook ipykernel
```

Main libraries used:

```python
pandas
matplotlib
scikit-learn
pyarrow
re
pathlib
```

---

## Notebook 1: Word Frequency and Bigram Analysis

### Purpose

The purpose of the word frequency section was to identify the most common meaningful terms and phrases in the cleaned Bitcoin tweet dataset.

### Cleaning Steps

The text was cleaned by removing:

- URLs
- Twitter mentions
- Hashtag symbols
- Numbers and special characters
- Common English stopwords
- Very short words
- Repeated domain terms such as `bitcoin`, `btc`, `crypto`, and `cryptocurrency`
- Generic low-value terms such as `just`, `like`, `time`, `people`, `think`, and `know`
- Spam or promotional terms found during output checking, such as `cashback`, `betfurysuccess`, `seasonaltokens`, and `cryptomining`

This cleaning was important because the first output contained generic or spam-like words that did not support strong analysis. The final cleaned version produced more meaningful results suitable for interpretation.

### Final Word Frequency Output

The final word frequency analysis identified common terms such as:

```text
buy, eth, market, money, price, project, ethereum, future, value, sell, gold, fiat, bullish, blockchain, dip
```

These terms suggest that Bitcoin-related discussion was strongly connected to:

- Buying and selling
- Market behaviour
- Price movement
- Investment value
- Alternative assets such as gold and fiat currency
- Blockchain and crypto projects

### Final Bigram Frequency Output

The final bigram analysis produced meaningful two-word phrases such as:

```text
bear market
long term
bull run
buy dip
store value
market cap
short term
bull market
legal tender
current price
stock market
price action
proof work
real estate
lightning network
self custody
cold storage
satoshi nakamoto
fiat money
```

These bigrams were useful because they provided stronger context than single words. They showed that the Bitcoin conversation was mainly shaped by:

- Market cycles
- Trading behaviour
- Long-term investment thinking
- Bitcoin as a store of value
- Bitcoin technology and custody practices
- Traditional finance comparisons

### Exported Outputs

The following outputs were saved in `outputs_text_analysis/`:

```text
top_30_words_hd.csv
top_30_words_hd.png
top_30_bigrams_hd.csv
top_30_bigrams_hd.png
```

---

## Notebook 2: Topic Modelling

### Purpose

The purpose of topic modelling was to identify major discussion themes in the Bitcoin tweet dataset.  
This goes beyond simple word frequency because it groups tweets into broader topics based on patterns in the text.

### Sampling

The full cleaned dataset was large, so a reproducible sample was used for topic modelling:

```text
Sample size: 200,000 tweets
Random state: 42
```

A fixed random seed was used so the results can be reproduced consistently.

### Method Used

Topic modelling was completed using:

```text
TF-IDF Vectorisation + Non-Negative Matrix Factorisation (NMF)
```

TF-IDF was used because it gives more importance to distinctive terms and reduces the effect of overly common words.

NMF was used because it produces interpretable topic groups for short social media text such as tweets.

### TF-IDF Settings

```python
TfidfVectorizer(
    stop_words=list(stopwords_hd),
    max_df=0.90,
    min_df=10,
    max_features=8000,
    ngram_range=(1, 2)
)
```

### Topic Model Settings

```python
NMF(
    n_components=5,
    random_state=42,
    init="nndsvda",
    max_iter=400
)
```

Five topics were selected because they provided a clear and interpretable structure for the report without making the topic model too broad or too fragmented.

---

## Final Topic Model Results

The topic model identified five major topics.

| Topic | Topic Label | Tweet Count | Percentage |
|---:|---|---:|---:|
| 0 | Buying, selling and trading behaviour | 13,410 | 6.70% |
| 1 | Bitcoin as money and store of value | 139,591 | 69.80% |
| 2 | Crypto projects and future expectations | 15,647 | 7.82% |
| 3 | Ethereum and altcoin discussion | 17,885 | 8.94% |
| 4 | Market cycles and price movement | 13,467 | 6.73% |

---

## Topic Labels and Supporting Terms

### Topic 0 — Buying, selling and trading behaviour

Top terms included:

```text
buy, dip, sell, buy dip, hodl, hold, buy hold
```

This topic represents tweets focused on trading decisions, buying dips, selling, and holding behaviour.

### Topic 1 — Bitcoin as money and store of value

Top terms included:

```text
money, price, buying, long, world, gold, value, fiat, inflation
```

This was the dominant topic, representing 69.80% of the sampled tweets. It suggests that most discussion framed Bitcoin as money, a store of value, or an alternative to traditional financial systems.

### Topic 2 — Crypto projects and future expectations

Top terms included:

```text
project, future, team, bsc, bnb, hope, strong, success, blockchain, support
```

This topic captures discussion about crypto projects, project teams, future expectations, and community optimism.

### Topic 3 — Ethereum and altcoin discussion

Top terms included:

```text
eth, ethereum, bnb, doge, ada, xrp, sol, nft, shib
```

This topic shows that although the dataset is Bitcoin-focused, users also discussed Ethereum and other altcoins.

### Topic 4 — Market cycles and price movement

Top terms included:

```text
market, bear, bear market, bull, bull market, cap, bull run, stock market
```

This topic represents discussion about market cycles, price movement, bullish/bearish sentiment, and comparison with stock markets.

---

## Key Findings from My Text Analysis Component

The word frequency and bigram analysis showed that Bitcoin tweets were strongly focused on investment-related language, especially buying, selling, price movement, market cycles, and long-term value.

The topic modelling results provided deeper evidence by grouping the tweets into five main themes. The dominant topic was **Bitcoin as money and store of value**, which represented **69.80%** of the sampled tweets. This suggests that the dataset is not only focused on short-term trading. Instead, a large part of the discussion frames Bitcoin as a monetary asset, store of value, or alternative to fiat currency and traditional finance.

The smaller topics showed additional discussion around trading behaviour, market cycles, crypto projects, and Ethereum/altcoin comparisons. Together, these findings support the broader assignment by showing the main themes in the social media discussion before these themes are connected with sentiment and network analysis.

---

## Report Figures and Tables to Use

Recommended outputs for the final report:

| Output | Purpose |
|---|---|
| `top_30_words_hd.png` | Shows the most common meaningful single-word terms. |
| `top_30_bigrams_hd.png` | Shows the most common meaningful two-word phrases. |
| `final_topic_terms_hd.csv` | Shows topic labels and top words. |
| `final_topic_summary_hd.csv` | Shows topic counts and percentages. |
| `topic_distribution_hd_final.png` | Visualises the distribution of dominant topics. |
| `representative_tweets_short_hd.csv` | Provides example tweets for topic validation. |

---

## Suggested Run Order

Run the notebooks in this order:

```text
1. 03_word_frequency_topic_modelling.ipynb
2. 04_topic_modelling.ipynb
```

Before running, confirm that the dataset is available at:

```text
data/bitcoin_tweet.parquet
```

---

## GitHub Note

The dataset file should not be pushed to GitHub because it is large.  
The `.gitignore` file should include:

```text
data/
*.parquet
```

The output folder can be included if the group wants markers to view generated charts and CSV outputs directly. If output files are too large, only selected report-ready figures and tables should be included.

---

## Current Status

Completed:

- Dataset loaded successfully
- HD-level text cleaning completed
- Word frequency analysis completed
- Bigram frequency analysis completed
- TF-IDF vectorisation completed
- NMF topic modelling completed
- Topic labels created
- Topic distribution calculated
- Representative tweets generated
- Final tables and charts exported

Pending:

- Add selected charts/tables into final report
- Connect text analysis findings with sentiment and network analysis
- Finalise written discussion for the report
