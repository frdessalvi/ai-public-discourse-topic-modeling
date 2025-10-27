# Investigating Public Concerns about AI  
*A Comparative Topic Modeling Analysis of Tweets and News Articles*

Artificial Intelligence (AI) is rapidly transforming social, economic, and technological domains. Public discourse reflects both optimism about its potential and persistent anxieties about its risks. Understanding these concerns is crucial for anticipating societal responses, guiding policy, and countering misinformation.

This project analyzes how public concerns about Artificial Intelligence (AI) are expressed across **social** and **traditional** media, combining **sentiment classification** and **topic modeling**. It was developed as the final project of a *Language Technology  (NLP)* course.

---

## Dataset Overview

| Source | Size / Period | Description |
|---------|---------------|-------------|
| **Tweets (X)** | ~20,000 English tweets (Jul 2023–Nov 2024) | Filtered for AI-related terms, manually annotated for sentiment. |
| **News Articles** | 500 English articles (Jun 2023–Dec 2024) | Retrieved from LexisNexis; manually extracted concern-focused sentences. |

> Due to licensing and privacy constraints, datasets are not included in this repository. Scripts and configs can reproduce the pipeline on equivalent data.

---

## Methodology

### 1. Sentiment Classification

We fine-tuned a `Twitter-RoBERTa-base` model on **2 000 manually annotated tweets** to classify overall sentiment toward AI as **negative**, **neutral**, or **positive**.  

| Model | Accuracy | Macro-avg F1 | Notes |
|--------|-----------|--------------|-------|
| Baseline (LogReg + TF-IDF) | 0.651 | 0.642 | Simple linear baseline |
| DistilBERT | 0.654 | 0.631 | Lightweight transformer |
| **Twitter-RoBERTa-base** | **0.698** | **0.694** | Best performance |

> `Twitter-RoBERTa-base` achieved the highest accuracy and macro-F1, confirming the value of pre-training on Twitter data for this domain.

Tweets predicted as *negative* were retained for subsequent topic modeling.

---

### 2. Text Preprocessing
- Lowercasing, punctuation & stopword removal  
- Lemmatization (SpaCy)  
- POS filtering (nouns, verbs, adjectives, adverbs)  
- Bigram extraction using NPMI > 0.5  
- TF-IDF representation for `NMF` and `SVD`; BoW for `LDA`

---

### 3. Topic Modeling
We applied **LDA**, **NMF**, and **SVD** on both corpora (tweets and news) and compared models using a combined coherence metric  
`Score = 0.75 × Cv + 0.25 × UMass`.

| Model | Tweets (Cv norm) | News (Cv norm) |
|--------|------------------|----------------|
| LDA | 0.25 | 0.52 |
| **NMF** | **1.00** | **0.99** |
| SVD | 0.13 | 0.25 |

A one-sided Wilcoxon signed-rank test confirmed the **superiority of NMF** (*p* < 1 × 10⁻⁴).  
After manual refinement of topic labels, coherence further improved:  
- Tweets : 0.60 → 0.82  
- News : 0.49 → 0.75

---

## Results and Key Findings

| Medium | Dominant Themes | Interpretation |
|---------|----------------|----------------|
| **Tweets** | Bots & automation, AI in war, Deepfakes, Existential risk, Thinking & education | Emotionally charged, speculative, platform-driven fears |
| **News** | Job automation, Algorithmic bias, Privacy, Scams, Ethical & institutional risks | Analytical framing, policy-oriented concerns |

> **Insight:** Social media emphasizes *emotional & speculative* risks, while journalism stresses *institutional & ethical* risks—revealing how communication norms shape AI narratives.

---

## Limitations and Future Work

- **Dataset coverage:** Public Kaggle and LexisNexis subsets may not reflect the full diversity of opinions.  
- **Lack of demographics:** User- or publication-level context not available.  
- **Manual refinement:** Human labeling of topics can be subjective.

**Future extensions**
- Broaden media sources and time frames  
- Track temporal shifts in AI discourse  
- Integrate conversation-level structures for tweets

---

## References
- Twitter-RoBERTa-base model — *Hugging Face Transformers*  
- LDA, NMF, SVD implementations — *scikit-learn* / *gensim*  
- Datasets — *Kaggle (tweets)*, *LexisNexis (news)*  

---

*Authors:* Elisa Degara · Francesca Dessalvi · Clara Montemurro · Tommaso Giacomello  
*Course:* Language Technology, 2025 – Bocconi University





