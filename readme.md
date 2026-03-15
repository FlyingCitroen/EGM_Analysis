# 📂 Dataset: 1990s Gaming Media Quantitative Analysis

This directory contains the primary datasets used for the quantitative research of gaming industry trends in the 1990s. The data was extracted from historical archives of *Electronic Gaming Monthly (EGM)*.

## 📊 Data Inventory & Metadata

### 1. Editorials Dataset (`editorials.csv`)
This dataset captures editorial content, primarily used for **NLP (Natural Language Processing)** and **Temporal Sentiment Analysis**.

| Column | Description | Technical Note |
|:---|:---|:---|
| `id` | Unique entry identifier | Primary Key |
| `topic` | Subject of the editorial | Categorical (Nullable) |
| `content` | Full-text body of the editorial | Source for Text Mining |
| `year` | Publication year (1990-1999) | Temporal Feature |
| `month` | Publication month (1-12) | Temporal Feature |
| `tokens` | Pre-processed word tokens | List[String] (Stop-words removed) |
| `year_month` | Combined temporal key (e.g., `1994-05`) | Unique key for Time-Series Viz |

### 2. Reviews Dataset (`reviews.csv`)
A structured dataset representing game evaluation metrics and platform distribution.

| Column | Description | Technical Note |
|:---|:---|:---|
| `issue` | Magazine issue number | Integer |
| `game` | Title of the video game | String (Normalized) |
| `platform` | Target hardware (e.g., PS1, Genesis) | Categorical Feature |
| `reviewer` | Raw string of reviewer names & scores | Unstructured Object |
| `year` | Publication year | Temporal Feature |
| `month` | Publication month | Temporal Feature |
| `average_score`| Calculated arithmetic mean of scores | Float (Target Variable) |
| `scores` | Extracted numerical score list | List[Integer] (Regex extracted) |

---

## 🛠️ Data Engineering Pipeline

To prepare these datasets for analysis, the following **ETL (Extract, Transform, Load)** steps were implemented:

1. **Information Extraction**: Used Python to digitize archival text into structured CSV formats.
2. **Text Normalization (NLP)**: 
   - Tokenized the `content` into the `tokens` column.
   - Applied lowercasing and punctuation removal to ensure consistency for frequency analysis.
3. **Regex-based Feature Extraction**: 
   - The `scores` column was derived from the raw `reviewer` string using **Regular Expressions (Regex)** to isolate numerical values from text.
   - Calculated `average_score` to enable cross-platform performance benchmarking.
4. **Time-Series Preparation**: 
   - Engineered the `year_month` feature to allow for granular monthly trend plotting, avoiding overlapping data points in visualizations.

---

## 📈 Analysis Potential

- **Sentiment Tracking**: Analyzing the `editorials` dataset to quantify industry optimism regarding 3D technology and internet integration.
- **Platform Performance**: Comparing `average_score` across different `platforms` to visualize the market dominance of hardware manufacturers.
- **Keyword Correlation**: Mapping the frequency of specific "tokens" (e.g., *Multi-player*, *Online*) against the timeline to identify market shifts.
