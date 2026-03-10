# Linux下安装Miniforge3
Miniforge3 是轻量版 conda 包管理工具，适配 Linux 系统的安装流程如下，全程通过终端操作即可完成。
##  下载安装脚本
1. 打开终端，执行以下命令自动下载适配当前系统架构的安装脚本：
``` bash
	curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```
   - 若提示 `curl` 未找到：先安装 curl（`sudo apt install curl`/`sudo yum install curl`，依系统发行版而定）。
   - 下载失败可手动访问 [官方发布页](https://github.com/conda-forge/miniforge/releases)，选择 `Miniforge3-Linux-x86_64.sh`（64位主流）/`Miniforge3-Linux-aarch64.sh`（ARM架构）下载。

## 执行安装脚本
1. 赋予脚本可执行权限：
``` bash
chmod +x Miniforge3-$(uname)-$(uname -m).sh
```
2. 运行安装脚本：
``` bash
bash Miniforge3-$(uname)-$(uname -m).sh
```
3. 安装交互步骤（按提示操作）：
   - 按 Enter 阅读协议，输入 `yes` 同意；
   - 确认安装路径（默认 `~/miniforge3`，建议保持默认或改为纯英文无空格路径）；
   - 关键：提示「Do you wish to initialize Miniforge3 by running conda init?」时，输入 `yes`（自动配置终端，无需手动加环境变量）；
   - 等待安装完成即可。

## 验证安装
1. 关闭当前终端，重新打开新终端（使配置生效）；
2. 执行版本检查命令：
``` bash
conda --version
mamba --version
```
若输出类似 `conda 24.9.2`、`mamba 1.5.3` 的版本信息，说明安装成功。

## 常见问题解决
- 终端输入 `conda` 提示未找到命令：
  1. 确认安装时选择了 `yes` 初始化 conda；
  2. 重启终端重试；
  3. 手动初始化：执行 `~/miniforge3/bin/conda init`，再重启终端。
- 不想自动初始化：每次使用前执行 `source ~/miniforge3/bin/activate` 激活环境即可。

#Miniforge #Linux