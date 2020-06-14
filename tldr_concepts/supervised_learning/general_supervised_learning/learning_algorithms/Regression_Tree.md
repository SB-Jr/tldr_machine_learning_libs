# Regression Tree

Basics of Decision Tree has been covered <a hre='https://github.com/SB-Jr/machine_learning_concepts/blob/master/learning_algorithms/Decision_Tree.md'>here</a>.

Like in decision trees we tried to define a cost function and then minimie it by finding a split which has the least cost function value, in Regression Trees we have **Residual Sum of Squares(RSS)** as the cost function.

$\begin{align} \Large \tag{1} RSS = \sum_{j=1}^J \sum_{i\in R_j} (y_i - \hat{y}_{R_j})^2 \end{align}$

Here our goal is to find the high-dimensional rectangles $R_1, R_2,....R_J$ that minimises RSS where $\hat{y_{R_j}}$ is the mean response for the training observation within the $j^{th}$ box.

 

> If we give a good look at the formula for RSS, we can infer that minimising RSS means, finding clusters of y’s such that they are very near to their mean value, i.e. finding clusters or hyper-rectangles such that the target values it encompasses are near to their mean and so predicting the mean is more accurate for that hyper-rectangle.



We can create trees 2 ways:

-  Create a tree until RSS crosses a threshold
  - But might result in bad trees as split in early node can be bad resulting in bad decisions
- Create a large tree and then prune it 
  - We can prune the tree as discussed in Decision Tree, i.e. by cross checking each node’s importance with a validation set. Removing the nodes which doesn’t give much of a good result on validation set. This way the tree will not be too biased.

The splitting of dataset into binary groups and then recursively doing this process until we reach an end(either crossing a threshold or sample being too small at leaf node) is known as **Recursive Binary Splitting(RBS)** or **Binary Recursive Partitioning **.



In Regression tree, the continuity of the result is achieved by predicting the mean of the target values in a region `m`, i.e. for the region `m` the prediction will be the mean of y’s or target values in that region.



## Weakest link Pruning

We can prune from the leaf nodes to the root by following a simple procedure

Starting with $T_0$ substitute a subtree with a leaf to obtain $T_1$ by minimizing:

$\begin{align} \large \tag{2} \frac{RSS(T_1) - RSS(T_0)}{|T_0| - |T_1|} \end{align}$

Iterate this pruning to obtain a sequence $T_0, T_1, ......T_m$ where $T_m$ is the null tree. Now select the optimal $T_i$ by cross validation.

**Remember:** We start from the leafs and then proceed to the root.



## Cost-Complexity Pruning

Cost complexity pruning generates a series of trees $T_0, ...... T_m$ where $T_0$ is the initial tree and $T_m$ is the null tree. At any given step $i$, the tree is created by removing a subtree from $i-1$ and replacing it with a leaf node with value chosen as in the tree building algorithm. 

Here we introduce a new hyper-parameter $\alpha$ , that balances the depth of the tree. We try to minimise: 

$\begin{align} \Large \tag{3} \sum_{m=1}^{|T|} \sum_{x_i \in R_m}(y_i - \bar{y}_{R_m})^2 + \alpha* |f(T)| \end{align}$

When $\alpha = \infty $ , we select the null tree and

when $\alpha = 0$ , we select the full tree

The solution to each $\alpha$ gives us the trees $T_1, T_2,......T_m$ from the weakest link pruning. We then choose the optimal $\alpha$ corresponding to the optimal $T_i$ by cross validation.

Here we use the K-Fold cross validation to check each tree, in place of using a single set as our cross validation set.