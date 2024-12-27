# 如何更改WSL Ubuntu默认用户

[BI2024/YTT/20241119]

由于WSL Ubuntu安装过程中可能出现的各类问题，当WSL Ubuntu首次启动后默认登录为root用户时，可以采用如下方案设置其它默认用户。

## 方案一

``` powershell
#在Windows系统使用管理员权限打开Powershell，执行如下命令关闭WSL
wsl --shutdown
#使用如下命令来设置默认登录用户(e.g. yuting)
ubuntu.exe config --default-user yuting
#执行后，打开WSL Ubuntu会发现默认用户已更改
```

## 方案二

在WSL中编辑`/etc/wsl.conf`，加入`user=<你的用户名>`，重启即可。

## 在WSL中添加用户
如果WSL中还没添加其它用户时，需在WSL Ubuntu中添加相应用户。
``` bash
#新建用户
useradd yuting
#为该用户设置密码
passwd yuting
#为便于后续操作，建议将该用户添加到了sudo组
usermod -aG sudo yuting
```
## 在WSL中更改Shell类型

用户切换完成后，如果WSL 终端命令行提示符（$）前不显示用户名称的话，可以通过修改Shell类型解决。
``` bash
#在个人账号下，通过vi工具编辑/etc/passwd文件
sudo vi /etc/passwd
#找到个人用户所在行，将Shell类型更改为/bin/bash
```

#WSL #Linux 