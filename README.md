# ISLP Chapter 3 Solutions

Solutions for questions 2, 9, 10, and 12 from Introduction to Statistical Learning with Python Chapter 3.

## Question 2

**KNN Classifier vs KNN Regression:**
- **KNN Classifier**: Predicts a category by taking a majority vote among the K nearest neighbors
- **KNN Regression**: Predicts a numerical value by averaging the values of the K nearest neighbors

## Question 9

### Parts a & b
See accompanying Jupyter notebook for detailed implementation.

### Part c - Multiple Linear Regression Analysis

#### i. Overall Model Significance
**Result**: YES, there is a statistically significant relationship between the predictors and mpg (p < 0.05)

#### ii. Statistically Significant Predictors  
**Significant predictors** (p < 0.05): `const`, `displacement`, `weight`, `year`, `origin`

#### iii. Year Coefficient Interpretation
- **Coefficient**: 0.7508
- **P-value**: < 0.001
- **Interpretation**: For each additional year, mpg increases by 0.7508 units on average, holding other variables constant. This relationship is statistically significant.

### Part d - Diagnostic Analysis

**Outlier Detection:**
- Number of potential outliers (|residual| > 2 std): 18
- Outlier observations: [43, 107, 110, 153, 164, 242, 245, 268, 307, 320, 322, 323, 324, 325, 327, 331, 381, 388]

**Leverage Analysis:**
- Number of high leverage points: 17
- High leverage observations: [6, 7, 8, 12, 13, 25, 26, 27, 28, 93, 94, 115, 209, 297, 298, 359, 388]

**Normality Test:**
- P-value: < 0.001
- **Conclusion**: Residuals may not be normally distributed

### Part e - Interaction Terms

**Model Performance:**
- Base model R²: 0.8215
- **Significant interactions**:
  - Weight × Horsepower: p < 0.001
  - Displacement × Cylinders: p < 0.001

### Part f - Variable Transformations

**Comparison of Model Fits:**
- Base model Adj. R²: 0.8182
- Log transformations Adj. R²: 0.8491
- **Polynomial terms Adj. R²: 0.8610** ⭐ Best
- Square root transformations Adj. R²: 0.8289

**Best transformation**: Polynomial (improved fit by 0.043)

## Question 10

### Part a - Initial Model Fit
- **R²**: 0.2393
- **Significant predictors** (p < 0.05): `Price`, `US_Yes`

### Part b - Coefficient Interpretation

| Predictor | Coefficient | Interpretation |
|-----------|-------------|----------------|
| Intercept | 13.0435 | Expected sales for rural, non-US store at $0 price |
| Price | -0.0545 | Each $1 price increase decreases sales by 0.0545 units |
| Urban_Yes | -0.0219 | Urban stores have 0.0219 lower sales than rural stores |
| US_Yes | 1.2006 | US stores have 1.2006 higher sales than non-US stores |

### Part c - Model Equation

**General form:**
```
Sales = β₀ + β₁(Price) + β₂(Urban_Yes) + β₃(US_Yes) + ε
```

**Fitted equation:**
```
Sales = 13.0435 + (-0.0545)(Price) + (-0.0219)(Urban_Yes) + (1.2006)(US_Yes) + ε
```

**Store-specific equations:**
- **Rural, Non-US**: Sales = 13.0435 + (-0.0545)(Price) + ε
- **Urban, Non-US**: Sales = 13.0216 + (-0.0545)(Price) + ε  
- **Rural, US**: Sales = 14.2440 + (-0.0545)(Price) + ε
- **Urban, US**: Sales = 14.2221 + (-0.0545)(Price) + ε

### Part d - Hypothesis Testing

Testing H₀: βⱼ = 0 vs H₁: βⱼ ≠ 0 for each predictor (α = 0.05)

| Predictor | Coefficient | P-value | Decision |
|-----------|-------------|---------|----------|
| Price | -0.0545 | < 0.001 | **REJECT H₀** (significant) |
| Urban_Yes | -0.0219 | 0.936 | FAIL TO REJECT H₀ (not significant) |
| US_Yes | 1.2006 | < 0.001 | **REJECT H₀** (significant) |

**Summary**: Can reject H₀ for Price and US_Yes

### Part e - Model Reduction

**Model Comparison:**
- Full model Adj. R²: 0.2335
- **Reduced model Adj. R²: 0.2354** ⭐ Better

**Reduced model equation:**
```
Sales = 13.0308 + (-0.0545)(Price) + (1.1996)(US_Yes) + ε
```

### Part f - Model Fit Assessment

| Model | R² | Adj. R² | AIC |
|-------|-----|---------|-----|
| Full model | 0.2393 | 0.2335 | 1863.31 |
| **Reduced model** | 0.2393 | **0.2354** | **1861.32** |

**Conclusions:**
- Both models explain ~23.9% of variance in Sales (moderate explanatory power)
- **Reduced model preferred**: same explanatory power with fewer parameters
- Both models have limited predictive power (R² ≈ 0.24)

### Part g - Confidence Intervals

**95% Confidence Intervals:**

| Predictor | Estimate | 95% CI | Interpretation |
|-----------|----------|--------|----------------|
| Intercept | 13.0308 | [11.79, 14.27] | Baseline sales level |
| Price | -0.0545 | [-0.065, -0.044] | Each $1 increase decreases sales by 0.044 to 0.065 units |
| US_Yes | 1.1996 | [0.69, 1.71] | US stores have 0.69 to 1.71 higher sales than non-US stores |

*All intervals exclude 0, confirming statistical significance*

### Part h - Outlier Analysis

**Diagnostic Results:**
- **Outliers** (|std residual| > 2): 23 observations
- **High leverage points** (> 0.015): 20 observations

## Question 12

### Part a - Theoretical Result
The coefficient estimates are equal when X and Y have the same sum of squares: Σxᵢ² = Σyᵢ²

### Part b - Numerical Example (Different Coefficients)

**Regression Coefficients:**
- Y on X: 0.998788
- X on Y: 1.000962
- **Different**: True

**Verification:**
- β₁ × β₂ = 0.999749
- r² = 0.999026

### Part c - Numerical Example (Equal Coefficients)

**Regression Coefficients:**
- Y on X: 0.628904
- X on Y: 0.628904
- **Equal**: True

**Verification:**
- Sum of x²: 82.73
- Sum of y²: 82.73
- *Coefficients are equal when sum of squares are equal*
