# Enterprise Tone-Scorer & Consistency Tracker

## Overview
A production-ready Natural Language Processing pipeline designed to analyze professional communications, detect nuanced emotional tones, and track communication consistency over time. 

Evolving beyond foundational algorithms like TF-IDF or simple keyword-matching, this project utilizes a Transformer-based model (Sentence Transformers) to evaluate the deep semantic context of live data. It features a secure IMAP integration to fetch and process live emails, alongside automated Seaborn visual analytics to track professionalism.

## 🚀 Key Features
* **Live IMAP Data Ingestion:** Securely connects to an email server to fetch, clean (HTML parsing via BeautifulSoup), and analyze live inbox data.
* **Semantic Vector Scoring:** Uses `all-MiniLM-L6-v2` to map text into vector space, calculating Cosine Similarity against professional anchors to bypass the "sarcasm loophole" of traditional models.
* **Baseline A/B Testing:** Automatically compares the Transformer's contextual understanding against a traditional Bag-of-Words baseline to mathematically prove model superiority.
* **Consistency Analytics:** Calculates the standard deviation of tone over time to evaluate whether a user maintains a steady, professional voice regardless of context.
* **Automated Visual Dashboards:** Uses Matplotlib and Seaborn to generate side-by-side grouped bar charts for instant stakeholder review.

## 🛠️ Technology Stack
* **Language:** Python
* **ML Architecture:** Hugging Face `sentence-transformers`, `scikit-learn`
* **Data & Viz:** Pandas, NumPy, Matplotlib, Seaborn
* **Data Extraction:** `imaplib`, `BeautifulSoup`

## 💻 Usage (Google Colab / Jupyter)
**Security Note:** Never hardcode your actual email password into this script. Generate a 16-digit App Password via your email provider's security settings.

```python
# 1. Initialize with secure credentials
MY_EMAIL = "your_email@gmail.com" 
MY_APP_PASSWORD = "your_16_digit_app_password" 

# 2. Fetch Live Data
fetcher = LiveEmailFetcher(MY_EMAIL, MY_APP_PASSWORD)
fetcher.connect()
live_emails = fetcher.fetch_recent_emails(limit=5)
fetcher.disconnect()

# 3. Analyze and Plot
scorer = EnterpriseToneScorer()
results_df = scorer.analyze_communications(live_emails)

scorer.plot_comparative_results(results_df)
