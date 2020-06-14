# PCA (Principal Component Analysis)

The best features that we can have for creating a model and work best with a target variable ares:

- **High Variance**
- **Uncorrelated:** features that are highly correlated with each other are less useful and in certain cases downright harmful. 
- **High Correlation with Target**

PCA (Principal Components Analysis) gives us our ideal set of features. **It creates a set of principal components that are rank ordered by variance** (the first component has higher variance than the second, the second has higher variance than the third, and so on)**, uncorrelated, and low in number** (we can throw away the lower ranked components as they contain little signal).

