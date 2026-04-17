# VS Code 中配置 R 开发环境

安装完成VS Code后可进一步配置R开发环境，这里以Conda创建的虚拟环境为例，也可以使用Renv等创建虚拟环境。
注：**不推荐**采用本方案在实际项目中进行开发，理解原理即可，建议使用`Jupyter+VS Code+Conda`等方案。

## 安装 VS Code 必要扩展
### R扩展
在 VS Code 扩展市场中搜索R，常见的是由 `REditorSupport` 提供的扩展。这是最核心的扩展，主要提供：
- R 语法高亮
- 运行选中代码或当前脚本
- 与 R 终端集成
- 部分对象查看与交互支持
### R Debugger（可选）
如果需要在VS Code中进行 R 调试，可以按需安装相关调试扩展。不过相较于 Python，R 在 VS Code 中的调试体验通常没有那么统一和成熟。所以多数情况下，先把重点放在：
- 正常运行脚本
- 正常发送代码到 R 终端
- 正常补全和查看提示
### 其他可选扩展
按需安装：
- Quarto
- Markdown All in One
- GitLens
- Error Lens
## 创建 Conda 环境
创建一个专门用于项目开发的 Conda 环境。
``` bash
# 创建 my_project_R 环境
conda create --name my_project_R -y
# 如需删除环境
# conda remove -n my_project_R --all
# 激活环境
conda activate my_project_R
```
### 安装 R 及常用组件
进入Conda环境后，安装 R 本体和常用增强组件。
### 安装 `r-base`
``` bash
mamba install -c conda-forge r-base
```
这是 R 的基础运行环境，没有它，就不能在该 Conda 环境里真正运行 R。
### 安装 `r-essentials`（可选）
``` bash
conda install -c conda-forge r-essentials -y
```
说明：
- `r-essentials` 会安装一批常见 R 开发与数据分析相关组件。
- 适合想快速搭好环境的人。
- 但它会装得比较多，不属于“最小化环境”。
### 安装 Jupyter（可选）
``` bash
mamba install jupyter
```
说明：
- 如果需要在该环境中使用 Notebook，这一步很有帮助。
- 即使当前主要在 VS Code 中写 `.R` 脚本，装上 Jupyter 也通常没有坏处。
###  安装 IRkernel（可选）
``` bash
mamba install r-irkernel
```
作用：
- 为 Jupyter 提供 R 内核支持
- 如果之后需要在 Notebook 中运行 R，这一步很关键。
### 安装 Radian
``` bash
mamba install radian
```
作用：
- `Radian` 是一个增强版 R 控制台。
- 相比原生 R 终端，交互体验通常更好。
- 在 VS Code 中配合 R 扩展使用时，体验通常明显优于默认 R 终端。
### 安装 `languageserver`

``` bash
mamba install r-languageserver
```
作用：
- 提供代码补全
- 变量和函数提示
- 跳转定义
- 更好的编辑器智能支持

这是 VS Code 中 R 开发体验提升最明显的组件之一。
### 安装 `httpgd`
``` bash
mamba install r-httpgd
```
作用：
- 改善 VS Code 中的绘图显示体验
- 更适合交互式绘图场景
### 可能需要的系统依赖
根据环境提示，有时还需要补系统库，例如：
``` bash
# 根据提示安装依赖
# sudo yum install libX11-devel cairo-devel
```
这类依赖通常出现在：
- Linux
- 远程服务器
- 图形相关组件安装时
如果安装 `httpgd` 或其他绘图相关包时报错，可以优先检查这些系统级依赖是否缺失。
## 配置 Radian
安装完 `radian` 后，需要在 VS Code 中把 R 终端切换到 `Radian`。
### 配置步骤
1. 打开设置 
   快捷键：
   - macOS：`cmd + ,`
   - Windows / Linux：`Ctrl + ,`
2. 搜索：
``` text
r.rterm.windows
```
或：
``` text
r.rterm.linux
```
如果是 macOS，也可以搜索对应的 R 终端路径设置项。
3. 将其配置为 `radian` 运行脚本。

  可以先在终端中查找 `radian` 路径：
``` bash
where radian
```
Linux / macOS 可以用：
``` bash
which radian
```

例如，在Windows上 `where radian` 返回类似：
```text
C:\Users\YourName\miniforge3\envs\my_project_R\Scripts\radian.exe
```
如果在 Linux 上返回类似：
``` text
/home/yourname/miniforge3/envs/my_project_R/bin/radian
```

以Windows为例，在`C:\Users\YourName\miniforge3\envs\my_project_R\Scripts\`目录中创建一脚本`start_radian_conda.bat`，将"r.rterm.windows"设置为`C:\Users\YourName\miniforge3\envs\my_project_R\Scripts\start_radian_conda.bat`。

``` start_radian_conda.bat
@echo off
call `C:\Users\YourName\miniforge3\condabin\conda.bat activate my_project_R
C:\Users\YourName\miniforge3\envs\my_project_R\Scripts\radian.exe
```


### 启用 Bracketed Paste
继续在设置中搜索：
``` text
r.br
```
启用 **Bracketed Paste**。
作用：
- 改善多行代码粘贴体验
- 减少粘贴代码时的格式错乱问题
- 配合 `Radian` 使用时更顺手
## 配置 httpgd
为了在 VS Code 中获得更好的绘图体验，可以启用 `httpgd`。
### 配置步骤
1. 打开设置
2. 搜索：
``` text
r.plot.useHttpgd
```
3. 启用它
启用后，R 扩展会优先使用 `httpgd` 进行图形显示。
适合场景：
- 交互式绘图
- 数据探索
- 在编辑器中查看绘图结果
## 其它推荐配置
### 调整 `r.rterm.option`

在设置中搜索：
```text
r.rterm.option
```
删除其中的：
```text
--no-save,--no-restore,--no-site-file
```
说明：
- 某些默认参数会影响 R 会话的交互行为
- 删除后通常更适合当前这种增强型终端工作流
- 如果后续遇到兼容问题，也可以再按需调整回来
### 启用 `r.sessionWatcher`
在设置中搜索：
``` text
r.sessionWatcher
```
将其勾选启用。
作用：
- 可以获得更接近 IDE 的交互体验
- 可以查看 dataframe
- 可以辅助绘图管理
- 对交互式分析更友好
如果想使用更原生、更简单的绘图方式，也可以取消勾选。可以这样理解：
- 勾选：偏 IDE 化体验
- 取消勾选：偏原生 R 终端体验

## 运行 R 文件的实例

完成 R 环境配置后，就可以在 VS Code 中实际运行 `.R` 文件了。
### 新建一个 R 脚本

例如创建文件`hello.R`，写入以下内容：
``` r
x <- 1:10
y <- x^2

print("Hello R in VS Code")
print(x)
print(mean(y))

plot(x, y, type = "b", col = "blue", pch = 19)
```

这个脚本做了几件事：
- 创建向量 `x`
- 计算 `y = x^2`
- 在终端输出文字和结果
- 画出一张简单的折线散点图
### 运行选中代码
这是最常用的方式，适合交互式调试。选中一行或多行代码，按`Windows`/`Linux`的快捷键 `Ctrl + Enter`，或 `macOS` 的 `Cmd + Enter`，即可将选中的代码发送到 R 终端执行。

### 运行整个 R 文件
如果希望一次性执行整个脚本，可以直接运行整个 `.R` 文件。常见方式：
- 在编辑器右上角点击运行整个文件
- 在命令面板中执行与运行当前 R 文件相关的命令
- 在 R 终端中使用 `source()`
例如在 R 终端中运行：
``` r
source("hello.R")
```

如果当前工作目录就是该文件所在目录，这样即可执行整个脚本。
### 在终端中直接运行
也可以不通过“逐段发送代码”，而是在终端中直接执行脚本。
#### 使用 Rscript
``` bash
Rscript hello.R
```
作用：
- 适合批处理执行
- 适合跑完整脚本
- 不依赖交互式 R 控制台

如果你使用的是 Conda 环境，记得先激活环境再运行：

```bash
conda activate my_project_R
Rscript hello.R
```

### 如何判断是否运行成功

运行成功后，一般会看到以下结果：

- 终端输出 `"Hello R in VS Code"`
- 输出 `x` 的内容
- 输出 `mean(y)` 的结果
- 如果启用了 `httpgd`，图形会在 VS Code 的绘图面板中显示。
- 如果没有启用 `httpgd`，则可能在默认图形设备中显示。


#VS-Code #R