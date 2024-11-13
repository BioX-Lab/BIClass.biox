# 如何解决storage.googleapis.com无法访问

> 以Linux为例，介绍本解决方案；本方案在/etc/hosts文件中添加主机名和 IP 地址的映射，当访问主机时系统会直接访问相应IP地址。

## 获取IP地址

https://tool.chinaz.com/speedtest/storage.googleapis.com  

## 修改host

使用`vi`等工具编辑`/etc/hosts`文件，在hosts文件最后添加`IP地址 storage.googleapis.com`。



#Google #Download #hosts