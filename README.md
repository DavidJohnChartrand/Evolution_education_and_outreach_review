# Evolution: Education & Outreach — Literature Review

A data pipeline that scrapes, cleans, and prepares every peer-reviewed article published in the journal *[Evolution: Education and Outreach](https://evolution-outreach.biomedcentral.com/)* (2007–2023) for downstream text analysis.

## Project Goals

The journal *Evolution: Education and Outreach* (EEO) is the primary venue for science-communication research on evolutionary biology. This project builds a structured dataset of all 666 articles published since the journal's founding to answer questions such as:

- How has the volume and focus of evolution education research changed over time?
- Which content types (Research, Review, Curriculum, Book Review, etc.) dominate the literature?
- What topics and themes recur across articles?

## Dataset

| Field | Description |
|---|---|
| `Title` | Full article title |
| `Authors` | List of author names |
| `Content Type` | Article category (Research, Book Review, Letters, etc.) |
| `Published date` | Publication date |
| `Article text` | Full article body text |
| `Article link` | Absolute URL to the article page |

**666 articles** spanning **2007–2023**, scraped from the BioMed Central open-access platform.

## Repository Structure

```
├── Scraper.ipynb          # Web scraper — collects raw article data
├── Cleaning.ipynb         # Data cleaning pipeline
├── Analysis.ipynb         # EDA + BERTopic thematic clustering
├── EEO_articles.csv       # Raw scraped dataset
├── requirements.txt       # Python dependencies
└── .gitignore
```

## Setup

### Prerequisites

- Python 3.10+
- Google Chrome
- [ChromeDriver](https://chromedriver.chromium.org/downloads) matching your Chrome version, accessible on your `PATH`

### Install dependencies

```bash
pip install -r requirements.txt
```

## Usage

### 1. Scraping (`Scraper.ipynb`)

Launches a Chrome browser via Splinter and paginates through all article listings on the journal website, visiting each article page to collect the full text.

> The scraped data is already saved in `EEO_articles.csv`. Only re-run the scraper if you need to update the dataset with newer articles.

### 2. Cleaning (`Cleaning.ipynb`)

Parses the raw CSV into analysis-ready form:

- Converts the `Authors` field from a stringified list to a Python list
- Parses `Published date` to a proper datetime
- Joins and strips boilerplate from the `Article text` paragraph list
- Makes `Article link` an absolute URL
- Outputs `EEO_articles_clean.csv`

### 3. Analysis (`Analysis.ipynb`)

Exploratory data analysis followed by unsupervised thematic clustering:

- Publication volume by year, content type breakdown, most prolific authors
- Sentence-transformer embeddings (titles) + BERTopic clustering
- Interactive topic keyword chart, 2-D topic map, and topics-over-time visualization

## Built With

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-orange?style=for-the-badge&logo=Jupyter&logoColor=white)](https://jupyter.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-4-green?style=for-the-badge)](https://www.crummy.com/software/BeautifulSoup/)
[![BERTopic](https://img.shields.io/badge/BERTopic-topic%20modelling-blueviolet?style=for-the-badge)](https://maartengr.github.io/BERTopic/)

## Author

David Chartrand
