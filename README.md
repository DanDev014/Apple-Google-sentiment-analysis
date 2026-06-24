# Apple-Google Twitter Sentiment Analysis

An end-to-end **Natural Language Processing (NLP)** pipeline for analyzing sentiment in Twitter posts related to **Apple** and **Google** products. This project applies text preprocessing, exploratory analysis, feature engineering, and machine learning to classify tweets as **positive** or **negative**, enabling automated brand sentiment monitoring.

---

## Project Overview

Social media platforms generate massive volumes of user-generated content every day, providing organizations with valuable insight into customer perception, product experience, and brand reputation.

Manually analyzing this data at scale is inefficient and unsustainable.

This project demonstrates how machine learning and NLP can automate sentiment classification to help organizations:

* Monitor brand perception in near real-time
* Detect customer dissatisfaction early
* Identify emerging product issues
* Support marketing and customer experience strategies

This project focuses on sentiment related to **Apple** and **Google** products using crowdsourced Twitter data.

---

## Business Problem

Organizations need an efficient way to understand customer sentiment at scale.

The challenge lies in the fact that Twitter data is:

* Unstructured
* Noisy
* Short-form
* Context-dependent

This project addresses that challenge by building a supervised NLP model capable of automatically classifying sentiment from tweets.

---

## Dataset

Dataset used:

**Judge Emotion About Brands and Products**

### Dataset Summary:

* **9,093 tweet records**
* Human-labeled sentiment annotations
* Real-world noisy text data
* Brand/product-specific sentiment

### Features:

| Feature                                              | Description          |
| ---------------------------------------------------- | -------------------- |
| `tweet_text`                                         | Raw tweet content    |
| `emotion_in_tweet_is_directed_at`                    | Brand/product target |
| `is_there_an_emotion_directed_at_a_brand_or_product` | Sentiment label      |

---

## Data Cleaning Pipeline

The preprocessing workflow includes:

* Removing missing tweet records
* Removing ambiguous labels (`I can't tell`)
* Standardizing sentiment labels
* Lowercasing text
* Removing URLs
* Removing user mentions
* Removing hashtags while preserving words
* Removing punctuation and non-alphabetic characters
* Stopword removal
* Preserving negation terms (`not`, `no`, `never`)
* Lemmatization using NLTK

Example:

**Before**

```text
@john I LOVE the new iPhone!! #Apple https://link.com
```

**After**

```text
love new iphone apple
```

---

## Exploratory Data Analysis (EDA)

EDA focused on:

### Sentiment distribution

* Identified class imbalance
* Neutral sentiment dominated

### Tweet length analysis

* Average tweet length: **11 words**

### Vocabulary analysis

* Unique vocabulary size: **9,329 words**

### Most frequent terms

Top terms included:

* sxsw
* apple
* google
* ipad
* iphone
* android

---

## Modeling Strategy

### Classification Approach

This project uses **binary classification**:

* Positive sentiment
* Negative sentiment

Neutral tweets were excluded to improve signal clarity.

---

## Feature Engineering

Text was transformed using:

### TF-IDF Vectorization

Configuration:

```python
ngram_range=(1,1)
max_features=5000
```

Why TF-IDF?

* Handles sparse text well
* Captures term importance
* Works efficiently on small-medium NLP datasets

---

## Models Evaluated

Three baseline models were trained:

### 1. Logistic Regression

Strong baseline for text classification.

---

### 2. Multinomial Naive Bayes

Fast and effective for bag-of-words models.

---

### 3. Linear Support Vector Classifier (LinearSVC)

Best overall performer.

---

## Model Performance

| Model                   | Accuracy | Negative Recall | Positive Recall |
| ----------------------- | -------- | --------------- | --------------- |
| Logistic Regression     | 85%      | 0.69            | 0.88            |
| Multinomial Naive Bayes | 85%      | 0.04            | 1.00            |
| LinearSVC               | **88%**  | **0.61**        | **0.93**        |

### Final Model Selected:

**LinearSVC**

Why?

* Highest overall accuracy
* Best F1-score
* Stronger balance between precision and recall

---

## Error Analysis

Common failure cases:

### False Positives

* Neutral tweets mistaken as positive
* Product announcements
* Comparisons without clear sentiment

### False Negatives

* Subtle positive sentiment
* Informal endorsements
* Short ambiguous phrases

Key finding:

The model performs best when sentiment is explicit.

---

## Feature Importance

Top positive indicators:

* cool
* free
* great
* awesome
* winning
* smart

Top negative indicators:

* fail
* hate
* crash
* faulty
* headache
* disappointment

This confirms the model learned meaningful sentiment patterns.

---

## Business Value

This model can support:

* Brand reputation monitoring
* Customer sentiment tracking
* Product feedback analysis
* Crisis detection
* Marketing intelligence

---

## Limitations

Current limitations include:

* Bag-of-words representation ignores context
* Struggles with sarcasm and irony
* Class imbalance remains a challenge
* Neutral sentiment excluded
* No metadata integration (emojis, engagement, timestamps)

---

## Future Improvements

Potential improvements:

* N-gram expansion
* Emoji sentiment handling
* Transformer-based models (BERT)
* Multi-class sentiment classification
* Cost-sensitive learning
* Human-in-the-loop review

---

## Tech Stack

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* NLTK
* Scikit-learn
* WordCloud

---

## Repository Structure

```bash
├── data/
│   └── judge-1377884607_tweet_product_company.csv
├── index.ipynb
├── README.md
├── requirements.txt
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/DanDev014/Apple-Google-sentiment-analysis.git
```

Move into the directory:

```bash
cd Apple-Google-sentiment-analysis
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run Jupyter Notebook:

```bash
jupyter notebook
```

---

## Author

**Daniel Njeru**
Data Scientist | NLP | Machine Learning | AI

---

**Built as an end-to-end NLP proof-of-concept for sentiment intelligence and brand monitoring.**

