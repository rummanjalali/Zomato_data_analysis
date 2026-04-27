
# Bangalore Restaurants Data Analysis (Zomato Dataset)

## Overview
This project presents an end-to-end data analysis and machine learning pipeline on the Zomato Bangalore restaurants dataset. The objective is to extract insights about restaurant behavior, perform predictive modeling, and explore clustering patterns.

The workflow includes:
- Data Cleaning & Preprocessing
- Exploratory Data Analysis (EDA)
- Feature Engineering
- Classification Modeling
- Regression Analysis
- Clustering & Visualization

---

## Dataset
- Source: Kaggle Zomato Bangalore Dataset
- Records: ~56,000 restaurants
- Features include:
  - Location
  - Restaurant Type
  - Cuisines
  - Ratings
  - Votes
  - Online Order Availability
  - Table Booking
  - Approximate Cost for Two

---

## Data Preprocessing

### Key Steps
- Converted binary columns (`Yes/No`) to numeric (1/0)
- Cleaned `rate` column (removed `/5`, converted to float)
- Converted `votes` and `cost` to numeric
- Reduced high-cardinality categorical features:
  - Kept top 10 categories
  - Replaced others with "Other"
- Handled missing values:
  - Mode for categorical
  - Median for numerical
- Dropped irrelevant columns:
  - phone, address, dish_liked, name

---

## Exploratory Data Analysis

### Key Insights
- Most restaurants:
  - Accept online orders
  - Do NOT allow table booking
- Ratings:
  - Normally distributed around ~3.7
- Votes & Cost:
  - Highly right-skewed
- Popular categories:
  - Location: "Other", BTM, HSR
  - Type: Quick Bites, Casual Dining
  - Cuisine: North Indian dominant

### Relationships
- Higher ratings → more votes
- Higher cost → more votes
- Cost does NOT strongly influence rating

---

## Feature Engineering

Created a new feature:
- `expensive`:
  - 1 → cost above median
  - 0 → otherwise

Dropped original cost column afterward.

---

## Machine Learning Models

### 1. Classification (Expensive vs Not)

Models used:
- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting

#### Results

| Model               | Accuracy | Precision | Recall | F1 Score |
|--------------------|----------|----------|--------|----------|
| Logistic Regression | 0.87     | 0.89     | 0.80   | 0.84     |
| Decision Tree       | 0.86     | 0.93     | 0.74   | 0.83     |
| Random Forest       | 0.92     | 0.94     | 0.88   | 0.91     |
| Gradient Boosting   | 0.86     | 0.90     | 0.77   | 0.83     |

Best Model: Random Forest

---

### 2. Regression (Predict Rating)

Models used:
- Linear Regression
- Ridge, Lasso, ElasticNet
- Random Forest Regressor
- Gradient Boosting Regressor

#### Results (RMSE)

| Model               | RMSE  |
|--------------------|-------|
| Linear Regression  | 0.318 |
| Ridge Regression   | 0.318 |
| Lasso Regression   | 0.383 |
| ElasticNet         | 0.382 |
| Random Forest      | 0.254 |
| Gradient Boosting  | 0.274 |

Best Model: Random Forest Regressor

---

## Clustering Analysis

### Method
- KMeans Clustering
- Optimal clusters determined using Elbow Method (k=4)

### Observations
- Clusters are NOT well-separated
- All clusters show similar characteristics:
  - Similar ratings (~3.7)
  - Similar votes
  - Same dominant categories

### Conclusion
- Features lack strong discriminative power
- Clustering not meaningful with current feature set

---

## Visualization

- Histograms for distributions
- Count plots for categorical features
- Pairplots for relationships
- Boxplots for comparisons
- t-SNE for cluster visualization

Result:
- Significant overlap between clusters

---

## Limitations

- High categorical compression (top 10 only)
- Loss of information due to "Other" grouping
- Sparse encoding leads to weak clustering
- Limited feature diversity

---

## Future Improvements

- Use advanced encoding:
  - Target Encoding
  - Embeddings
- Include more features:
  - Reviews text (NLP)
  - Restaurant name patterns
- Try better clustering:
  - DBSCAN
  - Hierarchical Clustering
- Apply PCA before clustering
- Hyperparameter tuning using GridSearchCV
- Handle skewness using log transformation

---

## Tech Stack

- Python
- Pandas, NumPy
- Seaborn, Matplotlib
- Scikit-learn

---

## How to Run

1. Clone repository
2. Install dependencies:
   pip install pandas numpy matplotlib seaborn scikit-learn
3. Run notebook or script

---

## Conclusion

- Random Forest performs best for both classification and regression
- Ratings are influenced more by popularity (votes) than cost
- Clustering needs better features for meaningful segmentation

---

## Author
RUMMAN JALALI

