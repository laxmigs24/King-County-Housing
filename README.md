
Project Title: King County House Price Prediction using Machine Learning

1. Project Overview

This project develops and evaluates multiple machine learning regression models to predict house prices in King County (Seattle) using historical housing data over a one-year period (from May 2014 through May 2015).

The objective is to build a model that accurately estimates property prices based on structural, geographical, and neighbourhood-related features, while ensuring strong generalisation to unseen data.

2. Motivation

Accurate house price prediction is a critical problem in real estate analytics.

This project explores how different regression models perform on structured housing data and identifies the most reliable approach for real-world price estimation.

3. Problem Statement

Given a dataset of residential property sales, predict the target variable:

Target (y): price

Using features such as:

- property size (sqft_living, sqft_lot)
- quality (grade, condition)
- location (lat, long, zipcode)
- neighbourhood context (sqft_living15, sqft_lot15)

4. Dataset

- Source: King County housing dataset (2014–2015)
- Size: ~21,600 observations
- Features: 21 original variables

Key characteristics:

- Right-skewed price distribution
- Strong correlation between price and size/quality variables

5. Methodology

5.1. Data Exploration

- Analysed data structure, distributions, and correlations
- Identified key predictive features (e.g. sqft_living, grade)

5.2. Data Cleaning

- Removed extreme outliers:
    - unrealistic bedroom/bathroom values
    - price outside 1st–99th percentile

- Verified:
- no missing values
- no duplicated rows (repeated IDs retained as valid sales)

6. Feature Engineering

- Created additional variables to better represent real-world property characteristics:

    - house_age
    - years_since_renovation
    - total_rooms
    - basement_ratio
    - living_lot_ratio

- Removed redundant features to avoid multicollinearity:

    - id, date
    - sqft_above, sqft_basement

7. Preprocessing Pipeline

- Numerical features:
    - Median imputation
    - Standard scaling

- Categorical features:
    - zipcode treated as categorical
    - One-hot encoding applied

8. Train/Test Split

- 80/20 split
- Ensures evaluation on unseen data
- Random state fixed for reproducibility

9. Models Evaluated

- Baseline models:

    - Linear Regression
    - KNN Regressor

- Improved models:

    - Ridge Regression
    - Random Forest Regressor
    - Gradient Boosting Regressor

10. Model Performance

| Model             | R²         | MAE         |
| ----------------- | ---------- | ----------- |
| Linear Regression | ~0.84      | ~$78K       |
| KNN Regressor     | ~0.78      | ~$83K       |
| Gradient Boosting | ~0.86      | ~$70K       |
| **Random Forest** | **~0.864** | **~$63.9K** |

Observation:
Ensemble models significantly outperform linear and distance-based models.

11. Hyperparameter Tuning

The best-performing model (Random Forest) was further optimised using:

- RandomizedSearchCV

Key parameters tuned:

- number of trees
- maximum depth
- minimum samples per split
- feature selection per split

Result:

- MAE improved to ~$63.2K
- R² improved to ~0.867

12. Final Model

Tuned Random Forest Regressor

Performance on test set:

- R²: ~0.867
- MAE: ~$63,188
- RMSE: ~$103,354

13. Evaluation Metrics

- MAE (Mean Absolute Error)
- Average absolute difference between predicted and actual prices
- RMSE (Root Mean Squared Error)
- Penalises larger errors more strongly
- R² (Coefficient of Determination)
- Proportion of variance explained by the model

14. Error Analysis

- Median error ≈ $36K
- Mean error ≈ $63K

Interpretation:

- Most predictions are relatively accurate
- A small number of large errors increase the mean
- Errors are higher for expensive properties

15. Predictions vs Actual Values

- Predictions closely follow actual values overall
- Greater deviation observed for high-price properties

16. Feature Importance

Most influential features (Random Forest):

- grade
- lat, long
- sqft_living
- sqft_living15
- sqft_lot15

Key insight:

- House prices are primarily driven by:

    - property quality
    - location
    - living space

17. Model Reliability

- No strong evidence of underfitting
- No strong evidence of overfitting
- Strong performance on test data indicates good generalisation

Hyperparameter tuning helped:

- control model complexity
- reduce variance
- improve robustness

18. How to Run the Project

1. Clone the repository
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
2. Install dependencies
pip install -r requirements.txt
3. Launch the notebook
jupyter notebook

Open:

ML_project_model comparison2.ipynb

Project Structure:

├── ML_project_model comparison2.ipynb
├── README.md
├── requirements.txt (optional)

19. Contributors

- Greg2828
- laxmigs24
- vitorferraz19

20. Key Takeaways

- Feature engineering is critical for model performance
- Ensemble methods handle complex relationships effectively
- MAE provides strong business interpretability
- Evaluation should combine metrics and error analysis
- Real-world datasets require careful cleaning and assumptions

21. Potential Future Improvements

- Cross-validation for more robust evaluation
- Feature selection optimisation
- Testing additional models (e.g. XGBoost, LightGBM)
- Deployment as a web-based pricing tool

22. Notes

- This project is part of a machine learning learning track
- Dataset reflects a specific region and time period (Seattle, 2014–2015)
- Model performance may vary on different markets
