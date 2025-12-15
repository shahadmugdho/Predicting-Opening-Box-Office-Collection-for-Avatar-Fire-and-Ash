````markdown
# 🎬 Box Office Prediction: Avatar: Fire and Ash

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![CatBoost](https://img.shields.io/badge/CatBoost-Regressor-green)
![Optuna](https://img.shields.io/badge/Optuna-Hyperparameter%20Tuning-orange)
![API](https://img.shields.io/badge/TMDb-API-primary)

## 📌 Project Overview
This project builds a machine learning pipeline to predict the **First Week Box Office Income** of upcoming movies, with a specific focus on the highly anticipated **"Avatar: Fire and Ash" (2025)**.

The solution aggregates historical box office data, enriches it with movie metadata (budget, cast, director, genres) via the TMDb API, and trains a **CatBoostRegressor** model optimized with **Optuna**. It features advanced feature engineering, including a custom "Star Power" metric for actors and directors.

## 📂 Repository Structure

| File | Description |
| :--- | :--- |
| `boxoffice_data_.py` | **Scraper:** Collects daily box office data from *Box Office Mojo* for a specified year range. |
| `tmdb_movie_data_2009_2025.py` | **API Fetcher:** Queries the *TMDb API* to get detailed metadata (budget, runtime, genres, cast) for the scraped movies. |
| `merging1.py` | **Preprocessor:** Merges the box office and API datasets. Handles data cleaning, currency conversion, and feature engineering (calculating *Star Power*). |
| `training_the_dataset.py` | **Trainer:** Trains a CatBoostRegressor model using the processed data. Implements **Optuna** for hyperparameter tuning to minimize RMSE. |
| `prediction.py` | **Inference:** Loads the trained model to predict the opening week box office for *Avatar: Fire and Ash* using manually defined feature inputs. |

## ⚙️ Key Features
* **Automated Data Collection:** Web scraping pipeline for Box Office Mojo and API integration for TMDb.
* **Feature Engineering:**
    * **Star Power:** A dynamic score calculated based on the historical box office success of the top 3 actors and the director.
    * **Temporal Features:** Release month, holiday releases, and day-of-week analysis.
* **Model Optimization:** Uses **Optuna** to find the optimal hyperparameters (learning rate, depth, L2 regularization) for the CatBoost model.

## 🚀 Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/avatar-box-office-prediction.git](https://github.com/your-username/avatar-box-office-prediction.git)
    cd avatar-box-office-prediction
    ```

2.  **Install dependencies:**
    ```bash
    pip install pandas numpy requests beautifulsoup4 tmdbv3api catboost optuna scikit-learn joblib
    ```

3.  **API Key Configuration:**
    * You need a valid API key from [The Movie Database (TMDb)](https://www.themoviedb.org/documentation/api).
    * Open `tmdb_movie_data_2009_2025.py` and `prediction.py` and replace the placeholder with your key:
        ```python
        tmdb.api_key = 'YOUR_TMDB_API_KEY'
        ```

## 🏃‍♂️ Usage Guide

Run the scripts in the following order to reproduce the entire pipeline:

### 1. Data Collection
Scrape raw box office data and fetch movie details.
```bash
python boxoffice_data_.py
python tmdb_movie_data_2009_2025.py
````

### 2\. Data Processing

Merge datasets and calculate Star Power.

```bash
python merging1.py
```

*Output: `movie_prediction_dataset_final.csv`*

### 3\. Model Training

Train the CatBoost model with hyperparameter tuning.

```bash
python training_the_dataset.py
```

*Output: `catboost_model_optuna.cbm` (Saved Model)*

### 4\. Prediction

Generate the prediction for *Avatar: Fire and Ash*.

```bash
python prediction.py
```

## 📊 Methodology

### The "Star Power" Metric

A unique aspect of this model is the `calculate_star_power` function found in `merging1.py`. It quantifies the bankability of cast and crew by:

1.  Aggregating the past revenue of movies associated with the top 3 actors and the director.
2.  Applying a logarithmic scale to normalize the huge variance in box office numbers.
3.  Summing these weights to create a single `Star_Power` feature for the model.

### Model Performance

The model is evaluated using **RMSE (Root Mean Squared Error)** on a validation set. The final hyperparameters are selected after 250 trials of Optuna optimization.

## 🔮 Prediction: Avatar 3

The `prediction.py` script inputs specific known data points for *Avatar: Fire and Ash*:

  * **Budget:** Estimated at $250M+
  * **Director:** James Cameron
  * **Cast:** Sam Worthington, Zoe Saldana, Sigourney Weaver
  * **Star Power:** Calculated dynamically based on the training data history.

**Current Output:** (Run the script to see the live prediction\!)

## 📜 Disclaimer

This project is for educational and research purposes. Box office predictions are estimates based on historical data patterns and do not guarantee actual financial performance.

```
```
