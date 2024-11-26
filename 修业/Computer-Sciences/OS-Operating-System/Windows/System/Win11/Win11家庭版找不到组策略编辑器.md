# Win11家庭版找不到组策略编辑器

组策略编辑器是Windows中一个强大的工具，用于管理计算机上的用户和计算机配置，在某些家庭版或教育版中可能缺失；可尝试通过如下方式安装。

## 创建、运行bat脚本

- 创建一个batch脚本`Group-Policy-Editor.bat`，包括如下命令。
``` cmd
@echo off
pushd "%~dp0"
dir /b C:\Windows\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~3*.mum >List.txt
dir /b C:\Windows\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~3*.mum >>List.txt
for /f %%i in ('findstr /i . List.txt 2^>nul') do dism /online /norestart /add-package:"C:\Windows\servicing\Packages\%%i"
pause

```
- 选择以管理员身份运行该脚本，如果UAC提示打开，请选择是；等批处理文件的命令执行完成后、关闭该窗口。
## 测试
- 按下`Windows + R`键打开“运行”对话框。
- 输入`gpedit.msc`并按下回车键，如果能打开“本地组策略编辑器”即为安装成功。



#Windows #Win11 #组策略