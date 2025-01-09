# Customer Churn Analysis

## Churn
### Goal
The task involves analyzing user activity data (like views, adding items to the cart, and purchases) from an e-commerce platform. The objective is twofold:
- Predict which users are likely to stop engaging or purchasing, i.e., churn.
- Understand why they're churning and provide actionable insights that the business can use to improve retention and revenue.
                        
### Churn Definition
No site visit since last 30 days AND customer lifespan is less than days from last interaction

### Rationale behind churn definition
My churn definition captures both behavioral signals: inactivity and historical engagement.

The 30-day window is a good sweet spot - long enough to filter out normal purchase cycles but short enough to enable timely interventions
Including customer lifespan adds crucial context - newer customers might have different expected visit patterns than long-term loyal ones
Using site visits rather than just purchases captures early warning signs, since dropping engagement often precedes purchase churn. The 30-day inactivity threshold makes perfect sense for e-commerce. Unlike subscription businesses where churn is crystal clear (they cancel), retail shopping has natural gaps. Think about it - even loyal customers don't typically shop every week. The 30-day window captures this natural shopping cycle while being short enough to let you intervene before losing them completely.

The second part - checking if their lifespan is shorter than days since last interaction - is best suited for handling edge cases because:
- It automatically adapts to each customer's unique shopping pattern. If someone typically shops every 2 weeks, a 30-day gap is concerning. If they shop quarterly, maybe not so much.
- It helps distinguish between true churners and seasonal shoppers (like holiday-only customers)
- It naturally handles new vs. established customers differently. A 30-day gap from a 2-year loyal customer means something very different than the same gap from a one-time buyer.

For predictive modeling, this definition gives us clean labels while avoiding some classic pitfalls:
- Not too sensitive (won't flag normal shopping gaps as churn)
- Not too lenient (won't wait until it's too late to intervene)
- Accounts for user heterogeneity (different shopping frequencies)

### Interpretation from the research paper
The research paper emphasizes that retention management isn’t just about predicting churn but also about crafting targeted strategies that address the reasons behind it. This involves:
- Moving beyond a simple yes/no categorization to identifying meaningful patterns in user behavior.
- Capturing elements like transaction recency, frequency, and patterns that predict churn while incorporating customer demographics and browsing behavior.
- Leveraging both traditional statistical methods and modern machine learning tools (like random forests and deep learning) to analyze structured and unstructured data.
- Using insights not only to retain customers but to enhance their lifetime value by understanding why they’re at risk and tailoring retention campaigns accordingly.

## Feature Rationale for Churn Prediction

## **1. Recency, Frequency, and Monetary (RFM) Metrics**
### **Recency**: Days since the last purchase
- **Rationale**: Indicates how recently a user made a purchase. Customers with recent purchases are more likely to remain engaged.

### **Frequency**: Number of purchases
- **Rationale**: Reflects how often a customer purchases, which helps identify loyal or habitual buyers.

### **Monetary**: Total amount spent
- **Rationale**: Measures customer value based on spending. High-spending customers are key contributors to revenue.

---

## **2. Temporal Features**
### **First interaction**: Timestamp of the first recorded event
- **Rationale**: Helps understand when the user started interacting with the platform.

### **Last interaction**: Timestamp of the last recorded event
- **Rationale**: Indicates whether the user is still active or has churned.

### **Activity days**: Number of unique days a user was active
- **Rationale**: Measures engagement consistency and user activity spread over time.

### **Inactivity period**: Days between the first and last interaction
- **Rationale**: Helps understand how stretched or condensed the user’s engagement is over time.

### **Customer lifespan**: Total days between the first and last interaction
- **Rationale**: Captures how long a user has been active on the platform.

### **Days since last interaction**: Days since the last recorded event
- **Rationale**: Indicates how recently the user interacted with the platform, important for churn prediction.

### **Interaction per day**: Distinct products interacted with per active day
- **Rationale**: Measures how engaged a user is during their active days, reflecting intensity of usage.

---

## **3. Time Preferences**
### **Morning, Afternoon, Evening, and Night shopper**
- **Rationale**: Understanding time preferences helps personalize engagement strategies (e.g., targeting users with offers at their active times).

### **Weekday and Weekend shopper**
- **Rationale**: Identifies whether users are more active during workdays or leisure time, aiding in promotional planning.

---

## **4. Purchase Acceleration Metrics**
### **Average time between purchases**
- **Rationale**: Helps identify the user’s purchasing cycle, enabling predictions of when they are likely to purchase again.

---

## **5. Session-Based Metrics**
### **Session count**: Number of unique sessions
- **Rationale**: Indicates how often the user visits the platform, a proxy for engagement.

### **Average session duration**: Mean duration of sessions
- **Rationale**: Reflects how long users stay engaged per session, highlighting deeper engagement.

### **Session variance**: Variance in session durations
- **Rationale**: Captures consistency or variability in user engagement patterns.

### **Total events**: Total number of events in all sessions
- **Rationale**: Measures overall engagement level.

### **Bounce rate**: Proportion of sessions with only one event
- **Rationale**: Indicates whether users engage deeply or just visit briefly (low engagement).

### **Average value density**: Revenue per minute of session duration
- **Rationale**: Combines engagement duration with monetary value to identify high-value users efficiently.

---

## **6. Product and Brand Preferences**
### **Most viewed brand and category**
- **Rationale**: Identifies brands/categories the user is most interested in, useful for recommendation systems.

### **Top purchased category**
- **Rationale**: Highlights user preferences for categories they purchase the most, aiding in targeted marketing.

---

## **7. Brand Loyalty**
### **Brand loyalty score**
- **Rationale**: Measures how committed a user is to a specific brand, useful for identifying loyalists who can be targeted for exclusive offers.

---

## **8. Behavioral Patterns**
### **Views, Carts, and Purchases**
- **Rationale**: Basic metrics to capture the volume of each user action, essential for behavioral analysis.

### **View-to-cart ratio**
- **Rationale**: Measures how effectively the platform converts views into cart additions.

### **Cart-to-purchase ratio**
- **Rationale**: Tracks conversion from intent (cart) to action (purchase), highlighting potential drop-offs in the buying process.

---

## **9. Browse-to-Purchase Behavior**
### **Average views before purchase**
- **Rationale**: Helps understand the user’s decision-making process and effort before purchasing.

### **Session conversion rate**
- **Rationale**: Measures how often sessions lead to purchases, reflecting session effectiveness.

---

## **10. Price Sensitivity and Patterns**
### **Price variance**
- **Rationale**: Indicates how much variability exists in the user’s price preferences.

### **Price range**
- **Rationale**: Captures the spread of prices the user is comfortable interacting with, helping identify high- or low-budget users.

### **Average price viewed and purchased**
- **Rationale**: Highlights user behavior with respect to pricing during browsing and buying.

### **High- and low-value interactions**
- **Rationale**: Indicates the extent to which a user interacts with products above or below their typical price range, reflecting price sensitivity.

### **Price sensitivity score**
- **Rationale**: Ratio of purchased to viewed prices indicates whether the user leans towards higher-value or lower-value purchases compared to their browsing habits.

---

## **11. Cart Abandonment Metrics**
### **Cart abandonment rate**
- **Rationale**: Measures the proportion of unconverted carts, reflecting potential user hesitation or dissatisfaction.

---

## **12. Product Interaction Patterns**
### **Distinct products, brands, and categories**
- **Rationale**: Measures the diversity of the user’s interactions, useful for understanding breadth of interest.

### **Category diversity**
- **Rationale**: Number of unique categories interacted with, indicating exploratory behavior.

### **Category exploration index**
- **Rationale**: Normalized measure of category diversity relative to total interactions, capturing exploration depth.

### **Repeat view rate**
- **Rationale**: Measures how often users revisit the same products, indicating strong interest or uncertainty.

---

These features collectively provide a comprehensive view of user behavior, preferences, engagement, and purchasing patterns. Each feature enables actionable insights, from personalized marketing to churn prediction, and builds a strong foundation for predictive modeling.


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
param_grid = {
    'depth': [3, 4, 5, 6],
    'learning_rate': [0.01, 0.05, 0.1],
    'n_estimators': [20, 25, 30, 40]
}

cat_boost_model = CatBoostClassifier(task_type='CPU', silent=True)

grid_search = GridSearchCV(
    estimator=cat_boost_model,
    param_grid=param_grid,
    cv=3,  # 3-fold cross-validation
    scoring='roc_auc',
    verbose=1,
    error_score='raise'
)

grid_search.fit(X, y, cat_features=categorical_cols)
best_params = grid_search.best_params_
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
