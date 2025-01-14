# 不同方式清空Windows中的回收站

## 从Windows桌面清空
Windows在桌面上一般包含回收站，右键单击桌面上的回收站，然后选择“清空回收站”选项即可。

## 从文件资源管理器清空
将回收站添加到文件资源管理器导航窗格中，点击回收站，在功能区找到“清空回收站”选项并点击。

## 使用磁盘清理清空
1. 右键单击“此电脑”中的C驱动器或系统驱动器，选择“属性”。
2. 在“常规”选项卡中，点击“磁盘清理”按钮。
3. 在下一个窗口中，删除除回收站之外的每个复选框的勾选。
4. 点击“确定”按钮并点击“删除文件”按钮确认删除。

## 使用Store Sense自动清空回收站
存储感知（在设置中打开：`System->Storage->Storage Sense`）可通过删除临时文件、清空回收站等方式为计算机创造空间，可按照相关指南自动删除回收站中的文件。

## 使用PowerShell清空

在Windows PowerShell中可以通过执行相关命令来清空回收站。

``` powershell
# 计算机上打开 Windows PowerShell，根据实际情况、执行如下某条命令 
# 运行后会提示用户确认清除本地计算机上的所有回收站
Clear-RecycleBin
# 指定C卷上的回收站
Clear-RecycleBin -DriveLetter C
# 使用Force参数后不会提示用户确认清除本地计算机上的所有回收站
Clear-RecycleBin -Force
# 当遇到错误时、会忽略相关错误
Clear-RecycleBin -Force -ErrorAction:Ignore
```
## 使用命令提示符清空
可以在命令提示符运行PowerShell相关命令。

``` cmd
# 计算机上打开命令提示符，根据实际情况、执行如下某条命令 
# 运行后会提示用户确认清除本地计算机上的所有回收站
PowerShell Clear-RecycleBin
# 指定C卷上的回收站
PowerShell Clear-RecycleBin -DriveLetter C
# 使用Force参数后不会提示用户确认清除本地计算机上的所有回收站
PowerShell Clear-RecycleBin -Force
# 当遇到错误时、会忽略相关错误
PowerShell Clear-RecycleBin -Force -ErrorAction:Ignore
```


#Windows #Recyle-Bin
