# 如何在Windows系统安装WSL

现将Windows系统中安装WSL（Windows Subsystem for Linux）的过程简要汇总如下。

## 系统要求检查
1. 确保你的Windows系统是Windows 10（版本1903或更高版本）或者Windows 11。因为旧版本的Windows不支持WSL或者支持的功能有限。
2. 你的电脑需要启用“适用于Linux的Windows子系统”可选功能。

## 启用“适用于Linux的Windows子系统”功能

1. 打开“控制面板”，选择“程序”，然后点击“程序和功能”。
2. 在左侧菜单中，选择“启用或关闭Windows功能”。
3. 在弹出的“Windows功能”对话框中，找到“适用于Linux的Windows子系统”选项，勾选它，然后点击“确定”。系统会提示你需要重新启动计算机，按照提示重启电脑使设置生效。

## 安装Linux分发版（以Ubuntu为例）

1. 打开Microsoft Store应用商店。
2. 在搜索栏中输入你想要安装的Linux发行版名称，如“Ubuntu”。
3. 从搜索结果中选择对应的Linux发行版应用程序（如Ubuntu），然后点击“获取”按钮进行下载和安装。安装完成后，你可以在开始菜单中找到对应的Linux发行版图标。

## 初始化安装的Linux分发版

1. 第一次运行安装好的Linux发行版（如Ubuntu）时，它会进行初始化配置。这个过程可能需要下载一些额外的文件和组件，同时会要求你设置用户名和密码，用于后续登录Linux系统。

安装完成后，你就可以在Windows系统中使用WSL运行Linux命令和应用程序了。在使用过程中，还可以根据自己的需求对WSL进行进一步的配置，例如设置文件共享、安装其他软件包等。

#Linux #WSL #Ubuntu