## sklearn

---

- **估计器做完拟合来预测，而转换器做完拟合来转换。**

  1. 将分类型变量 (categorical) 编码成数值型变量 (numerical)

  2. 规范化 (normalize) 或标准化 (standardize) 数值型变量

- **特征缩放**

  ​	 数据要做的最重要的转换之一是特征缩放 (feature scaling)。当输入的数值的量刚不同时，机器学习算法的性能都不会好。

  - 标准化 (standardization)：每个维度的特征减去该特征均值，除以该维度的标准差。

  - 规范化 (normalization)：每个维度的特征减去该特征最小值，除以该特征的最大值与最小值之差。

    <img src="https://ss.csdn.net/p?https://mmbiz.qpic.cn/mmbiz_png/e4kxNicDVcCG8Qqr40b4vh0Uc9XdXCdktVicicQ2uzAgYu2ia6Cial7lUb9MWThOTGb6m2kNIGGeiaicEZunYeSJaFJicQ/640?wx_fmt=png" alt="img" style="zoom:150%;" />

---

**Model Selection 估计器**

模型选择 (Model Selction) 在机器学习非常重要，它主要用于评估模型表现，常见的 Model Selection 估计器有以下几个：

- `cross_validate`: 评估交叉验证的表现。
- `learning_curve`: 建立学习曲线。  
- `GridSearchCV`: 用交叉验证从网格中一组超参数搜索出最佳超参数。
- `RandomizedSearchCV`: 用交叉验证从一组随机超参数搜索出最佳超参数。

最大树深、最多特征数、最小可分裂样本数、和分裂标准

**回归**模型可预测连续值。例如，回归模型做出的预测可回答如下问题：

- 加利福尼亚州一栋房产的价值是多少？
- 用户点击此广告的概率是多少？

**分类**模型可预测离散值。例如，分类模型做出的预测可回答如下问题：

- 某个指定电子邮件是垃圾邮件还是非垃圾邮件？

- 这是一张狗、猫还是仓鼠图片？

  对于分类的预测器而言：

  1. 对于分类问题，我们不仅想知道预测的类别是什么，有时还想知道预测该类别的信心如何。前者用 predict()，后者用 predict_proba()

  2. score() 返回的是分类准确率
  3. decision_function() 返回的是每个样例在每个类下的分数值

---

**均方误差** (**MSE**) 指的是每个样本的平均平方损失。要计算 MSE，请求出各个样本的所有平方损失之和，然后除以样本数量

权重初始化

- 对于凸型问题，权重可以从任意地方开始，神经网络不适用

- SDG和小批量梯度下降

梯度下降法算法用梯度乘以一个称为**学习速率**（有时也称为**步长**）的标量，以确定下一个点的位置