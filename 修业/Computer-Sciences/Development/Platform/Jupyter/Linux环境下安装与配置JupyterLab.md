# Linux环境下安装与配置JupyterLab
JupyterLab 是 Jupyter 生态中的现代化交互式开发界面，适合在 Linux 环境中进行 Python、R、Notebook、终端和数据分析等工作。安装JupyterLab可以在后台运行一个服务，用户通过浏览器访问界面进行开发，也可以在VS Code中使用Jupyter插件连接到这个服务。
## 安装前建议
在 Linux 环境中使用 JupyterLab 时，推荐遵循以下原则：
- 不要长期直接在 Conda 的 `base` 环境中做开发。
- 建议为 JupyterLab 单独创建一个环境。
- 不同项目使用各自独立的 Conda 环境。
- 需要在 Jupyter 中使用某个环境时，为该环境安装并注册对应内核。
如果只是临时测试，也可以直接在当前 Python 环境中安装 JupyterLab，但长期使用仍建议采用独立环境方案。
## 安装 JupyterLab

### 使用 Conda/Mamba 安装
推荐先创建一个专门用于运行 JupyterLab 的环境。
``` bash
conda create -n jupyterlab python=3.12 -y
# conda remove -n jupyterlab --all -y
conda activate jupyterlab
```
安装 JupyterLab：
``` bash
conda install -c conda-forge jupyterlab
# 或
mamba install -c conda-forge jupyterlab
# 也可以安装jupyter: mamba install -c conda-forge jupyter
```
如果希望 JupyterLab 能更方便地识别多个 Conda 环境，可以安装：
``` bash
conda install -c conda-forge nb_conda_kernels
# 或
mamba install -c conda-forge nb_conda_kernels
```
在实际使用中，也可以“手动为目标环境注册内核”，这样更清晰、可控。
### 使用 pip 安装
如果使用的是普通 Python 环境，也可以直接安装：
``` bash
python -m pip install --upgrade pip
python -m pip install jupyterlab
```
安装完成后可用以下命令验证：
``` bash
jupyter lab --version
```
## 配置 Python 内核
JupyterLab 本身是前端与服务端界面，真正执行代码的是“内核”。如果希望在某个 Python 环境中运行 Notebook，需要在该环境中安装 `ipykernel`。
### 在目标环境中安装 ipykernel
例如某个项目环境名为 `myenv`：
``` bash
conda activate myenv
conda install ipykernel
# 或
mamba install ipykernel
# 或
python -m pip install ipykernel
```
### 注册该环境为 Jupyter 内核
``` bash
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```
说明：
- `--name` 是 Jupyter 内核内部名称
- `--display-name` 是在 JupyterLab 界面中看到的名称
### 查看已注册内核
``` bash
jupyter kernelspec list
```
## 配置 R内核
如果希望在 JupyterLab 中运行R，应安装与使用 `IRkernel`。
例如在 R 环境中执行：
``` r
install.packages("IRkernel")
IRkernel::installspec(user = TRUE, name = "ir", displayname = "R")
```
如果是 Conda R 环境，也可以在对应环境中安装 `r-irkernel`，部分情况下会自动被识别。
## 启动 JupyterLab

### 本机测试启动
先在终端中测试是否可正常启动：
``` bash
jupyter lab
```
默认会在本机启动，并输出访问链接。
### 指定监听地址和端口
如果需要从其他机器访问，可以指定 IP 和端口：
```bash
jupyter lab --ip=0.0.0.0 --port=8888 --no-browser
```
常见含义：
- `--ip=0.0.0.0`：监听所有网卡地址
- `--port=8888`：指定端口
- `--no-browser`：不自动打开浏览器
## 生成配置文件
可以先生成默认配置文件：
``` bash
jupyter lab --generate-config
```
通常会生成到：
``` bash
~/.jupyter/jupyter_lab_config.py
```
不过现在 JupyterLab 底层通常使用 Jupyter Server，很多配置也可能写入：
``` bash
~/.jupyter/jupyter_server_config.py
```
实际维护时，更建议优先关注 `jupyter_server_config.py` 和 `jupyter_server_config.json`。
## 设置密码

为了安全，建议为 JupyterLab 设置密码。执行：
``` bash
jupyter lab password
```
输入密码后，系统通常会把加密后的密码写入：
``` bash
~/.jupyter/jupyter_server_config.json
```
## 修改配置文件
如果需要允许远程访问，可以编辑配置文件，例如：
``` bash
~/.jupyter/jupyter_lab_config.py
```
加入或修改以下内容：
``` python
c.ServerApp.allow_remote_access = True
c.ServerApp.ip = "0.0.0.0"
c.ServerApp.port = 8888
c.ServerApp.open_browser = False
```
### 可选配置
如果已经通过 `jupyter lab password` 设置了密码，通常不需要再手动写：
``` python
c.ServerApp.password = "..."
```
如无特殊需要，也不建议手工维护密码哈希值。
## 访问方式说明
### 仅本机访问
如果只想在服务器本机使用，可以保持默认设置，或显式写为：
``` python
c.ServerApp.ip = "127.0.0.1"
```
这种方式最安全，适合通过 SSH 隧道访问。
###  局域网访问
如果局域网内其他设备需要访问，可设置：
``` python
c.ServerApp.ip = "0.0.0.0"
```
然后通过浏览器访问：
``` text
http://服务器IP:8888
```
### 公网访问
如果服务器直接暴露在公网，务必注意：
- 设置强密码
- 建议启用 HTTPS
- 建议使用反向代理
- 最好限制来源 IP
- 尽量不要裸露开放默认端口给整个公网
公网场景下，推荐配合 Nginx、Caddy 或 Traefik 做反向代理，而不是直接把 JupyterLab 端口完全暴露出去。
## 将 JupyterLab 配置为 systemd 服务
为了让 JupyterLab 在后台稳定运行，并支持开机自启，可以使用 systemd。
### 确认可执行文件路径
先激活 JupyterLab 所在环境，查看实际路径：
```bash
which jupyter
which python
```
例如可能得到：

``` bash
/home/yourname/miniforge3/envs/jupyterlab/bin/jupyter
/home/yourname/miniforge3/envs/jupyterlab/bin/python
```
### 创建服务文件
创建：
``` bash
sudo vi /etc/systemd/system/jupyterlab.service
```
写入以下内容：
```ini
[Unit]
Description=JupyterLab Service
After=network.target

[Service]
Type=simple
User=yourname
Group=yourgroup
WorkingDirectory=/home/yourname
ExecStart=/home/yourname/miniforge3/envs/jupyterlab/bin/jupyter lab --config=/home/yourname/.jupyter/jupyter_lab_config.py
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```
### 重新加载并启动服务
``` bash
sudo systemctl daemon-reload
sudo systemctl enable jupyterlab
sudo systemctl start jupyterlab
```
如果修改了服务文件，可执行：
``` bash
sudo systemctl restart jupyterlab
```
### 查看服务状态
``` bash
sudo systemctl status jupyterlab
```
查看日志：
``` bash
sudo journalctl -u jupyterlab.service
```
实时查看日志：
``` bash
sudo journalctl -u jupyterlab.service -f
```
## 防火墙设置

如果服务器启用了防火墙，需要放行 JupyterLab 使用的端口，例如 8888：
```bash
sudo ufw allow 8888/tcp
```
查看防火墙状态：
``` bash
sudo ufw status
```
如果使用的是云服务器，还要检查云平台安全组是否放行对应端口。
## 配置 HTTPS
如果需要通过公网或不可信网络访问，建议启用 HTTPS。在配置文件中可指定证书和私钥：
``` python
c.ServerApp.certfile = "/path/to/your/certificate.crt"
c.ServerApp.keyfile = "/path/to/your/private.key"
```
更常见、更推荐的做法是：
- 用 Nginx 或 Caddy 做 HTTPS 反向代理
- 让反向代理处理证书续期与 TLS 配置
- JupyterLab 仅在本机或内网端口监听

#Linux #JupyterLab