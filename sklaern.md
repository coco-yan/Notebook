```python
# Explained variance score: 1 is perfect prediction
# and 0 means that there is no linear relationship
# between X and y.
>>> regr.score(diabetes_X_test, diabetes_y_test)
0.5850753022690...
```

- Occam’s razor: *prefer simpler models*

```python
#clear current figure
plt.clf()
```

- [3D plot](https://scikit-learn.org/stable/auto_examples/linear_model/plot_ols_3d.html)

```
#画出空间图形的表面
ax.plot_surface() 
```

