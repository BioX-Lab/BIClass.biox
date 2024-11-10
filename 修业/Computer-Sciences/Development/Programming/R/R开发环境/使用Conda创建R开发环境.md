# 使用Conda创建R开发环境

## 写在前面
一般在官网（https://www.r-project.org/）下载相应R安装包、安装，可以直接使用R自带的开发环境，或者安装RStudio等IDE进行相应开发。

如果个人项目对R环境依赖性高，推荐利用Conda进行开发环境创建与维护。本文简要介绍使用Conda创建R开发环境（利用RStudio/Visual Studio Code/Jupyter Lab等IDE进行开发），以BIClass_py310环境为例。

```bash
### R
## r-base
conda install -c conda-forge r-base=4.4.1 -y

## r-essentials（可选）
conda install -c conda-forge r-essentials=4.4 -y

### 可以使用R控制台进行简单的开发、测试

### 选用Jupyter[BIClass项目默认IDE]
## jupyter
pip install jupyter -i https://pypi.tuna.tsinghua.edu.cn/simple

### 选用VS Code
## VS-Code
# Radian：R编辑器
pip install radian

### 选用RStudio
## RStudio
# Linux/MacOS
# conda install -c conda-forge rstudio-desktop -y
## Windows
# Windows中不推荐在conda环境中安装rstudio
# r::rstudio安装可能会存在冲突，可选择其它安装源
#conda install -c r rstudio -y
conda install -c rdonnelly rstudio -y
```

## Jupyter相关配置
进一步配置conda环境，在BIClass_py310环境环境中打开R，安装和配置IRkernel；之后可以新建notebook开发、测试相关代码。
``` R
## 安装IRkernel
install.packages('IRkernel')
## 将R内核注册到Jupyter
IRkernel::installspec()

```
### 安装Jupyter扩展

```bash
## 安装variableinspector
conda install -c conda-forge jupyterlab-variableinspector -y
```
## VS Code相关配置
> 以Windows系统为例。

依次安装VS Code插件：R Extension for Visual Studio Code、R Debugger等。

### 安装R包
```R
## 安装languageserver：实现代码自动补齐等
install.packages("languageserver")
## 安装httpgd
install.packages("httpgds")
```

### 配置Radian
1. 点开设置（`cmd + ,`）。
2. 输入`r.rterm.windows`，进行`Radian`配置，这里需要输入你的Radian路径（Radian路径可以通过`where radian`获取）。
3. 设置Bracketed Paste，输入`r.br`，启用Bracketed Paste。

### 配置httpgd
1. 点开设置（`cmd + ,`）。
2. 输入`r.plot.useHttpgd`，启用Httpgd。

### 快捷键设置（可选）
根据需要进行快捷键设置。

### 其它配置
1. 输入 `r.rterm.option`，删除`--no-save,--no-restore, --no-site-file`。
2. 输入r.sessionWatcher，勾选。可以实现绘图IDE，查看dataframe。如果想用原生绘图，取消勾选即可。
#### 配置Jupyter

如果在VS Code中使用Jupyter时，安装Jupyter插件。



#Conda #RStudio #VS-Code #R
