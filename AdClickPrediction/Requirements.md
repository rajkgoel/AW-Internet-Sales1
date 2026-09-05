# Click-Through Rate (CTR) Prediction Project

## Problem Understanding

### What You're Building

A predictive system that determines the likelihood of a user clicking on an advertisement based on:

- **User characteristics** (demographics, behavior)
- **Advertisement attributes** (campaign, product, webpage)
- **Temporal factors** (time of day, day of week)
- **Contextual features** (session information)

### Business Context

- **Why it matters:** Higher CTR = More revenue for advertisers
- **Use case:** Ad targeting, campaign optimization, budget allocation
- **Success metric:** Accurately identify users likely to click (high ROC-AUC)

### Key Challenge

**Highly Imbalanced Dataset:** In real-world scenarios, click rates are typically 1-5%, meaning 95-99% of data points are "no clicks".

## Dataset Features

| Feature | Description |
| --- | --- |
| `session_id` | Unique identifier for the session. |
| `DateTime` | Timestamp of the ad impression. |
| `user_id` | Unique identifier for the user. |
| `product` | The product being advertised. |
| `campaign_id` | Identifier for the advertising campaign. |
| `webpage_id` | Identifier for the webpage where the ad was displayed. |
| `product_category_1` | The broad, high-level category of the product. Think of this as the main "department" in a store (e.g., Men's Fashion, Home & Garden). |
| `product_category_2` | A sub-category or a more specific niche within the primary category. For example, if Category 1 is "Electronics," Category 2 might be "Headphones" or "Laptops." |
| `user_group_id` | Identifier for the user group. |
| `gender` | The gender of the user (e.g., Male, Female). |
| `age_level` | The age bracket or level of the user. |
| `user_depth` | A metric representing the user's depth of engagement or history. |
| `city_development_index` | A score representing the development level of the user's city. |
| `var_1` | An anonymized feature (likely a categorical or count variable). |
| `is_click` | The target variable indicating whether the user clicked on the ad (1 for click, 0 for no click). |

## Questions to Approach

1. **Data Loading & Initial Assessment:** Efficiently load the raw ad impression data and perform an initial deep dive to understand its structure and quality?
2. **Feature Engineering & Enrichment:** Transform the raw data into powerful predictive features that capture user behavior, ad context, and temporal patterns?
3. **Data Preprocessing & Transformation:** Prepare the engineered features for machine learning models, addressing issues like missing values and categorical data?
4. **Handling Data Imbalance:** Use techniques to mitigate the challenges posed by a heavily imbalanced target variable to ensure the model doesn't overlook the minority class?
5. **Model Selection & Training:** Which machine learning algorithms are best suited for ad click prediction, and how do I train them effectively on the prepared data?
6. **Model Evaluation & Comparison:** Assess the performance of the trained models and determine which one is most effective for the ad click prediction task?
7. **Insights & Interpretability:** Extract actionable insights from the best-performing model to understand the drivers of ad clicks?

## Phase 1: Data Exploration & Understanding

### Step 1: Initial Data Loading

**What to Check:**

- **Dataset dimensions:** How many rows and columns?
- **Column types:** Which are numerical? Which are categorical?
- **Target variable:** What is the click-through rate (CTR)?
- **Missing values:** Which columns have nulls and how many?

### Step 2: Exploratory Data Analysis (EDA)

**Key Questions to Answer:**

**Target Distribution**

- What percentage of ads get clicked?
- Is the dataset severely imbalanced?
- Do you need resampling techniques?

**Temporal Patterns**

- Which hours have highest click rates?
- Are weekends different from weekdays?
- Do certain months perform better?

**User Behavior**

- Do certain age groups click more?
- Is there a gender difference in click rates?
- How does user group affect clicking?

**Campaign Performance**

- Which campaigns have highest CTR?
- Which products get more clicks?
- Do certain webpages convert better?

## Phase 2: Feature Engineering

### Feature Engineering Strategy

#### 1. DateTime Feature Extraction

**Why:** Time patterns strongly influence user behavior.

**Features to Create:**

```python
# Extract from DateTime column
- hour: Hour of day (0-23)
- day_of_week: Day (0=Monday, 6=Sunday)
- day_of_month: Date of month (1-31)
- month: Month of year (1-12)
- is_weekend: Binary flag (Saturday/Sunday = 1)
- time_of_day: Categorical (night/morning/afternoon/evening)
```

**Rationale:**

- Users click more during lunch hours
- Weekends may have different behavior
- End-of-month might affect purchasing decisions

#### 2. Interaction Features

**Why:** Combinations of features often reveal hidden patterns.

**Features to Create:**

```python
- user_product_interaction: user_id + product
- campaign_webpage: campaign_id + webpage_id
- gender_age: gender + age_level
```

**Rationale:**

- Specific user-product combinations might have high affinity
- Campaign effectiveness varies by placement
- Demographics combinations reveal micro-segments

#### 3. Aggregated Features

**Why:** Historical performance is a strong predictor.

**User-Level Aggregations:**

```python
- user_total_views: How many ads has this user seen?
- user_total_clicks: How many times has this user clicked?
- user_ctr: User's personal click-through rate
- user_sessions: Number of unique sessions per user
```

**Product-Level Aggregations:**

```python
- product_views: Total times this product was shown
- product_ctr: This product's historical click rate
```

**Campaign-Level Aggregations:**

```python
- campaign_views: Total impressions for this campaign
- campaign_ctr: Campaign's historical performance
```

## Phase 3: Data Preprocessing

### Step 1: Handle Missing Values

**Strategy:**

```python
# Numerical columns: Fill with median (robust to outliers)
# Categorical columns: Fill with mode (most frequent value)
```

### Step 2: Encode Categorical Variables

**Approach:** Label Encoding

**Columns to Encode:**

- `product`
- `campaign_id`
- `webpage_id`
- `product_category_1`, `product_category_2`
- `gender`
- `user_group_id`
- `var_1`
- All interaction features (`user_product_interaction`, etc.)

### Step 3: Feature Selection

**Columns to Drop:**

```python
drop_cols = ['DateTime', 'session_id', 'user_id']
```

**Why Drop These?**

- `DateTime`: Already extracted features from it
- `session_id`: Too granular, no predictive value
- `user_id`: Causes overfitting (too many unique values)

**Final Feature Set:**

- All engineered features
- Encoded categorical variables
- Aggregated statistics

### Step 4: Train-Test Split

**Why Stratify?** In imbalanced datasets, stratification ensures both train and test have similar CTR.

### Step 5: Feature Scaling

**Method:** StandardScaler

```python
# Transforms features to have:
# - Mean = 0
# - Standard deviation = 1
```

**Why Scale?**

- **Required for:** Logistic Regression, SVM
- **Improves:** Convergence speed, model performance
- **Not critical for:** Tree-based models (Random Forest, Gradient Boosting)

## Phase 4: Handling Class Imbalance

### Understanding the Problem

**Typical CTR Scenario:**

- Class 0 (No Click): 95-98%
- Class 1 (Click): 2-5%

**Why This Matters:**

- Models tend to predict the majority class
- High accuracy (95%) can be achieved by always predicting "no click"
- Need to balance precision and recall

## Phase 5: Model Building

### Model Selection Strategy

**Why Multiple Models?**

- Different algorithms capture different patterns
- Ensemble of models often performs better
- Compare to find best approach for this dataset

## Phase 6: Model Evaluation

### Metrics for Imbalanced Classification

**❌ Don't Rely On:**

- **Accuracy:** Misleading in imbalanced datasets
  - 95% accuracy = always predicting "no click"

**✅ Focus On:**

- **Precision:** Of predicted clicks, how many were actual clicks?

  ```
  Precision = True Positives / (True Positives + False Positives)
  ```

  *Business Impact:* Reduces wasted ad spend

- **Recall:** Of actual clicks, how many did we predict?

  ```
  Recall = True Positives / (True Positives + False Negatives)
  ```

  *Business Impact:* Captures revenue opportunities

- **F1-Score:** Harmonic mean of Precision and Recall

  ```
  F1 = 2 × (Precision × Recall) / (Precision + Recall)
  ```

  *Business Impact:* Balances both metrics

- **ROC-AUC:** Area Under Receiver Operating Characteristic Curve

  ```
  Range: 0.5 (random) to 1.0 (perfect)
  ```

  *Business Impact:* Overall model discrimination ability — **Most Important Metric for this problem**

### Interpretation Guidelines

**Good Performance Indicators:**

- ROC-AUC > 0.75: Good discrimination
- F1-Score > 0.30: Reasonable for imbalanced data
- Recall > 0.50: Catching majority of clickers
- Precision > 0.30: Reducing false positives

**Model Comparison:**

- Compare all metrics across models
- Consider trade-offs (precision vs recall)
- Choose based on business priority

## Phase 7: Visualization & Insights

### Essential Visualizations

**1️⃣ Model Comparison Chart**

- **Purpose:** Compare all metrics across models
- **Type:** Grouped bar chart
- **Shows:** Accuracy, Precision, Recall, F1, ROC-AUC side-by-side

**2️⃣ Feature Importance Plot**

- **Purpose:** Identify most influential features
- **Type:** Horizontal bar chart
- **Shows:** Top 20 features for tree-based models
- **Insights:** Which features drive clicks?

**3️⃣ Confusion Matrix**

- **Purpose:** Understand error types
- **Type:** Heatmap
- **Shows:** True Positives, False Positives, True Negatives, False Negatives
- **Helps:** Identify if model is biased

**4️⃣ ROC Curve (Optional)**

- **Purpose:** Visualize precision-recall trade-off
- **Type:** Line plot
- **Shows:** True Positive Rate vs False Positive Rate

### Key Insights to Extract

**Which features matter most?**

- User historical behavior (`user_ctr`)
- Product popularity (`product_ctr`)
- Time-based features (`hour`, `day_of_week`)

**Which model performs best?**

- Highest ROC-AUC
- Best F1-score
- Consider training time

**What patterns exist?**

- Peak clicking hours
- High-performing campaigns
- User segments with high CTR
