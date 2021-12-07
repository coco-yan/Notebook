# Matlab 笔记

[toc]

***Matlab 存储逻辑是按列优先存储！***



## 字符数组与字符串

---

字符串: **使用双引号**`tempText = "Temperature is " + c + "C"`

字符数组：**使用单引号**`seq = 'GCTAGAATCC'`, `seq2 = [seq 'ATTAGAAACC']`

字符串数组：`strlength(A)`



## 矩阵

---

### 索引

- 线性索引：`A(8)` 向下遍历每一列

### 删除

- `X(:,2) = []`

### find 函数返回的是索引



## 函数

---

- 主函数可以从定义这些函数的文件外（例如，从 MATLAB 命令行或从其他文件的函数中）调用，而局部函数则没有此功能。局部函数仅对其自己的文件中的主函数和其他局部函数可见。

- 不定参数的函数：`nargin` 和 `nargout` 为特殊变量，告知与函数的每次特定使用相关的输入和输出参数的数目

### lambda 函数

`f = @(arglist) expression`

`f = @(x) x.^2;`

### 句柄函数

- **句柄作为引用函数的一种方式,函数句柄通常在参数列表中传递给其他函数**

```matlab
%句柄函数 @(x) 表示x是自变量，尽量使用句柄函数
f = @(x) 2*X^2
```

```matlab
p = fminsearch(@humps, 0.5)
```

[关于句柄函数](https://ww2.mathworks.cn/help/matlab/learn_matlab/operations-on-nonlinear-functions.html)



## [数据分析](https://ww2.mathworks.cn/help/matlab/learn_matlab/data-analysis.html)

---

### 逻辑索引

```matlab
% 用逻辑索引删除缺少的数据，请使用 `isfinite(x)`
x = x(isfinite(x))
% 删除离群值
x = x(abs(x-mean(x)) <= 3*std(x))
```

### 滑动平均 convn 函数

```matlab
span = 3; % Size of the averaging window
window = ones(span,1)/span; 
smoothed_c3m = convn(c3m,window,'same');
```

### 频数统计

- `tabulate(x)`



 
