# VS Code中配置Python开发环境
安装完成VS Code后可进一步配置 Python开发环境，这里以Conda创建的虚拟环境为例，也可以使用UV或者venv等创虚拟环境。
## 安装必要扩展

### Python
这是核心扩展，提供：
- Python 语法支持
- 运行和调试支持
- 解释器选择
- 测试支持

### Python Debugger

调试器扩展提供更强大的调试功能，支持断点、变量监视、调用堆栈等功能，极大提升调试效率。

### Pylance
提供：
- 更强的自动补全
- 类型提示
- 定义跳转
- 更好的编辑体验

### Jupyter（可选）
如果使用 Notebook，可以安装。 
如果只是普通 `.py` 文件开发，可以先不装。

### 其他常用扩展（可选）
- Black Formatter
- Ruff
- GitLens
- Error Lens
建议不要一开始装太多功能重叠的扩展，以免冲突。
## 选择正确的Conda解释器
### 选择方法
按：
``` text
Ctrl + Shift + P
```
搜索：
``` text
Python: Select Interpreter
```
然后在列表中选择对应的 Conda 环境。 
通常会看到类似：

``` text
Python 3.11.x ('my_python_project': conda)
```
选中它即可。
选择后，VS Code 底部状态栏通常会显示当前环境信息。
### 验证解释器是否正确

创建一个 `main.py`：

``` python
import sys

print("Hello from Conda in VS Code")
print(sys.executable)
```
运行后重点检查：
- 是否能正常输出
- `sys.executable` 是否指向 Conda 环境中的 Python
如果路径属于目标 Conda 环境，说明配置基本成功。
## 在 VS Code 中运行 Python
### 使用内置终端运行
``` bash
python main.py
```
前提是当前终端已经激活正确的 Conda 环境。
### 使用右上角运行按钮
适合快速执行当前文件，需确认 VS Code 的解释器已经切换到目标 Conda 环境。
### 使用调试模式
点击左侧调试图标，设置断点后点击绿色运行按钮，可以进入调试模式，逐行检查代码执行情况。

#VS-Code #Python