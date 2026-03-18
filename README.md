# 🎥 Semantic-Emotional Hybrid Video Ranking System

## 📌 Overview

With the rapid growth of educational content on platforms like YouTube, identifying high-quality learning resources has become increasingly challenging. Traditional ranking methods rely heavily on surface-level metrics such as views, likes, and comment counts, which often fail to reflect the **true instructional quality** of a video.

This project proposes a **Hybrid Video Ranking System** that integrates:

* 📊 Engagement Signals (likes, comments, sentiment)
* 🧠 Semantic Relevance (transformer-based embeddings)
* 🎓 Intrinsic Teaching Quality (ITQS)

The system ranks videos based on a **balanced combination of audience engagement and educational value**, enabling more meaningful content discovery.

---

## 🚀 Key Features

* 🔍 **Semantic Filtering** using transformer embeddings (E5 model)
* 💬 **Sentiment Analysis** using RoBERTa-based model
* 📈 **Emotional Engagement Modeling**
* 🎓 **Intrinsic Teaching Quality Score (ITQS)**
* ⚖️ **Adaptive Hybrid Ranking**
* 📊 **Baseline Comparison (Views, Likes, Comments)**
* 🧪 **Ablation Study & Sensitivity Analysis**
* 📉 **Statistical Validation (Spearman Correlation, p-values)**

---

## 🏗️ System Architecture

```
YouTube API
     ↓
Data Collection (Videos + Comments)
     ↓
Text Cleaning & Preprocessing
     ↓
Semantic Relevance Filtering (Embeddings)
     ↓
Sentiment Analysis
     ↓
Emotional Engagement Modeling
     ↓
Intrinsic Teaching Quality (ITQS)
     ↓
Hybrid Ranking Model
     ↓
Evaluation & Analysis
```

---

## ⚙️ Methodology

### 🔹 Phase 1: Data Collection

* Used YouTube Data API
* Collected:

  * Video metadata (views, likes, duration)
  * User comments

---

### 🔹 Phase 2: Text Preprocessing

* Lowercasing
* Removing URLs & special characters
* Token normalization

---

### 🔹 Phase 3: Semantic Relevance Filtering

* Model: `intfloat/e5-base-v2`
* Converts text into embeddings
* Computes similarity with query:

```
"Complete Python programming tutorial explaining concepts and problem solving"
```

* Top-K relevant comments selected

---

### 🔹 Phase 4: Sentiment Analysis

* Model: `cardiffnlp/twitter-roberta-base-sentiment-latest`
* Output mapped to:

  * Positive → +score
  * Negative → -score
  * Neutral → 0

---

### 🔹 Phase 5: Emotional Engagement

[
EmotionScore = Relevance × Sentiment
]

Aggregated per video:

* Mean → Emotional Engagement
* Variance → Stability
* Count → Discussion Volume

---

### 🔹 Phase 6: Engagement Score (ES)

[
ES = 0.4E + 0.2(1 - Var) + 0.2Likes + 0.2Comments
]

---

### 🔹 Phase 7: Intrinsic Teaching Quality Score (ITQS)

Based on:

* Semantic Alignment
* Depth (duration)
* Lexical Diversity
* Teaching Score

[
ITQS = 0.3SA + 0.2Depth + 0.2LexDiv + 0.3Teaching
]

---

### 🔹 Phase 8: Hybrid Ranking Model

[
Hybrid = \alpha \cdot ES + (1-\alpha) \cdot ITQS
]

Where:

[
\alpha = \frac{\log(1+RC)}{\log(1+RC) + k}
]

* (RC): Relevant Comment Count
* (k = 5): smoothing parameter

---

## 📊 Evaluation

### 🔹 Baseline Models

* Views-based ranking
* Likes-based ranking
* Comment-based ranking

---

### 🔹 Ablation Study

Compared:

* Baselines vs Hybrid model

Key Insight:

> Hybrid ranking differs from simple popularity metrics and promotes high-quality educational videos.

---

### 🔹 Sensitivity Analysis

* Tested different values of (k)
* Result:

  * Stable rankings for (k ≥ 3)
  * Optimal choice: **k = 5**

---

### 🔹 Statistical Validation

* Spearman Correlation
* p-value significance testing

Example:

* ES vs Hybrid → Moderate correlation
* ITQS vs Hybrid → Strong correlation
* ES vs ITQS → Independent signals

---

### 🔹 Top-K Overlap

| Metric   | Overlap with Hybrid |
| -------- | ------------------- |
| Views    | 4                   |
| Likes    | 4                   |
| Comments | 0                   |

Insight:

> Comment count alone is not a reliable indicator of teaching quality.

---

### 🔹 NDCG@K Evaluation

Evaluates ranking quality based on relevance (ITQS).

Result:

> Hybrid model ranks high-quality videos more effectively than baselines.

---

## 📈 Results

* Hybrid model balances:

  * Engagement
  * Teaching quality
* Successfully promotes:

  * High-quality but less popular videos
* Filters:

  * Noisy engagement (e.g., high comments without value)

---

## 🧠 Key Insights

* Popularity ≠ Educational Quality
* Engagement and teaching quality are independent signals
* Hybrid ranking improves content discovery
* Model is robust and stable across parameter variations

---

## 🛠️ Technologies Used

* Python 🐍
* Pandas & NumPy
* Scikit-learn
* Sentence Transformers
* HuggingFace Transformers
* YouTube Data API
* Matplotlib & Seaborn

---

## 📂 Project Structure

```
├── data/
├── notebooks/
├── youtube_videos.csv
├── youtube_comments.csv
├── cleaned_data.csv
├── phase_outputs/
├── README.md
```

---

## 🔮 Future Work

* Incorporate video transcripts
* Use real user feedback for evaluation
* Deploy as recommendation system
* Fine-tune LLM for teaching quality scoring

---

## 👨‍💻 Author

**Nayanesh Chennareddy**
B.Tech CSE – Amrita Vishwa Vidyapeetham
Focus: AI, NLP, Computer Vision

---

## ⭐ Conclusion

This project demonstrates a **multi-stage hybrid ranking framework** that integrates semantic understanding, emotional analysis, and intrinsic teaching quality to improve educational video ranking beyond traditional popularity-based methods.

---
