# WSL中安装Anaconda
本文演示如何在WSL Ubuntu中安装Anaconda，也可以安装Miniconda等。

## 更新系统软件包
``` bash
# 确保系统处于最新状态，避免一些因旧版本软件包导致的安装问题
sudo apt update
sudo apt -y upgrade
```
## Anaconda 安装
``` bash
# 下载安装包
wget https://repo.anaconda.com/archive/Anaconda3-2024.10-1-Linux-x86_64.sh
# 根据提示安装Anaconda，使用默认值即可（最后一步提示是否初始化Conda环境变量时，建议选择`yes`，也可以后续通过`conda init`自行初始化; 初始化Conda环境变量后，每次打开终端会默认打开`base`环境）
./Anaconda3-2024.10-1-Linux-x86_64.sh

```
## 验证安装

``` bash
conda --version
```
## 配置 Conda（可选）
可以配置 Conda 的源（修改`.condarc`文件），以加快软件包的下载速度；如果网络没有问题，可以使用默认配置。



#WSL #Conda 