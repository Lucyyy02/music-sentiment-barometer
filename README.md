# Music as a Sentiment Barometer

> Analysing 66 years of Billboard Hot 100 audio features against US economic indicators to test whether music reflects how the economy *feels* rather than how it *is.*

---

## Live Dashboard

**[View Interactive Dashboard](https://Lucyyy02.github.io/music-sentiment-barometer/music_sentiment_dashboard.html)**

Select any date range from 1958 to 2024 to explore the economic conditions and sonic fingerprint of that era, alongside the top charting songs of the period.

---

## Hero Chart

![Hero Chart](<img width="2385" height="1621" alt="hero_chart" src="https://github.com/user-attachments/assets/4a404ef1-d2be-40fb-89cf-2ad933691b21" />)

*60-year timeline of average Billboard Hot 100 valence (musical happiness), Okun Misery Index, and Michigan Consumer Sentiment — with NBER recession bands shaded.*

---

## Research Question

Prior research (Larson, 2022) established that the Okun Misery Index — a hard economic indicator — correlates with shifts in the audio features of popular music. This project extends that work by introducing **Michigan Consumer Sentiment** as a competing predictor, asking:

> Does music better reflect *what the economy is* (Misery Index) or *how people feel about it* (Consumer Sentiment)?

---

## Key Findings

- **The Misery Index drives the emotional character of music.** Loudness (R²=0.253), valence (R²=0.249), and speechiness (R²=0.248) are the three strongest associations in the dataset — all dominated by the Misery Index. During economic hardship, Americans gravitate toward happier, quieter, and less vocal-heavy music.

- **Michigan Sentiment drives the rhythmic and energetic character of music.** Tempo (R²=0.109), instrumentalness (R²=0.107), and energy (R²=0.034) respond more strongly to perceived economic conditions than to hard data. When consumer confidence falls, music slows down and loses energy.

- **Neither indicator alone tells the full story.** The combined model consistently outperforms either predictor alone, confirming the two indicators capture independent, additive information.

- **Tempo shows a 5-month lag tied to sentiment.** Lag analysis found that Michigan Sentiment shifts show up in the pace of charting music approximately 5 months later — consistent with the music production timeline and the strongest directional evidence in the analysis.

- **Danceability does not support the simple recession pop narrative** at the monthly average level, suggesting the relationship is non-linear or genre-specific.

---

## Data Sources

| Source | What | Coverage |
|---|---|---|
| [HipsterVizNinja GitHub](https://github.com/HipsterVizNinja/random-data/tree/main/Music/hot-100) | Billboard Hot 100 chart positions | 1958–present |
| [TidyTuesday / R4DS](https://github.com/rfordatascience/tidytuesday/tree/master/data/2021/2021-09-14) | Spotify audio features (pre-scraped) | 1958–2021 |
| [FRED — St. Louis Fed](https://fred.stlouisfed.org/) | Unemployment, CPI, GDP, Michigan Sentiment, Recession indicator | 1958–2024 |

---

## Methodology

Four models were estimated across 10 Spotify audio features:

| Model | Description |
|---|---|
| **A — Larson Replication** | OLS: audio feature ~ Misery Index |
| **B — Sentiment Model** | OLS: audio feature ~ Michigan Sentiment |
| **C — Horse Race** | OLS: audio feature ~ Misery Index + Michigan Sentiment |
| **D — Lag Analysis** | Cross-correlation at 1–12 month lags |

Ridge regression (RidgeCV, 5-fold) was run as a robustness check to account for multicollinearity between the two predictors. Agreement rate between OLS and Ridge was 60%, with the three most reliable findings (loudness, valence, speechiness) confirmed by both methods.

---

## Project Structure

```
music-sentiment-barometer/
├── 01_data_collection.ipynb       # Data pull and merging
├── 02_eda_visualization.ipynb     # EDA and hero chart
├── 03_regression_models.ipynb     # OLS, Ridge, lag analysis
├── 04_results_writeup.ipynb       # Write-up and dashboard build
├── music_sentiment_dashboard.html # Interactive dashboard
├── hero_chart.png                 # Hero visualisation
└── README.md
```

---

## Tech Stack

`Python` `pandas` `NumPy` `statsmodels` `scikit-learn` `matplotlib` `seaborn` `Plotly` `FRED API` `Google Colab`

---

## References

- Larson, L.A. (2022). *The Lure of Musical Comfort*. CMC Senior Theses, 3076.
- Karthikeyan, A. (2024). *How Music Reflects Perception of the Economy*. Georgia Tech Equilibrium.
- Castro, V. (2026). *Brat Recession: Hyperpop, EDM, and Financial Crises*. St Andrews Economist.
