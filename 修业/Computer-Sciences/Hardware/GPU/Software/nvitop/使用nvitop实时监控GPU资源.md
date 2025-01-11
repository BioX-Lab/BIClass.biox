# 使用nvitop实时监控GPU资源
nvitop能够提供有关GPU利用率、温度、内存使用情况等重要信息。

## 安装nvitop

在本地Conda环境，如`base`或者`BIClass_py310`中通过`pip install nvitop`会从 Python Package Index 官方源下载并安装nvitop及其依赖，安装后可在当前Python环境使用。
## 查看监控
安装完在终端输入`nvitop`，会展示GPU相关指标，如利用率、内存使用、温度、进程信息等，执行`nvitop -m full`可查看更多进阶指标；也可编写资源调度脚本，智能监控GPU资源。


#GPU #nvitop