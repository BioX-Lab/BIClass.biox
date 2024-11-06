# RStudio Server如何切换不同R环境

实际项目开发过程中，有时需要切换不同的R环境（包括不同版本的R引擎及R包等）；不同的R环境可通过Conda等方式创建与维护；本文以CentOS 7.9和Conda创建的R环境为例。

RStudio Server安装完成后，可以看到其配置文件：“/etc/rstudio/rserver.conf”；接下来需要修改rserver.conf配置文件中的rsession-which-r与rsession-ld-library-path变量（本修改需要个人账号具有sudo权限）。

假设要切换为Conda环境env1中的R，依次将上述两个变量进行修改：
```
# 将"/.../envs/env1"替换为个人相应的conda环境的路径
rsession-which-r=/.../envs/env1/bin/R
rsession-ld-library-path=/.../envs/env1/lib:/.../envs/env1/x86_64-conda-linux-gnu/lib

```
rserver.conf修改完成后，即可重启RStudio Server、使配置生效（`rstudio-server restart`）；可以将上述修改过程写成脚本、便于后续切换。


#R #RStudio-Server



