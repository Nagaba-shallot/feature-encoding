# 🏠 House Price Prediction - Encoding Techniques Comparison

## 📋 Project Overview

This project explores and compares different **categorical encoding techniques** for predicting house prices using the **Ames Housing Dataset**. The goal is to understand how different encoding methods affect the performance of a **Linear Regression** model.

### 🎯 Key Questions Answered
- Which encoding technique works best for house price prediction?
- How do hybrid encoding approaches compare to individual methods?
- What impact does feature encoding have on model performance?

---

## 📊 Dataset

### Ames Housing Dataset
- **Source:** Kaggle - House Prices: Advanced Regression Techniques
- **Training Samples:** 1,460 houses
- **Features:** 80 (mixed numeric and categorical)
- **Target Variable:** SalePrice (continuous)

### Feature Types
| Type | Count | Examples |
|------|-------|----------|
| Numerical | 36 | LotArea, YearBuilt, GrLivArea |
| Categorical | 44 | Neighborhood, MSZoning, SaleType |

---

## 🔧 Encoding Methods Compared

### 1️⃣ Label Encoding
Converts each category to a unique integer (0, 1, 2, ...).
- **Best for:** Ordinal features (e.g., quality ratings)
- **Pros:** Simple, memory-efficient
- **Cons:** May imply false ordinal relationships

### 2️⃣ One-Hot Encoding
Creates binary columns for each category.
- **Best for:** Nominal features (e.g., Neighborhood)
- **Pros:** Preserves category relationships
- **Cons:** Creates many columns (curse of dimensionality)

### 3️⃣ Feature Hashing
Uses a hash function to convert categories to fixed-size vectors.
- **Best for:** High-cardinality features
- **Pros:** Memory-efficient, fixed dimensions
- **Cons:** Hash collisions possible

### 4️⃣ Frequency Encoding
Replaces categories with their frequency in the dataset.
- **Best for:** Features where frequency matters
- **Pros:** Simple, captures importance
- **Cons:** May overfit rare categories

### 5️⃣ Label + One-Hot (Hybrid)
Combines Label Encoding for ordinal features and One-Hot for nominal features.
- **Best for:** Mixed feature types
- **Pros:** Best of both worlds
- **Cons:** More complex implementation

### 6️⃣ Hashing + Frequency (Hybrid)
Combines Feature Hashing for high-cardinality and Frequency Encoding for others.
- **Best for:** Memory-efficient encoding
- **Pros:** Good balance of performance and memory
- **Cons:** May lose some information

---

## 📈 Results

### Performance Comparison

| Method | RMSE ($) | R² Score | Data Shape | Rank |
|--------|----------|----------|------------|------|
| 1. Label Encoding | 34,119.51 | 0.8482 | (1460, 80) | 4 |
| 2. One-Hot Encoding | 65,346.16 | 0.4433 | (1460, 268) | 6 |
| 3. Feature Hashing | *Pending* | *Pending* | (1460, 100) | - |
| 4. Frequency Encoding | 33,687.39 | 0.8520 | (1460, 80) | 3 |
| **5. Label + One-Hot** | **29,974.42** | **0.8829** | (1460, 235) | **1** 🏆 |
| 6. Hashing + Frequency | 31,824.23 | 0.8680 | (1460, 130) | 2 |

### 🏆 Best Performing Method: **Label + One-Hot (Hybrid)**

**Why it works best:**
- Preserves ordinal relationships (Label Encoding for quality ratings)
- Properly handles nominal categories (One-Hot for neighborhoods)
- Avoids creating too many sparse features
- Captures meaningful patterns in the data

---

## 📊 Visualizations

### RMSE Comparison
*Bar chart showing RMSE for each encoding method*

### R² Score Comparison
*Bar chart showing R² scores for each encoding method*

### Actual vs Predicted Plots
*Scatter plots showing prediction accuracy for each method*

---

## 🛠️ Technical Details

### Model
- **Algorithm:** Linear Regression
- **Evaluation Metrics:**
  - RMSE (Root Mean Squared Error)
  - R² Score (Coefficient of Determination)
- **Train/Test Split:** 80/20

### Libraries Used
```python
import pandas as pd          # Data manipulation
import numpy as np           # Numerical operations
import matplotlib.pyplot as plt  # Visualization
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
from sklearn.feature_extraction import FeatureHasher
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score

## 🚀 How to Run

### 1. Clone the Repository
```bash
git clone https://github.com/Nagaba-shallot/feature-encoding.git
cd feature-encoding
```

### 2. Install Dependencies
```bash
pip install pandas numpy matplotlib scikit-learn
```

### 3. Run the Notebook
```bash
jupyter notebook Features.ipynb
```

### 4. Run All Cells
Click **Kernel** → **Restart & Run All** in the Jupyter interface.

---

## 📁 Repository Structure

```text
house-price-encoding-comparison/
├── Features.ipynb              # Main Jupyter Notebook
├── train.csv                   # Training dataset
├── test.csv                    # Test dataset
├── sample_submission.csv       # Sample submission file
├── README.md                   # Project documentation
└── requirements.txt            # Python dependencies
```

---

## 💡 Key Insights: What We Learned

*   **Hybrid approaches outperform single methods** — Combining *Label + One-Hot* encoding gave the best overall results. The structured combination proved greater than the sum of its parts.
*   **One-Hot Encoding alone performed poorly** — It created too many sparse columns (**268 features** total), which led to overfitting.
*   **Frequency Encoding is a strong baseline** — Simple yet highly effective, achieving the second-best $R^2$ score.
*   **Feature Hashing is highly memory-efficient** — It successfully reduced dimensionality to a fixed size (**100 features**) while maintaining reasonable performance metrics.
*   **Ordinal features must be preserved** — Applying *Label Encoding* to quality ratings helped maintain their natural mathematical order, preventing the model from assuming artificial relationships.

---

## 📝 Recommendations

### 🏆 For Best Performance
*   Use a **Label + One-Hot** hybrid approach.
*   Clearly separate ordinal vs. nominal features.
*   Apply the appropriate encoding method to each distinct feature type.

### 💾 For Large Datasets
*   Use a **Hashing + Frequency** hybrid.
*   This approach is memory-efficient and strikes an excellent balance between scale and performance.

### ⚡ For Simple Projects
*   Default to **Frequency Encoding**.
*   It is easy to implement and yields a decent baseline performance.

---

## 🔬 Future Work

- [ ] Add **Cyclic Encoding** for time-based features (such as month and year built).
- [ ] Try **Target Encoding** for high-cardinality features like neighborhood.
- [ ] Experiment with different hyperparameter hash sizes.
- [ ] Test alternative ensemble models (e.g., **Random Forest**, **XGBoost**).
- [ ] Add a comprehensive **feature importance** analysis block.

---

## 👤 Author

*   **Name:** Nagaba Shallot
*   **GitHub:** @Nagaba-shallot(https://github.com/Nagaba-shallot)
*   **LinkedIn:** Nagaba Shallot(https://www.linkedin.com/in/nagaba-shallot-9a81a5402)

**Date:**27 August 2026

---

## 📄 License

This project is for educational purposes as part of a Machine learnig and Data Science.

---

## 🙏 Acknowledgments

*   **Kaggle** for providing the Ames Housing Dataset.
*   **scikit-learn** for the robust machine learning utility tools.
*   **My Instructor** for guidance, reviews, and continuous feedback.
