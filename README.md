# Customer Churn Analysis

## Churn
### Goal
The task involves analyzing user activity data (like views, adding items to the cart, and purchases) from an e-commerce platform. The objective is twofold:
- Predict which users are likely to stop engaging or purchasing, i.e., churn.
- Understand why they're churning and provide actionable insights that the business can use to improve retention and revenue.

### Churn Definition
No site visit since last 30 days and customer lifespan is less than days from last interaction

### Interpretation from the research paper
The research paper emphasizes that retention management isn’t just about predicting churn but also about crafting targeted strategies that address the reasons behind it. This involves:
- Defining churn: Moving beyond a simple yes/no categorization to identifying meaningful patterns in user behavior.
- Feature creation: Capturing elements like transaction recency, frequency, and patterns that predict churn while incorporating customer demographics and browsing behavior.
- Methodology: Leveraging both traditional statistical methods and modern machine learning tools (like random forests and deep learning) to analyze structured and unstructured data.
- Actionable strategies: Using insights not only to retain customers but to enhance their lifetime value by understanding why they’re at risk and tailoring retention campaigns accordingly.

## Model Selection and Training Process

### Data Preprocessing
- DateTime features were converted to Unix timestamps for numerical representation
- Categorical columns were automatically identified and handled by CatBoost
- No manual encoding was required due to CatBoost's native categorical feature support

### Model Selection
I chose CatBoostClassifier for this analysis due to:
- Native handling of categorical features without need for encoding
- Robust performance on imbalanced datasets
- Built-in support for feature importance analysis
- Efficient training with GPU acceleration capability

### Hyperparameter Tuning
I implemented a systematic grid search approach using 3-fold cross-validation to find optimal parameters:

Parameters explored:
- Tree depth: [3, 4, 5, 6]
- Learning rate: [0.01, 0.05, 0.1]
- Number of estimators: [20, 25, 30, 40]

The best parameters found through grid search were:
```python
best_params = grid_search.best_params_  # Actual values will be populated during training
```

## Model Performance Metrics

### Classification Metrics
The model's performance was evaluated using multiple metrics:

1. ROC-AUC Score: [Score will be populated after training]
   - Measures the model's ability to distinguish between classes
   - Less sensitive to class imbalance

2. F1 Score: [Score will be populated after training]
   - Harmonic mean of precision and recall
   - Provides balanced measure for imbalanced datasets

3. Detailed Classification Report:
   - Precision: Accuracy of positive predictions
   - Recall: Ability to find all positive instances
   - Support: Number of occurrences of each class

### Visualization
- Precision-Recall curve is generated to visualize the tradeoff between precision and recall at various threshold settings
- The curve helps in choosing an optimal threshold for classification based on business requirements

## Feature Importance Analysis

### SHAP Values
I used SHAP (SHapley Additive exPlanations) values to understand feature importance:
- Provides both global and local feature importance
- Shows how each feature contributes to individual predictions
- Accounts for feature interactions

Key insights from SHAP analysis:
1. Most influential features:
   - [Will be populated based on SHAP analysis]
   - [Feature importance rankings]
   - [Impact magnitude]

2. Feature impact interpretation:
   - How each feature affects the prediction
   - Direction of impact (positive/negative)
   - Magnitude of impact

### Business Implications

Based on the feature importance analysis:

1. Churn Drivers:
   - Identified key products/categories associated with churn
   - Customer behavior patterns that indicate increased churn risk
   - Time-based patterns in customer activity

2. Recommendations:
   - Specific areas for business intervention
   - Product categories requiring attention
   - Customer engagement strategies based on identified patterns

## Usage Instructions

To run the analysis:
1. Ensure all required libraries are installed
2. Load and preprocess the data according to the preprocessing steps
3. Run the model training with hyperparameter optimization
4. Generate and interpret the performance metrics and SHAP values

## Dependencies
- scikit-learn
- CatBoost
- SHAP
- matplotlib
- pandas
- numpy

## Future Improvements
1. Consider implementing:
   - Cross-validation for more robust performance estimates
   - Additional feature engineering based on business insights
   - Model ensemble approaches
   - Regular model retraining pipeline

2. Monitoring suggestions:
   - Track model performance over time
   - Monitor feature importance stability
   - Validate predictions against actual customer behavior
