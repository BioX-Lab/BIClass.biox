# Linux环境下IBM Aspera Connect安装与使用
IBM Aspera Connect支持多种平台环境，这里以Linux环境为例介绍其安装与使用。
## 使用Conda安装
推荐创建一个专属的conda环境用于aspera-cli的安装与运行。
``` bash
# 创建Conda环境
conda create -n Aspera -y
conda activate Aspera
# 安装aspera-cli
# 也可使用bioconda源安装
conda install -c hcc aspera-cli -y
```
## 官网安装包下载安装
安装过程中会出现“GLIBC_2.28' not found”等错误，需升级系统的glibc版本（不推荐），或者可以下载、安装低版本安装包。
### 下载安装包
访问[Aspera官方下载页面](https://www.ibm.com/support/fixcentral/swg/selectFixes?parent=ibm~Other%20software&product=ibm/Other+software/IBM+Aspera+Connect&release=All&platform=All&function=all)，找到适用于Linux系统的安装包。
### 解压安装包
使用`tar`命令解压下载的安装包，如`tar xvf ibm-aspera-connect_4.1.1.73_linux.tar.gz`。
### 运行安装脚本
进入解压后的目录，运行安装脚本`bash ibm-aspera-connect_4.1.1.73_linux.sh`完成安装。
### 添加环境变量
将Aspera的可执行文件路径添加到环境变量中，在`~/.bashrc`文件中添加`export PATH=~/.aspera/connect/bin/:$PATH`，然后执行`source ~/.bashrc`使环境变量生效。

## 配置方法
### 导入密钥文件
若安装完直接使用出现找不到密钥文件的错误，需下载OpenSSH并制作密钥文件。将生成的`asperaweb_id_dsa.openssh`文件移动到`~/.aspera/connect/etc/`目录下。
## 测试运行
使用`ascp -h`命令查看程序是否能正常运行。


#Aspera #Linux