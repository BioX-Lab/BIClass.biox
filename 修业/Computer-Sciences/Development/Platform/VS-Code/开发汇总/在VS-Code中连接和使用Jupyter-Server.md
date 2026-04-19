# 在VS Code中连接和使用Jupyter Server
Jupyter Server 可以理解为提供 Notebook 内核、文件访问和代码执行能力的后端服务。VS Code 安装了 Jupyter 扩展后，可以连接这个后端，从而在本地或远程环境中运行 `.ipynb` Notebook，或者执行 `# %%` 形式的交互式代码单元。这种方式适合：
- 服务器上有数据和算力，本地只负责编辑
- 希望统一管理 Notebook 运行环境
- 在远程 Linux 主机、实验室服务器、云主机上运行代码
- 避免本地重复安装大量科学计算依赖
## 前提准备
在 VS Code 中使用 Jupyter Server，通常需要准备以下内容。
### VS Code 扩展
建议至少安装：
- Python
- Jupyter
如果要做 R 开发，还建议安装：
- R
- 相关语言支持扩展（可选）
### Jupyter Server 所在环境
Jupyter Server 所在的环境通常需要安装：
``` bash
pip install jupyterlab notebook
# 或者 pip install jupyter
```
或者用 Conda：
``` bash
conda install -c conda-forge jupyterlab notebook
# 或者 conda install -c conda-forge jupyter
# 或者 mamba install -c conda-forge jupyter
```
## Python 内核准备
如果 Jupyter Server 要运行 Python 代码，目标 Python 环境通常需要能被识别为一个 Jupyter Kernel。
### 安装 ipykernel
``` bash
conda activate myenv
conda install ipykernel
# 或者 mamba install ipykernel
```
或者：
``` bash
pip install ipykernel
```
### 注册内核
有时需要手动注册：
``` bash
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```
参数含义：
- `--name`：内核内部名称
- `--display-name`：在 VS Code / Jupyter 中显示的名称
### 查看已有内核
``` bash
jupyter kernelspec list
```
如果能看到类似：
``` text
myenv    ...
python3  ...
```
说明 Jupyter 已能识别该 Python 内核。
## R 内核准备
如果想通过 Jupyter Server 在 VS Code 中运行 R 代码，需要准备 R 内核，而不是 Python 的 `ipykernel`。
### 安装 IRkernel
在 R 中执行：
```r
install.packages("IRkernel")
# 或者在bash终端运行： conda install r-irkernel
```
### 注册 R 内核
在 R 中执行：
``` r
IRkernel::installspec()
```
如果想指定显示名称：
``` r
IRkernel::installspec(name = "ir", displayname = "R")
```
### 查看是否注册成功
``` bash
jupyter kernelspec list
```
应能看到类似：
``` text
ir    ...
```
如果使用 Conda 安装了 `r-irkernel`，有时 Jupyter 会自动识别，不一定需要再手动执行 `IRkernel::installspec()`；但如果 VS Code 中看不到 R 内核，手动注册通常最稳妥。
## 在VS Code中连接 Jupyter Server
打开一个 `.ipynb` 文件，或者在一个 Python 脚本中使用 `# %%` 形式的交互式代码单元时，在VS Code右上角点击`Select Kernel`,点击`Select Another Kernel`，选择 `Existing Jupyter Server`，然后输入 Jupyter Server 的 URL 地址即可连接。
### 连接本机启动的 Jupyter Server
比如在本机 Conda 环境中启动：
``` bash
jupyter lab
```
或者：
``` bash
jupyter notebook
```
然后 VS Code 连接本地地址，例如：
```text
http://localhost:8888/lab?token=xxxxxxxx
```
这种方式适合：
- 本地已经配置好 Python / R / Jupyter 环境
- 想用 VS Code 代替浏览器来操作 Notebook
- 希望同时保留 `.ipynb` 和脚本式开发体验
### 连接远程 Jupyter Server
比如服务器上已启动 Jupyter Server，在 VS Code 中填写远程 URL：
``` text
http://your-server:8888/lab?token=xxxxxxxx
```
或配置过反向代理后的地址：
``` text
https://your-domain/jupyter/?token=xxxxxxxx
```
这种方式适合：
- 数据在远程服务器，不方便下载到本地
- 远程环境已安装好 CUDA、深度学习框架、R 包等
- 希望直接使用服务器资源运行 Notebook
### 连接成功后的表现
连接成功后：
- VS Code 可以列出该 Server 提供的 kernel
- 打开 `.ipynb` 时可以选择远程 kernel
- 运行 Notebook 时，代码实际在 Jupyter Server 所在机器执行
## 如何获取 Jupyter Server URL
### 启动时终端输出
运行：
``` bash
jupyter lab
```
通常终端会输出类似：
``` text
http://localhost:8888/lab?token=xxxxxxxxxxxxxxxx
```
复制这个地址即可。
### 查看运行中的服务
如果终端已关闭或滚动找不到，可尝试：
``` bash
jupyter server list
```
或：
```bash
jupyter notebook list
```
可能输出：
``` text
Currently running servers:
http://localhost:8888/?token=xxxxxxxx :: /path/to/workdir
```

#VS-Code #Jupyter-Server