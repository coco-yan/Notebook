[toc]

# 2. End-to-End ML Project



## Get the Data 

### 1. Take a Quick Look at the Data Structure

1. data.head()、data.info()、data.value_counts()
2. data.hist()  查看数值型 feature 的直方图

- 我们可以发现有些值经过了 scale 和 **capped** 处理，所以在对应最大值处的频率较高
- 很多 histograms 是 **tail-heavy** 的，导致很多算法很难 detect patterns。我们要将这些变量转换为更像 **bell-shaped** 的分布，for example **Compute their logarithm**。

### 2. Create a Test Set

- warning: 在进一步查看 data 前应该创建 test set

  - 抽样时候注意对重要的特征进行分层抽样，防止出现 Sample Bias

    ```python
    from sklearn.model_selection import StratifiedShuffleSplit
    
    split = StratifiedShuffleSplit(n_splits=1, test_size=0.2, random_state=42)
    for train_index, test_index in split.split(housing, housing["income_cat"]):
        strat_train_set = housing.loc[train_index]
        strat_test_set = housing.loc[test_index]
    ```



## Discover and Visualize the Data to Gain Insight

### 1. Visualizing Data

- scatter plot `housing.plot(kind="scatter", x="longitude", y="latitude", alpha=0.1)`

  其中 $\alpha$ 指定高密度区域突出，低密度区域淡化

  ```python
  housing.plot(kind="scatter", x="longitude", y="latitude", alpha=0.4,
               s=housing["population"]/100, label="population", figsize=(10,7),
               c="median_house_value", cmap=plt.get_cmap("jet"), colorbar=True,
               sharex=False)
  plt.legend()
  ```



### 2. Looking for Correlations

- data.corr( )

  - 注意 corr 等于 0 只能说明无线性相关性，可能存在非线性的相关性




- scatter_matrix( )

  > plot every numerical attribute against every other numerical attribute，plus a histogram of each numerical attribute

  ```python
  from pandas.plotting import sctter_matrix
  scatter_matrix(data[], figsize=(12,8))
  ```

- heatmap

```python
plt.figure(figsize=(8,8))
sns.heatmap(corr_matrix, vmin=-1,vmax=1,center=5, fmt='.1f',annot=True)
#annot显示注释
#fmt显示注释数字格式
#center 颜色 The value at which to center the colormap when plotting divergant data
```

<img src="\note.assets\heatmap.png" alt="heatmap"  />

### 3. Experimenting with Attribute Combinations

- **Iterative:** 
  
  - this round of exploration **doesnt have to be thorough**; the point is to start off on the right foot and gain qucik insight to form a good **prototype**. 
  - **Analyze output to gain insight and come back again**.
  
  **构造特称，查看特征与 label 之间的相关性**
  
  

## Prepare the Data for Machine Learning Algorithms

### 1. Data Cleaning

1. 填充缺失值
   - 在 training set 上计算中位数并 **保存**，用于填充 test set 和 new data

   - 可以使用 **SimpleImputer** 方便地处理缺失值

     ```python
     from sklearn.impute import SimpleImputer
     imputer = SimpleImputer(strategy="median") 
     imputer.fit()
     ### imputer.statistics_ 保存了每个特征的统计结果
     ### 注意！transform 结果是一个numpy或scipy矩阵
     ```

2. **处理 text 和 Categorical**

   - OrdinalEncoder

     **assum two nearby values  are more similar than two distant values.** Fine for categories like “bad, average, bad”. 

   - OneHotEncoder

     











## Classification

- 很多数据集里的标签是string，需要转换成numbers

### Performance Measures

### Measuring Accuracy Using Cross-Validation

$$
Precision = \frac{TP}{TP + FP}
$$

$$
Recall(sensitivity)(TPR) = \frac{TP}{TP+FN}
$$

$$
F_1 score = \frac{2}{\frac{1}{precision} + \frac{1}{recall}} = \frac{TP}{TP + \frac{FN+FP}{2}}
$$

#### $F_1 score$:

Favors classifiers that have similar precision and recall. This is not always what you want: in some contexts you mostly care about **precision**, and in other contexts you really care about **recall**.

### Precision/Recall Trade-off

`from sklearn.metrics import precision_recall_curve` 

![image-20210515201420475](\note.assets\image-20210515201420475.png)

### The ROC  Curve and AUC score

![image-20210515202637814](\note.assets\image-20210515202637814.png)

#### **Trade off ** 

higher the recall (TPR), the more false positives (FPR) the classifier produces

#### A rule of thumb 

you should prefer the PR curve whenever the positive class is rare or when you care more about the false positives than the false negatives. Otherwise, use the ROC curve. 

