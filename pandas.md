[toc]

# Pandas

### 随机抽样

```python
# 随机抽样
price.loc[price.sample(frac=0.2,axis=0).index,price.sample(frac=0.5,axis=1).columns]=np.nan
```

### 条件索引 np.where 

```python
df[col] = np.where(df[col]>200, 'high', 'low')
df[np.where(df>7)] # np.where返回的是神奇索引
```

```python
array.flatten() # 返回拷贝
array.ravel() # 返回视图
np.argsort() # 返回排序后的下标

#连接
np.hstack() np.c_[]
np.vstack()
```

```python
df.rename()传入字典修改index或columns
df.reindex()传入列表修改为列表中的index，并指定缺失值的填充逻辑
df.reset_index() 按层级恢复（取消）为默认索引
```



## 数据类型优化

### 读入数据的同时选择 dtype

https://www.kaggle.com/rohanrao/tutorial-on-reading-large-datasets

```python
column_types = {'acquisition_info': 'category', 'h_caught_stealing': 'float32'}
read_and_optimized = pd.read_csv('game_logs.csv',dtype=column_types,parse_dates=['date'],infer_datetime_format=True)
```

### 选择子列改变 dtype

```python
# 选取一类数据类型进行转换
df.select_dtypes(include=['object']).apply(pd.to_numeric, downcast='float')
```

### 使用 Categoricals 优化 object 类型

```python
ser = ser.astype('category')
```

### 转换成 datetime 类型

```python
df['date'] = pd.to_datetime(date,format='%Y%m%d')
df['date'] = pd.PeriodIndex(freq = 'Q')
```



### 常见困惑

- **`dropna` 操作的`thresh`参数:**

  thresh 指定的是有效值的个数, 可以乘上行数转换成有效值的比例

  见: [对thresh的理解](https://www.plus2net.com/python/pandas-dataframe-dropna-thresh.php)

### 参考

[华为云 Dataframe 优化](https://www.huaweicloud.com/articles/13c7fa4f76d6b44d17df77c08859ae65.html)

[catorgory 类型详细操作](https://www.yiibai.com/pandas/python_pandas_categorical_data.html)



## 有用的代码 Snippets

---

- **用于动态获取对应列的索引数值（iloc），可以对不同的df动态索引**

```python
col_names = "total_rooms", "total_bedrooms", "population", "households"
rooms_ix, bedrooms_ix, population_ix, households_ix = [
    housing.columns.get_loc(c) for c in col_names] # get the column indices
```

