# 在WSL中安装Docker

本文以WSL Ubunu为例安装最新版Docker。

## 卸载旧版本
如果以前没有安装过，可以忽略。
``` bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done

```
## 安装Docker Desktop（推荐）
- 下载Docker Desktop（https://docs.docker.com/get-started/get-docker/）并按照安装说明进行操作（默认选项即可）。
- 安装后，从 Windows 开始菜单启动 Docker Desktop，然后从任务栏的隐藏图标菜单中选择 Docker 图标。 右键单击该图标以显示 Docker 命令菜单，然后选择“设置”。 
- 确保在“设置”>“常规”中选中“使用基于 WSL 2 的引擎”。 
- 通过转到“设置”>“资源”>“WSL 集成”，从要启用 Docker 集成的已安装 WSL 2 发行版中进行选择。 
- 若要确认已安装 Docker，请打开 WSL 发行版（例如 Ubuntu），并通过输入 docker --version 来显示版本和内部版本号。
- 通过使用 docker run hello-world 运行简单的内置 Docker 映像，测试安装是否正常工作。

## 使用脚本安装
``` bash
#切换到相应目录
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

```
## 参考资料

- [Ubuntu | Docker Docs](https://docs.docker.com/engine/install/ubuntu/)

#WSL #Docker