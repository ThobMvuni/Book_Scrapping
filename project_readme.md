# Book Price Analytics & Predictive Modeling

An end-to-end data science pipeline evaluating whether book metadata (star ratings, title length, word count) can predict listing prices on the demonstration website [Books to Scrape](https://books.toscrape.com). 

This repository covers the complete workflow from automated web scraping and data cleaning to exploratory data analysis (EDA) and linear regression modeling.

---

## 📌 Project Overview & Key Findings

- **Dataset Size:** 1,000 scraped book titles across 50 catalog pages.
- **Key EDA Insight:** Listing prices span from **£10.00 to £59.99**, with a mean price of **£35.07** ($\sigma = £14.45$) and a median of **£35.98**. Listed star ratings show a negligible linear correlation ($r = +0.0282$) with price.
- **Model Result:** A Multiple Linear Regression model achieved a test MAE of **£12.69** ($R^2 = -0.0113$), performing slightly below a baseline model predicting the training-set mean price (Test MAE of **£12.66**).
- **Dataset Caution:** *Books to Scrape* is a synthetic demonstration platform with randomly generated prices and ratings. This project serves as a showcase of a reproducible data science methodology rather than commercial pricing intelligence.

---

## 🛠️ Repository Structure

```text
├── data/
│   └── books_scraped_clean.csv   # Cleaned dataset (1,000 rows)
├── notebooks/
│   └── book_price_analysis.ipynb # Full analysis, scraping & modeling notebook
├── reports/
│   └── book_price_analysis_report.pdf # Standalone evaluation report
├── requirements.txt              # Python dependency file
└── README.md                     # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook or JupyterLab

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/book-price-analytics.git
   cd book-price-analytics
   ```

2. **Create and activate a virtual environment (optional but recommended):**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

---

## ⚙️ Workflow Steps

### 1. Data Acquisition & Scraping
The collection script parses catalog pagination using `requests` and `BeautifulSoup`, extracting:
- Product Title & Detail Link
- Raw Price (`£XX.XX`)
- Textual Star Rating (`One` through `Five`)
- Availability Status

### 2. Data Cleaning & Feature Engineering
- Converts price strings to floating-point numeric values (`float`).
- Maps textual ratings to integer values ($1$ to $5$).
- Derives title length metrics: `title_length` (character count) and `word_count`.
- Verifies zero null values and checks for duplicate entries.

### 3. Exploratory Data Analysis
Generates visual representations of:
- Price distribution across the entire dataset (histogram & KDE).
- Group metric spreads across star rating tiers (boxplot).
- Actual vs. predicted model outputs.

### 4. Predictive Modeling
- Splits data into 800 training and 200 testing records (`random_state=42`).
- Pipeline includes median imputation fitted strictly on training data.
- Fits a `LinearRegression` model using `rating`, `title_length`, and `word_count`.
- Compares results against a dummy mean-price baseline model.

---

## 📊 Summary of Model Performance

| Model Variant | Test MAE (£) | Test RMSE (£) | Test $R^2$ |
| :--- | :---: | :---: | :---: |
| **Mean-Price Baseline** | £12.66 | £14.53 | -0.0051 |
| **Multiple Linear Regression** | £12.69 | £14.58 | -0.0113 |

---

## 💡 Future Recommendations

1. **Extend Web Scraper:** Crawl individual product detail pages to extract book categories (genres) and numerical stock quantities.
2. **Implement Cross-Validation:** Utilize $K$-fold cross-validation on the training set to evaluate stability across samples.
3. **Collect Real-Market Data:** Apply the pipeline to real-world book API endpoints (e.g., Google Books API, Open Library) for commercial pricing models.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.