# VS Code中使用Jupyter进行Python开发

Jupyter 不只是浏览器里的 Notebook。在 VS Code 中，也可以直接使用 `.ipynb` 笔记本或带有 `# %%` 单元标记的 `.py` 文件进行交互式开发。如果已经在 VS Code 中配置好了 Python 环境（这里以Conda创建的虚拟环境为例），再加上 Jupyter 支持后，基本就可以形成一套完整的 Python 交互式开发工作流。

## 安装 VS Code 扩展
打开 VS Code 扩展面板，安装以下扩展：
- Python
- Jupyter
一般由 Microsoft 发布，安装量很高，直接搜索即可。安装完成后，VS Code 才能：
- 识别 `.ipynb` 文件
- 在编辑器中运行 Notebook 单元
- 支持 `.py` 文件中的交互式单元
- 选择和切换 Jupyter 内核
## 准备 Python 环境
可以使用系统 Python，也可以使用 Conda 环境。  如果是日常项目开发，通常更推荐 Conda 或 venv，避免不同项目之间相互污染。
### 使用 Conda 创建环境

例如创建一个用于 Jupyter 开发的环境：
``` bash
conda create -n py-jupyter python=3.11 -y
```
激活环境：
``` bash
conda activate py-jupyter
```
安装常用包：
``` bash
conda install ipykernel
# 或者 mamba install ipykernel
```
或者使用 `pip`：
``` bash
pip install ipykernel
```
如果还要做数据分析等，可根据需求安装：
``` bash
pip install numpy pandas matplotlib seaborn
```
## 在 VS Code 中选择 Python 解释器
打开 VS Code 后，按以下方式选择解释器：
- 按 `Ctrl + Shift + P`
- 输入 `Python: Select Interpreter`
- 选择你刚创建的环境
例如：
- `conda (py-jupyter)`
- 或对应环境中的 `python.exe`
如果解释器选错了，后面 Jupyter 内核通常也会混乱，比如：
- 包明明安装了却导入失败
- Notebook 运行时找不到模块
- VS Code 中显示的内核和终端环境不一致
## 安装并注册 ipykernel
虽然有时 VS Code 会自动提示安装，但更推荐手动确认当前环境中已经安装 `ipykernel`。
``` bash
pip install ipykernel
# 或者 mamba install ipykernel
```
为了让该环境更清晰地出现在 Jupyter 内核列表中，需要手动注册：
``` bash
python -m ipykernel install --user --name py-jupyter --display-name "Python (py-jupyter)"
```
注册后，在 VS Code 的 Jupyter 内核列表里更容易识别这个环境。
## 两种常见使用方式
在 VS Code 中，Jupyter 开发主要有两种方式：
- 直接使用 `.ipynb` 文件
- 在 `.py` 文件中使用 `# %%` 单元
## 直接使用 `.ipynb` Notebook
### 新建 Notebook
在 VS Code 中可以：
- `Ctrl + Shift + P`
- 输入 `Create: New Jupyter Notebook`
或者直接新建一个 `.ipynb` 文件。
### 选择内核
打开 Notebook 后，右上角通常会显示内核选择区域。  
点击后选择你当前项目对应的环境，例如：
- `Python (py-jupyter)`
### 编写并运行单元
Notebook 以单元为单位执行。可以把代码分块写入不同单元，例如：
``` python
import numpy as np
import pandas as pd

print("hello jupyter")
```
再新建一个单元：
``` python
x = np.arange(10)
x
```

运行后，输出会直接显示在单元下面。

### 适合的场景
`.ipynb` 方式更适合：

- 教学演示
- 数据探索
- 可视化分析
- 临时实验
- 需要保留输出结果的场景
## 在 `.py` 文件中使用交互式单元
也可以把代码保存在普通 Python 文件中，便于：
- 更容易纳入 Git 管理
- 更适合工程化开发
- 文件结构更清晰
- 可同时兼顾脚本运行和交互调试
### 使用 `# %%` 分隔代码单元
在 Python 文件中写：
``` python
# %%
import numpy as np
import matplotlib.pyplot as plt

# %%
x = np.linspace(0, 10, 100)
y = np.sin(x)

# %%
plt.plot(x, y)
plt.show()
```
### 运行单元

当 VS Code 识别到 `# %%` 后，单元上方通常会出现：
- Run Cell
- Run Below
- Debug Cell
点击即可运行。运行结果通常会出现在：
- Interactive Window
- 或 Jupyter 相关输出面板中
### 这种方式的优点
- 保留 `.py` 的可维护性
- 仍然能获得 Notebook 风格的分块执行体验
- 更适合逐步实验后整理成正式脚本
- 对版本控制更友好
如果平时既写分析代码，又希望代码最后能沉淀为正式项目文件，这种方式通常非常合适。

### 一个简单示例

下面给一个最常见的交互式数据分析例子。

``` python
# %%
import pandas as pd
import matplotlib.pyplot as plt

# %%
df = pd.DataFrame({
    "name": ["A", "B", "C", "D"],
    "score": [80, 92, 75, 96]
})

df

# %%
df["score"].plot(kind="bar")
plt.title("Scores")
plt.show()

# %%
df["score"].mean()
```
这个例子可以体现 Jupyter 工作流的特点：
- 先构造数据
- 再查看数据
- 再画图
- 再做统计
- 每一步都可以立即看到结果
## 如何选择内核
在 Notebook 或 Interactive Window 中，内核选择非常关键。
如果代码运行报错，比如：
``` python
ModuleNotFoundError: No module named 'pandas'
```
通常优先检查：
- 当前内核是不是你想用的环境
- 当前 VS Code 解释器是不是同一个环境
- 该环境里是否真的安装了对应包
建议始终保持下面三者一致：
- VS Code 选择的 Python 解释器
- 终端激活的环境
- Jupyter 使用的内核
## 常见工作流
一个比较实用的 VS Code + Jupyter 工作流可以是这样：
### 项目初始化
- 创建项目目录
- 创建独立 Conda 环境
- 安装 `ipykernel` 和项目依赖
- 在 VS Code 中打开项目文件夹
### 探索阶段
- 用 `.ipynb` 或 `.py + # %%` 做快速实验
- 观察数据
- 画图
- 调整参数
- 验证思路
### 整理阶段
- 将稳定的逻辑提炼到正式 `.py` 模块中
- 把重复代码封装为函数
- 把路径、参数、配置从代码里抽离出来
### 沉淀阶段
- 把临时分析结果整理成文档
- 保留关键 Notebook 作为实验记录
- 将核心流程转为脚本或项目代码
## 绘图显示问题
在 Jupyter 环境中做可视化时，经常会用到 `matplotlib`。
常见写法例如：
``` python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3], [2, 4, 1])
plt.show()
```
如果图没有正常显示，可以检查：
- 是否安装了 `matplotlib`
- 当前内核是否正确
- 是否执行了绘图单元
- VS Code 的 Jupyter 扩展是否工作正常
如果你使用的是交互窗口，通常不需要额外配置，也能直接看到图形输出。
## Notebook 与普通脚本怎么选

### 更适合 Notebook 的情况
- 需要边写边看结果
- 需要展示中间过程
- 需要频繁画图
- 需要保留输出结果
- 偏探索性分析
### 更适合 `.py` 脚本的情况
- 代码已经相对稳定
- 需要模块化组织
- 需要自动化执行
- 需要良好的版本控制体验
- 偏工程化开发
### 折中方案
很多时候最好的方式不是二选一，而是组合使用：
- 前期用 Jupyter 快速探索
- 后期把稳定逻辑沉淀到 `.py`
- 必要时保留少量 Notebook 作为实验记录和结果展示


#VS-Code #Jupyter #Python #Conda
