# NBA Player Longevity Prediction with Gaussian Naive Bayes

## Project Overview
This project aimed to predict NBA player longevity (defined as a career lasting 5 years or more) using a Gaussian Naive Bayes classification model. We analyzed engineered NBA player data, implemented a probabilistic classifier, and evaluated its performance with a focus on business-relevant metrics for a scouting department.

## Dataset
*   **Filename:** `extracted_nba_players_data.csv`
*   **Target Variable:** `target_5yrs` (binary: 1 for longevity, 0 for no longevity)
*   **Features:** Various engineered basketball statistics (e.g., `fg`, `3p`, `ft`, `reb`, `ast`, `stl`, `blk`, `tov`, `total_points`, `efficiency`).

## Modeling Approach
1.  **Data Loading and Preparation:** The dataset was loaded into a pandas DataFrame. Features (`X`) and the target variable (`y`) were separated.
2.  **Data Splitting:** The data was split into training and testing sets using `train_test_split` with a `test_size` of 0.2 and `random_state=42`.
3.  **Model Implementation:** A `GaussianNB` classifier from `sklearn.naive_bayes` was initialized and trained on the training data.
4.  **Prediction:** Predictions were made on the test set (`y_pred`).

## Model Evaluation
The model's performance was evaluated using a Confusion Matrix, Precision, and Recall.

*   **Confusion Matrix:**
    *   True Negatives: 85 (Correctly predicted no longevity)
    *   False Positives: 14 (Incorrectly predicted longevity - 'busts')
    *   False Negatives: 76 (Incorrectly predicted no longevity - 'missed talent')
    *   True Positives: 93 (Correctly predicted longevity)

*   **Precision: 0.8692**
    *   Interpretation: When the model predicts a player will have a 5-year career, it is correct approximately 87% of the time. This is excellent for minimizing false positives (avoiding 'busts').

*   **Recall: 0.5503**
    *   Interpretation: The model correctly identifies about 55% of all players who actually go on to have a 5-year career. This indicates a moderate ability to minimize false negatives (missing out on talented players).

## Naive Bayes "Independence Assumption" Analysis
*   **Assumption:** Gaussian Naive Bayes assumes that all features are conditionally independent given the target variable. This implies that the value of one statistic (e.g., `total_points`) does not influence another (e.g., `efficiency`) when predicting longevity.
*   **Realism for Basketball Stats:** This assumption is largely **unrealistic** for basketball statistics. Metrics like points, assists, and minutes played are highly correlated. For instance, more minutes often lead to more points, and efficient players tend to score more. Despite this violation, Naive Bayes can still perform surprisingly well due to its robust ranking of probabilities.

## Model Reliability and Limitations for a Scouting Department

### Reliability:
*   **High Precision:** The model is highly reliable for identifying players who *are* likely to achieve longevity, which is crucial for making confident investment decisions and avoiding 'busts'.
*   **Efficiency:** It's a simple, fast, and computationally inexpensive model.

### Limitations:
*   **Moderate Recall:** The model misses a significant portion of players who *do* achieve longevity (false negatives). This means valuable talent could be overlooked if the model is used as a sole decision-making tool.
*   **Violated Assumption:** The independence assumption is violated by the nature of basketball statistics, meaning the model's underlying probability calculations might be inaccurate, although its classification performance can still be acceptable.
*   **No Direct Feature Importance:** Gaussian Naive Bayes does not inherently provide a clear ranking of the most influential features, which can limit interpretability for scouts seeking to understand *why* a player is predicted to succeed or fail.
*   **Binary Output:** Provides only a binary prediction (longevity vs. no longevity) without detailed explanations or nuanced probabilities, which might be insufficient for comprehensive scouting.

### Actionable Recommendations:
*   **Filter, Not Final Decision:** Use the model as an initial filter to identify a strong pool of potential long-term players (high precision output) for further, in-depth human scouting.
*   **Beware of Missed Talent:** Do not solely dismiss players predicted to have no longevity without additional human review, as the model has a notable recall limitation.
*   **Complement with Expertise:** Always integrate model predictions with qualitative assessments, game film analysis, and the vast experience of human scouts.
*   **Explore Alternatives:** Consider exploring more sophisticated models (e.g., Logistic Regression, Random Forests) that can better handle feature correlations and provide richer insights into feature importance.
