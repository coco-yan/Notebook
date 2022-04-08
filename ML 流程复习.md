## ML 流程复习
[toc]
---

### Concept
**Mutual Information:** Pearson相关系数只能描述数据间的线性相关关系，而互信息能描述任何关系，常用于**决策树节点分裂**，**特征选择:** 
`mutual_info_regression`: *for real-valued targets*, `mutual_info_classif`: *for categorical targets* 
> It is closely linked to the concept of entropy. This is because it can also be known as the reduction of uncertainty of a random variable if another is known. Therefore, a high mutual information value indicates a large reduction of uncertainty whereas a low value indicates a small reduction. If the mutual information is zero, that means that the two random variables are independent.
In theory there's no upper bound to what MI can be. In practice though values above 2.0 or so are uncommon. (Mutual information is a logarithmic quantity, so it increases very slowly.)

$$ I(X;Y) = \int_{Y}\int_{X} p_{(X,Y)}(x,y) \cdot log\left(\frac{p_{(X,Y)}(x,y)}{p_{X}(x)p_{Y}(y))} \right ) dxdy$$

$$\begin{align*}  
I(X; Y) & =  H(X) – H(X|Y) \\   
& = H(Y) – H(Y|X)   \\  
& = H(X) + H(Y) – H(X,Y)  \\  
& = H(X,Y) – H(X|Y) – H(Y|X)  
\end{align*} $$

Entropy (H) measures the level of expected **uncertainty** in a random variable. Therefore, H(X) is approximately how much information can be learned of the random variable X by observing just one sample.    

$$H(X) = -\sum_{x_{i}\in X}P(X=x_{i})\cdot log(P(X=x_{i}))$$

![](./pic/mutual%20infomation.png)

> **Notice:** 
>- It's possible for a feature to be *very informative when interacting with other features*, but not so informative all alone. MI can't detect interactions between features. It is a univariate metric. **Domain knowledge can offer a lot of guidance here**
> - The actual usefulness of a feature depends on the model you use it with. A feature is only useful to the extent that its relationship with the target is one your model can learn. Just because a feature has a high MI score doesn't mean your model will be able to do anything with that information. You may need to transform the feature first to expose the association.

<https://quantdare.com/what-is-mutual-information/> 
<https://www.kaggle.com/code/ryanholbrook/mutual-information>  



### Feature Engineering


#### Creating Features
1. **Mathematical Transform**
    - Interaction with a Categorical
2. **Counts**
3. **Building-up and breaking-down features**
4. **Group Transforms:** *group counts, mean, ratio...*
5. **Add `Clustering labels/Cluster-Distance` with K-means**
 whether and how to rescale features is rarely automatic -- it will usually depend on some domain knowledge about your data and what you're trying to predict. Comparing different rescaling schemes through cross-validation can also be helpful. 
  
    Features | rescaling or not
    --|--|--
    `Latitude` and `Longitude` of cities in California | No
    `Lot Area` and `Living Area` of houses in Ames, Iowa | Yes/No
    `Number of Doors` and `Horsepower` of a 1989 model car | Yes and must


6. **PCA**: partitioning of the variation in the data
    > - **Applied to standerlized data**:  With standardized data - - "variation" means "correlation".
    > - new features are called the `principal components` of the data. The weights themselves are called `loadings`.
    > - PCA tells us the amount of variation in each component

    two ways you could use PCA for feature engineering.
    1. **descriptive technique**
    compute the MI scores for the components and see what kind of variation is most predictive of your target. That could give you ideas for kinds of features to create -- a product of `Height` and `Diameter` if `Size` is important, say, or a ratio of `Height` and `Diameter` if Shape is important.
        - **the signs and magnitudes of a component's loadings tell us what kind of variation it's captured.** 生成loadings的df时记得转置（方便看）`pca.components_.T`

    2. **use the components themselves as features**
        - Dimensionality reduction
        - Anomaly detection / Outlier detection
            ```python
            sns.catplot(
            y="value",
            col="variable",
            data=X_pca.melt(),
            kind='boxen',
            sharey=False,
            col_wrap=2, );
            ```
        - Noise reduction
        - Decorrelation
7. **Target Encoding**
    Use Case:
    - **High-cardinality features**
    - **Domain-motivated features**

    <https://www.kaggle.com/code/ryanholbrook/principal-component-analysis>
1. Mathematical Transform
    - Interaction with a Categorical
2. Counts
3. Building-up and breaking-down features
4. Group Transforms: *group counts, mean, ratio...*
5. Add `Clustering labels/Cluster-Distance` with K-means
 whether and how to rescale features is rarely automatic -- it will usually depend on some domain knowledge about your data and what you're trying to predict. Comparing different rescaling schemes through cross-validation can also be helpful. 
    
    Features | rescaling or not
    --|--|--
    `Latitude` and `Longitude` of cities in California | No
    `Lot Area` and `Living Area` of houses in Ames, Iowa | Yes/No
    `Number of Doors` and `Horsepower` of a 1989 model car | Yes and must


6. **PCA**: partitioning of the variation in the data
    > - **Applied to standerlized data**:  With standardized data - - "variation" means "correlation".
    > - new features are called the `principal components` of the data. The weights themselves are called `loadings`.
    > - PCA tells us the amount of variation in each component

    two ways you could use PCA for feature engineering.
    1. **descriptive technique**
    compute the MI scores for the components and see what kind of variation is most predictive of your target. That could give you ideas for kinds of features to create -- a product of `Height` and `Diameter` if `Size` is important, say, or a ratio of `Height` and `Diameter` if Shape is important.
        - **the signs and magnitudes of a component's loadings tell us what kind of variation it's captured.** 生成loadings的df时记得转置（方便看）`pca.components_.T`

    2. **use the components themselves as features**
        - Dimensionality reduction
        - Anomaly detection / Outlier detection
            ```python
            sns.catplot(
            y="value",
            col="variable",
            data=X_pca.melt(),
            kind='boxen',
            sharey=False,
            col_wrap=2, );
            ```
        - Noise reduction
        - Decorrelation
7. **Target Encoding**
    - Use Case:
        - **High-cardinality features**
        - **Domain-motivated features**
    - How(`from category_encoders import MEstimateEncoder`)
        - Create the encoding and training splits and fit the encoder
        `encoder = MEstimateEncoder(cols=["Zipcode"], m=5.0)`

    <https://www.kaggle.com/code/ryanholbrook/principal-component-analysis>

---


### Code Snippets
#### Method
`X,y = df.pop(colname)`: 删除colname列，返回删除后的X，和colname列
`df.gt() -> boolen`: built-in greater-than method, `df.gt(0.0).sum(axis=1)`
`df.factorize()`: 生成`Label-Encoding`
`df.select_dtypes(["object"]).nunique()`: 计算object中唯一类别的数量




#### Snippets
```python
# 将字符串分离成两列    
customer[["Type", "Level"]] = (  # Create two new features
    customer["Policy"]           # from the Policy feature
    .str                         # through the string accessor
    .split(" ", expand=True)     # by splitting on " "
                                 # and expanding the result into separate columns
)
```

```python
# 计算Mutual Information并可视化
def make_mi_scores(X, y):
    X = X.copy()
    for colname in X.select_dtypes(["object", "category"]):
        X[colname], _ = X[colname].factorize()
    # All discrete features should now have integer dtypes
    discrete_features = [pd.api.types.is_integer_dtype(t) for t in X.dtypes]
    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features, random_state=0)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores

def plot_mi_scores(scores):
    scores = scores.sort_values(ascending=True)
    width = np.arange(len(scores)) # 每个bar的y的起始位置
    ticks = list(scores.index)
    plt.barh(width, scores)
    plt.yticks(width, ticks)
    plt.title("Mutual Information Scores")
```

```python
# 多个类别相关关系散点图，hue为聚类类别
sns.relplot(
    x="value", y="SalePrice", hue="Cluster", col="variable",
    height=4, aspect=1, facet_kws={'sharex': False}, col_wrap=3,
    data=Xy.melt(
        value_vars=features, id_vars=["SalePrice", "Cluster"],
    ),
);
```

```python
# Explained Variance and Cumulative Variance
def plot_variance(pca, width=8, dpi=100):
    # Create figure
    fig, axs = plt.subplots(1, 2)
    n = pca.n_components_
    grid = np.arange(1, n + 1)
    # Explained variance
    evr = pca.explained_variance_ratio_
    axs[0].bar(grid, evr)
    axs[0].set(
        xlabel="Component", title="% Explained Variance", ylim=(0.0, 1.0)
    )
    # Cumulative Variance
    cv = np.cumsum(evr)
    axs[1].plot(np.r_[0, grid], np.r_[0, cv], "o-")
    axs[1].set(
        xlabel="Component", title="% Cumulative Variance", ylim=(0.0, 1.0)
    )
    # Set up figure
    fig.set(figwidth=8, dpi=100)
    return axs
```

```python
# rmParams setting 
plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
```

### Misunderstandings
**Scaling and Normalization:**`zscore`是scaling方法，不会改变数据的分布，`scipy.stats: cox-box`是将数据转换为正态分布的方法，`log`也是常用的方法