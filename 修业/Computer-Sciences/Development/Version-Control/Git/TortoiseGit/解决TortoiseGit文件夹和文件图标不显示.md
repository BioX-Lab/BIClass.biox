# 解决TortoiseGit文件夹和文件图标不显示

TortoiseGit图标在电脑上不显示，影响版本控制的可视化操作，可参考如下解决方案。

## 调整TortoiseGit在注册表中的优先级
- 打开TortoiseGit的Settings，进入`Icon Overlays` -> `Overlay Handlers` -> `Start registry editor`。
- 找到`ShellIconOverlayIdentifiers`文件夹。
- 将TortoiseGit相关的几个文件夹前面重命名，添加几个空格，确保它们排在最前面。

## 设置MaxCachedIcons选项
- 在注册表路径`HKEY_LOCAL_MACHINE\Software\Microsoft\windows\CurrentVersion\Explorer`下，检查是否存在`Max Cached Icons`选项。
- 如果不存在，新建一个`Max Cached Icons`选项，数值数据设置为2000。

## 重启电脑
为保证效果准确性，重启电脑后，图标应恢复正常显示。

## 补充设置
- 打开TortoiseGit的Settings，在Icon Overlays中将Status cache设置为Shell，Drive Types设置为Fixed drivers，并勾选Show excluded folders as normal。
- 如果问题仍未解决，可以尝试重新安装TortoiseGit，确保系统和软件版本匹配（如64位系统安装64位TortoiseGit）。
## 注意事项
- 修改注册表时需谨慎操作，错误的修改可能导致系统不稳定。
- 在进行注册表修改前，可选择备份注册表。

#TortoiseGit #Git