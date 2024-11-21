# Win11安装Ubuntu WSL时报错：WslRegisterDistribution failed with error: 0x800701bc

”WslRegisterDistribution failed with error: 0x800701bc" 是在尝试安装 WSL时出现的错误，需要开启“虚拟机平台”功能。

1. 打开“控制面板”，选择“程序”，然后点击“程序和功能”。
2. 在左侧菜单中，选择“启用或关闭Windows功能”。
3. 在弹出的“Windows功能”对话框中，找到“虚拟机平台”选项，勾选它，然后点击“确定”。系统会提示你需要重新启动计算机，按照提示重启电脑使设置生效。
重启后重新打开Ubuntu，即可进行（初始使用）配置、使用。

#WSL #Windows #Win11
