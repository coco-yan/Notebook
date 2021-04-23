## Missing values

`from sklearn.preprocessing import Imputer`

## categorical Variables

- Label 
- One-Hot Encoding

## Pipelines

## Cross-Validation

## XGBoost parameters

1.  n_estimators

   - 循环次数，等于在ensemble中加入的模型数目
   - 过低underfitting，过高overfitting。typical value 100-1000 。
2.  early_stopping_rounds

   - 出现几次score退化之后自动停止
   - reasonable choice =5
3. learning rate

   - we can multiply the predictions from each model by a small number before adding them in

   - In general, a small learning rate and large number of estimators will yield more accurate XGBoost model
   - As default, XGBoost sets `learning_rate=0.1`
4.  n_jobs
    - On larger datasets where runtime is a consideration, you can use parallelism to build your models faster. It's common to set the parameter `n_jobs` equal to the number of cores on your machine. On smaller datasets, this won't help.

## Data Leakage

- target leakage
- train-test contamination

# Categorical Encodings

