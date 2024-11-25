# 使用Conda创建程序运行环境

Conda 是一种常用的包和环境管理器，支持包括Python、R在内的多种编程语言，在Python程序开发中应用广泛。根据使用的操作系统可选择相应版本的Anaconda (https://anaconda.org/, 推荐) 或 Miniconda安装Conda。
Anaconda安装后，在终端（命令行）中即可运行conda命令。在进行程序开发或者安装、使用相关（复杂）软件、流程时，可以先通过conda命令为其创建运行环境，conda的详细用法可以通过conda --help查阅帮助文档等途径学习。
这里创建一个名为"BIClass_py310"的conda环境，用于后续BIClass.biox项目的开发（默认运行环境）。不同项目的conda环境尽量独立（隔离）。
```bash
## 如下命令在不同的操作系统中相同
# 创建BIClass_py310 conda环境，指定Python 3.10
conda create -n BIClass_py310 python=3.10 -y

# 激活新创建的conda环境
conda activate BIClass_py310

# 使用pip安装 jupyter(-i 指定安装源，适配国内网络环境)，用于Jupyter Notebook相关操作
pip install jupyter -i https://pypi.tuna.tsinghua.edu.cn/simple

# 其它包在需要时进行安装
```

#Conda