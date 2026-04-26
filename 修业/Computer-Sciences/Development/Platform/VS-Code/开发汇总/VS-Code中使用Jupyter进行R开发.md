# VS-Code中使用Jupyter进行R开发
Jupyter 不只用来运行 Python Notebook。在 VS Code 中，也可以用 Jupyter 进行 R 的交互式开发，包括直接使用 `.ipynb` 笔记本，或者在合适的环境中运行 R 内核。
如果已经在 VS Code 中配置好了 R 环境，那么再加上 Jupyter 支持后，就可以形成一套适合数据分析、统计建模和可视化探索的 R 交互式工作流。如果希望统一管理 Python、R 与 Jupyter，使用 **Conda** 来准备 R 环境通常会更省心，也更便于隔离项目依赖。
## 安装 VS Code 扩展
打开 VS Code 扩展面板，安装以下扩展：
- Python
- Jupyter
- R
一般建议优先使用以下扩展：
- Microsoft 发布的 Python 扩展
- Microsoft 发布的 Jupyter 扩展
- REditorSupport 发布的 R 扩展
安装完成后，VS Code 才能更方便地：
- 识别 `.ipynb` 文件
- 在编辑器中运行 Notebook 单元
- 选择和切换 Jupyter 内核
- 提供 R 语言基础编辑支持
- 配合 R 终端进行代码运行和调试
## 准备 R 环境
要在 VS Code 中通过 Jupyter 使用 R，核心是让当前 R 环境具备 **Jupyter 内核** 能力，通常这依赖 `IRkernel`。
准备方式大致有两种：
- 直接使用系统安装的 R，再额外安装 `IRkernel`。
- 使用 **Conda 环境**统一安装和管理 R、Jupyter 与相关依赖
如果已经有比较成熟的 Conda 工作流，通常更建议第二种方式。
### 使用系统安装的 R
先确认系统中已经安装 R：
``` bash
R --version
```
如果能正常显示版本信息，说明 R 已经可用。
然后进入 R 终端，安装 `IRkernel`：
``` r
install.packages("IRkernel")
```
安装完成后，把它注册为 Jupyter 内核：
``` r
IRkernel::installspec()
```
注册完成后，VS Code 的 Jupyter 内核列表中通常就会出现 R 相关选项。
### 使用 Conda 准备 R 环境
如果希望把 R、Jupyter、IRkernel 和项目依赖放到同一个隔离环境里，推荐使用 Conda。这样做可以：
- 环境隔离更清晰
- 项目依赖更容易复现
- 更适合同时混用 Python 和 R
- 更方便在 VS Code 中切换不同项目环境
- 出问题时更容易定位是环境问题还是代码问题
#### 创建 Conda 环境
建议按项目创建独立环境。例如：
``` bash
conda create -n r-jupyter-dev -c conda-forge r-base r-irkernel jupyter
```
如果还希望这个环境也能顺手运行一些常见 R 分析任务，也可以一起装一些常用包：
``` bash
conda create -n r-jupyter-dev -c conda-forge r-base r-irkernel jupyter r-tidyverse r-data.table r-ggplot2
```
创建完成后，激活环境：
``` bash
conda activate r-jupyter-dev
```
#### 检查 R 是否可用
激活环境后，检查 R 版本：
``` bash
R --version
```
再检查 Jupyter 是否可用：
``` bash
jupyter --version
```
如果都能正常输出，说明这个 Conda 环境已经具备基础条件。
#### 在 Conda 环境中补充安装 R 包
如果环境创建时没有一次性装完，也可以激活环境后再安装：
``` bash
conda install -c conda-forge r-irkernel r-tidyverse r-data.table r-ggplot2
```
如果某些包 Conda 中没有，或者你就是希望从 R 官方仓库安装，也可以在激活该环境后进入 R：
``` r
install.packages("包名")
```
这样安装的包也会进入当前 Conda 环境对应的 R 库中。
#### 注册 R 内核
很多情况下，安装 `r-irkernel` 后，Jupyter 已经能够识别 R 内核。但如果 VS Code 中仍然看不到 R 内核，可以在激活 Conda 环境后进入 R，手动执行：
``` r
IRkernel::installspec()
```
如果想更明确地注册到当前用户，也可以这样：
``` r
IRkernel::installspec(user = TRUE)
```
## 在 VS Code 中使用 R 内核
打开 VS Code 后，可以直接新建或打开一个 `.ipynb` 文件。
### 新建 Notebook
在 VS Code 中可以：
- `Ctrl + Shift + P`
- 输入 `Create: New Jupyter Notebook`
或者直接新建一个 `.ipynb` 文件。
### 选择 R 内核
打开Notebook后，点击右上角的内核选择区域，选择已经注册好的 R 内核，例如：
- `R`
- 带有具体版本信息的 R kernel
- 与某个 Conda 环境关联的 R 内核
如果看不到 R 内核，通常说明：
- `IRkernel` 还没有安装
- `IRkernel::installspec()` 还没有执行
- VS Code 没有正确识别本地 Jupyter 环境
- 当前系统里的 Jupyter 组件不完整
- 你当前打开的并不是准备好 R 内核的那个环境
## 直接使用 `.ipynb` Notebook
### 编写并运行单元
Notebook 以单元为单位执行。可以把 R 代码分块写在不同单元中，例如：
``` r
x <- 1:10
x
```
再新建一个单元：
``` r
mean(x)
```
运行后，输出会直接显示在单元下面。
### 一个简单示例
下面给一个最常见的 R 数据分析示例：
``` r
df <- data.frame(
  name = c("A", "B", "C", "D"),
  score = c(80, 92, 75, 96)
)
df
```
再运行：
``` r
mean(df$score)
```
再画图：
``` r
barplot(df$score, names.arg = df$name, col = "steelblue")
title("Scores")
```
## 推荐实践
如果你打算长期在 VS Code 中使用 Jupyter 进行 R 开发，比较推荐：
- 优先按项目创建独立 Conda 环境
- 在同一环境中统一安装 R、Jupyter、IRkernel 和项目依赖
- 探索阶段优先使用 Notebook
- 稳定后将逻辑整理为 `.R` 脚本
- 尽量减少系统 R、Conda R、多个 Jupyter 安装混用

#VS-Code #Jupyter #R #Conda