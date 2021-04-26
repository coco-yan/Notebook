# 虚拟环境

---

## python 创建虚拟环境

```shell
mkdir MyProject
cd MyProject
python -m venv venv
```

## conda创建虚拟环境

```shell
conda create -n env
```

### 关于jupyter使用多个环境的问题

详细见 [stackoverflow](https://stackoverflow.com/questions/39604271/conda-environments-not-showing-up-in-jupyter-notebook?answertab=votes#tab-top) 

- 在每个虚拟环境中都要安装`ipykernal` ，使用conda安装可能会出现killed问题，可以用pip

- 在运行jupyter的环境中安装`nb_conda_kernels`  

  ```shell
  conda install nb_conda_kernels  # 用于自动发现ipython内核
  ```

  