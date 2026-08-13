# Ixigo Customer Sentiment Analysis Using NLP

A text analytics project analysing **9,609 Google Play reviews of the Ixigo travel application** to identify dominant customer sentiment, recurring complaints, and actionable product and business insights.

The project was developed as part of the **EM5033: Text Analytics for Business** course using **Python for data extraction and Orange Data Mining for NLP and sentiment analysis**.

---

## Project Overview

Travel platforms receive large volumes of unstructured customer feedback covering bookings, payments, refunds, pricing, customer support, and technical issues.

The objective of this project was to move beyond numerical star ratings and analyse the **actual language used by customers** to identify recurring pain points and their potential implications for customer retention and business performance.

The analysis covers:

* Text preprocessing
* Tokenization and stop-word removal
* Lemmatization/stemming
* Bag-of-Words representation
* Sentiment scoring
* Rating–sentiment comparison
* Word-frequency analysis
* Complaint-theme identification
* Business interpretation and recommendations

---

## Dataset

The dataset contains **9,609 Google Play reviews** of the Ixigo application spanning **2011 to March 2026**, with 15 variables including review text, star ratings, thumbs-up counts, developer responses, and app-version information.

### Dataset Summary

| Attribute          |                 Value |
| ------------------ | --------------------: |
| Reviews            |             **9,609** |
| Variables          |                **15** |
| Period             | **2011 – March 2026** |
| Primary text field |  `review_description` |
| Rating field       |              `rating` |
| Source             |           Google Play |

The dataset was extracted from Google Play using Python and subsequently analysed using Orange's Text Mining workflow.

# Technologies Used

* **Python** — Data extraction
* **Orange Data Mining** — NLP and sentiment analysis
* **Orange Text Mining Add-on**
* **VADER sentiment analysis**
* **Bag-of-Words**
* **Word Clouds**
* **Exploratory Text Analysis**

---

# Limitations

* Google Play reviews are **self-selected user feedback** and may overrepresent dissatisfied users.
* Lexicon-based sentiment analysis may struggle with sarcasm, context, mixed sentiment, and domain-specific language.
* Keyword frequency does not establish causality.
* Business impacts such as churn, CAC, or LTV were interpreted conceptually rather than estimated directly from transactional data.
* The findings should therefore be treated as **exploratory customer-feedback insights**, not causal estimates.

---

## Disclaimer

This is a coursework project developed using **multiple public sources, prior similar NLP approaches, and AI-assisted tools** during research, implementation, debugging, and documentation. It should not be considered original research or independently validated; refer to the cited sources for further verification.

---

## References

* Google Play — Ixigo application reviews
* Orange Data Mining
* Python extraction code provided through coursework
* Additional NLP/sentiment-analysis references listed in the accompanying report

