# Customer Churn Analysis

## Model Selection and Training Process

### Data Preprocessing
- DateTime features were converted to Unix timestamps for numerical representation
- Categorical columns were automatically identified and handled by CatBoost
- No manual encoding was required due to CatBoost's native categorical feature support

### Model Selection
We chose CatBoostClassifier for this analysis due to:
- Native handling of categorical features without need for encoding
- Robust performance on imbalanced datasets
- Built-in support for feature importance analysis
- Efficient training with GPU acceleration capability

### Hyperparameter Tuning
We implemented a systematic grid search approach using 3-fold cross-validation to find optimal parameters:

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
We used SHAP (SHapley Additive exPlanations) values to understand feature importance:
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
