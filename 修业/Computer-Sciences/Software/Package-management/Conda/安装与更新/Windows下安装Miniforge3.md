# Windows下安装Miniforge3

Miniforge3是轻量化的conda包管理工具，以下是 Windows 系统的快速安装与验证步骤。
##  下载安装包
1. 访问官方发布页：https://github.com/conda-forge/miniforge/releases
2. 根据系统位数选择对应安装包：
   - 64 位（主流）：`Miniforge3-Windows-x86_64.exe`
   - ARM64（如 Surface Pro X）：`Miniforge3-Windows-aarch64.exe`
   - 32 位（极少）：`Miniforge3-Windows-x86.exe`
3. 下载后保存到本地（如 Downloads 文件夹）。

## 安装步骤
1. 双击下载的 `.exe` 文件启动安装向导，依次点击「Next」→ 同意协议 →「Next」。
2. 选择安装用户：推荐「Just Me」（无需管理员权限，更安全）；需所有用户使用则选「All Users」（需管理员权限）。
3. 选择安装路径：建议用**纯英文、无空格路径**（如 `D:\miniforge3`），默认路径为 `C:\Users\<你的用户名>\miniforge3`。
4. 高级选项（关键）：
   - 必勾选：`Add Miniforge3 to my PATH environment variable`（添加到系统 PATH，方便终端直接调用 conda）；
   - 可选：`Register Miniforge3 as my default Python`（设为系统默认 Python，按需勾选）。
1. 点击「Install」等待安装完成，最后点击「Finish」。
## 验证安装
1. 新开 CMD 或 PowerShell 窗口（旧窗口可能不生效）。
2. 输入以下命令检查版本：
``` bash
conda --version
mamba --version
```
若输出类似 `conda 24.9.2`、`mamba 1.5.3` 的版本信息，说明安装成功。

## 常见问题解决
- 提示「conda 不是内部或外部命令」：
  1. 确认安装时勾选了「Add to PATH」；
  2. 关闭所有旧终端，重新打开新窗口重试；
  3. 仍失败则手动添加环境变量（安装目录下的 `Scripts` 和 `Library\bin` 路径）。
- 不想添加到 PATH：从开始菜单打开「Miniforge Prompt」即可使用 conda/mamba。

#Miniforge #Windows