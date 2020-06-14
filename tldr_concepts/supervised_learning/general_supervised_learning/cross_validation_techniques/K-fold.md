# K-Fold Cross Validation

 ## **Problem**

Usually, we split the data set into training and testing sets and use the training set to train the model and testing set to test the model. We then evaluate the model performance based on an error metric to determine the accuracy of the model. This method however, is not very reliable as the accuracy obtained for one test set can be very different to the accuracy obtained for a different test set.

## Solution

K-Fold CV is where a given data set is split into a **K** number of sections/folds where each fold is used as a testing set at some point.

So, in 1st itteration, the 1st fold is used to test the model and other K-1 folds are used to train the model. In the 2nd itteration, the 2nd fold is used to test the model and the 1st fold and the remaining K-2 folds are used to train the model and so on…



> *A poorly chosen value for k may result in a mis-representative idea of the skill of the model, such as a score with a high variance (that may change a lot based on the data used to fit the model), or a high bias, (such as an overestimate of the skill of the model).*



Three common tactics for choosing a value for k are as follows:

- **Representative**: The value for k is chosen such that each train/test group of data samples is large enough to be statistically representative of the broader dataset.
- **k=10**: The value for k is fixed to 10, a value that has been found through experimentation to generally result in a model skill estimate with low bias a modest variance.
- **k=n**: The value for k is fixed to n, where n is the size of the dataset to give each test sample an opportunity to be used in the hold out dataset. This approach is called leave-one-out cross-validation.



> “*As k gets larger, the difference in size between the training set and the resampling subsets gets smaller. As this difference decreases, the bias of the technique becomes smaller*“



# Scikit Implementation

```python
from sklearn.model_selection import KFold
kfold = KFold(n_splits=10, andom_state=42, shuffle=True)
for train_index, test_index in kfold.split(X):
  model.fit(X[train_index], y[train_index])
  print(model.evaluate(X[test_index], y[test_index]))
```

 

------

# K-fold != Batch Normalization

This is not to be confused with batch normalization, as in batch normalization even though it breaks the dataset into batches like in K-Fold, but 

-  None of the batches is even once used for cross validation
- all K-1 folds used for training can be either used 1 at a time (i.e. not in batches or batch_size = 1) or in batches inside the model.

K-fold is jst to split the data before it is given to the model for fitting while batch normalization is used inside the model after data is given to it.