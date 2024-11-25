# 使用命令行安装与更新WSL

如下命令默认使用PowerShell或者Command Prompt，以管理员权限启动。

## 查看微软应用商店中可用的WSL发行版列表
`wsl -l -o`

## 命令行安装

安装Ubuntu系统镜像
`wsl --install -d Ubuntu`
安装指定版本Ubuntu
`wsl --install -d Ubuntu-24.04`

## 升级WSL内核
`wsl --update`
### 重启WSL内核
内核升级完成以后，电脑重启才会生效，这个可以用命令重启
`wsl -l -shutdown`
## 查看本地系统WSL情况
`wsl -l -v`

## 升级Linux系统的包
建议使用发行版的首选包管理器定期更新和升级包。 对于 Ubuntu 或 Debian，请使用以下命令。
`sudo apt update && sudo apt upgrade`


#WSL #Windows 