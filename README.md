# Advanced-Neural-Network-Models-for-Precision-Real-Estate-

Can deep learning predict real estate prices more accurately than traditional models?  
This project explores how feedforward neural networks can outperform linear regression by capturing nonlinear relationships in housing features and prices.

---

##  Overview

This project uses structured housing data to compare the predictive performance of traditional regression models against a fully connected neural network (ANN).  
By tuning hyperparameters like learning rate, dropout, and network depth, the model achieved higher precision in estimating home prices — showcasing the potential of neural networks in real estate analytics.

---

##  Dataset Summary

-  **Location**: Real estate data from metropolitan areas (includes property size, location, amenities)
-  **Features**: Square footage, location type, bedroom/bathroom count, year built, etc.
-  **Target**: Home sale price (continuous variable)

---

##  Modeling Approach

###  Preprocessing
- Cleaned missing values and normalized numeric inputs
- One-hot encoded categorical features
- Split into training, validation, and test sets (80/10/10)

###  Baseline Model
- Linear regression with normalized input features
- Served as a benchmark for model comparison

###  Neural Network (ANN)
- Multi-layer feedforward network using Keras/TensorFlow
- Tuned:
  - Learning rate  
  - Batch size  
  - Dropout rate  
  - Number of hidden layers and neurons

- Optimized using:
  - Mean Squared Error (MSE) loss
  - Adam optimizer
  - Early stopping to prevent overfitting

---

##  Results

| Model               | RMSE     | R² Score |
|--------------------|----------|----------|
| Linear Regression  | 162,503  | 0.61     |
| Neural Network     | **118,090**  | **0.83**     |

- The ANN significantly outperformed linear regression, especially on high-priced properties where nonlinear trends were strongest.
- Model tuning and regularization (e.g. dropout) helped reduce overfitting.

---

##  Tools Used

- Python (Pandas, NumPy, Scikit-learn)
- Keras / TensorFlow
- ggplot2 (for visualization)
- RMarkdown (for documentation)

---

##  Repository Structure

📄 Advanced Neural Network Models for Precision Real Estate.Rmd # Full report in R Markdown
📄 Advanced Neural Network Models for Precision Real Estate.pdf # Rendered report
📄 README.md # Project summary


---

##  Key Takeaways

- Achieved highly accurate house price predictions with a neural network (RMSE = **0.0199**), outperforming Ridge and Linear Regression by a wide margin.
- Identified `grade`, `sqft_living`, and `waterfront` as the most influential features, improving model transparency.
- Ridge Regression explained **85.39% of variance**, helping mitigate feature redundancy and overfitting risks.
- Neural networks proved especially effective for capturing complex pricing patterns — particularly in high-value homes.

---

## 📬 Contact

Created by **Enoghayin Jillient Imasuen**  
🔗 [GitHub](https://github.com/enoimasuen) | [LinkedIn](https://www.linkedin.com/in/enoghayin-jillient-imasuen-9080b2236?)

