# Grid Search

Grid search is the process of performing hyper parameter tuning in order to determine the optimal values for a given model. This is significant as the performance of the entire model is based on the hyper parameter values specified.

## Scikit Learn Implementation

```python
from sklearn.model_selection import GridSearchCV
gsc = GrdidSearchCV(estimator=my_estimator({some_params}),
                   param_grid = {
                     'C' : [],
                     'epsilon' : [],
                     'gamma'  : []
                   },
                   cv=5, scoring='neg_mean_squared_error', njobs=-1)
grid_result = gsc.fit(X, y)
best_params = grid_result.best_params_
best_estimator = my_estimator({necessary_params},
                             c=best_params['c'],
                             epsilon=best_params['epsilon'],
                             gamma=best_params['gamma'])

```

Here my_estimator is the model whose hyper parameter we are trying to tune. In the param_grid we pass the hyper-parameter and the range of values in which which we have to find the perfect combination for our estimator. Here we passed `c`, `gamma`, `epsilon` as an example for the estimator we are using.

With the tuning a cross validation process is also performed in order to determine the hyper parameter value set which provides the best accuracy levels.