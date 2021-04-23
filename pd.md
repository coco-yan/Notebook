```python
# 随机抽样
price.loc[price.sample(frac=0.2,axis=0).index,price.sample(frac=0.5,axis=1).columns]=np.nan
```

```python
array.flatten() # 返回拷贝
array.ravel() # 返回视图
a[np.where(a>7)] # np.where返回的是神奇索引
np.argsort() # 返回排序后的下标

#连接
np.hstack()
np.vstack()
```

- <kbd>fillna</kbd> 填充可以使用字典来指定每一列填充的值

```
df.rename()传入字典修改index或columns
df.reindex()传入列表修改为列表中的index，并指定缺失值的填充逻辑
df.reset_index() 按层级恢复（取消）为默认索引
```

---

## matplotlib 

![image-20201230003907732](C:\Users\SHUHAN\AppData\Roaming\Typora\typora-user-images\image-20201230003907732.png) 

