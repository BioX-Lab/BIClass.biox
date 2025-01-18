# 如何在Jupyter中运行Pythont程序文件
Jupyter中运行Python程序文件可以采用如下某种方法。

## 使用`%run`魔法命令

在 Jupyter Notebook 的一个代码单元格中，你可以使用 `%run` 魔法命令直接运行一个 Python 程序文件。

假设你有一个名为 `my_program.py` 的 Python 文件。
``` python
## my_program.py
def add(a, b):
    return a + b
if __name__ == "__main__":
    result = add(3, 5)
    print(result)
```
可以在 Jupyter 的一个代码单元格中输入以下命令：
``` python
%run my_program.py
```

## 使用`!`符号执行系统命令

可以使用 `!` 符号在Jupyter中执行系统命令（类似于在命令行终端中运行命令），包括运行 Python 程序。

在 Jupyter 的一个代码单元格中输入以下命令：
```python
!python my_program.py
```

## 将Python文件内容复制到 Jupyter 代码单元格中

如果不想使用外部文件，可以将 `my_program.py` 中的代码复制到 Jupyter 的代码单元格中运行。
代码的执行方式和普通的 Python 解释器一样，按 `Shift + Enter` 键运行代码单元格。


## 使用建议
- 对于较长的程序文件，使用 `%run` 或 `!` 方法会更方便，避免在 Jupyter 中输入大量代码。
- 当使用 `%run` 或 `!` 时，确保文件的路径正确，避免 `FileNotFoundError`。
- 如果你使用的 Python 程序依赖于相对路径来读取或写入文件，可能需要注意 Jupyter 的工作目录，可以使用 `os` 模块来调整工作目录。
``` python
import os
os.chdir('/path/to/your/program')
```
## 在 Jupyter Lab 中的使用
上述方法在 Jupyter Lab 中同样适用，因为Jupyter Lab是 Jupyter Notebook的增强版，操作基本一致。


#Jupyter #Python