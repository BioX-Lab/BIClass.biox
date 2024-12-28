# 在Windows中比较两个目录的差异

## 使用命令行工具 fc
`fc`主要用于比较文件，但结合一些脚本可用于目录比较。它能逐行比较文本文件，但对二进制文件及复杂目录结构支持有限。

### 示例脚本

``` batch
@echo off
setlocal enabledelayedexpansion

:: Ensure the first directory path is provided
if "%~1"=="" (
    echo Please provide the first directory path as the first argument.
    exit /b 1
)

:: Ensure the second directory path is provided
if "%~2"=="" (
    echo Please provide the second directory path as the second argument.
    exit /b 1
)

set "dir1=%~1"
set "dir2=%~2"

:: Check if the first directory exists
if not exist "%dir1%" (
    echo The directory "%dir1%" does not exist.
    exit /b 1
)

:: Check if the second directory exists
if not exist "%dir2%" (
    echo The directory "%dir2%" does not exist.
    exit /b 1
)

echo Comparing files and directories in "%dir1%" and "%dir2%"...

:: Call compareDirs function to compare the directories
call :compareDirs "%dir1%" "%dir2%" "dir1"
call :compareDirs "%dir2%" "%dir1%" "dir2"

exit /b 0

:: Function to compare directories and files
:compareDirs
set "sourceDir=%~1"
set "targetDir=%~2"
set "sourceLabel=%~3"

echo Comparing %sourceLabel%...

:: Loop through files and directories in the source directory
for /r "%sourceDir%" %%f in (*) do (
    set "sourcePath=%%~f"
    set "targetPath=!sourcePath:%sourceDir%=%targetDir%!"

    :: Check if the target is a file or directory
    call :isFileOrDirectory "!sourcePath!"
    set "Dir_or_File=!result!"

    :: Check if the target file/directory exists
    if exist "!targetPath!" (
	
        if "!Dir_or_File!"=="FILE" (
            :: Compare files
            fc /b "%%f" "!targetPath!" >nul
            if errorlevel 1 (
                echo Files differ: %%f and !targetPath!
            ) else (
                echo Files are the same: %%f and !targetPath!
            )
        ) else (
			echo %%f
            echo Directory found in both locations: %%f
        )
    ) else (
        :: Handle missing files or directories
        if "!Dir_or_File!"=="FILE" (
            echo File missing in %targetDir%: %%f
        ) else (
            echo Directory missing in %targetDir%: %%f
        )
    )
)

exit /b 0

:: Function to check if the path is a file or directory
:isFileOrDirectory
set "inputPath=%~1"

:: Check if the path exists
if not exist "%inputPath%" (
    ::echo The path "%inputPath%" does not exist.
    set "result=NONE"
    goto :eof
)

:: Check if it's a directory
if exist "%inputPath%\" (
    set "result=DIR"
) else (
    set "result=FILE"
)

goto :eof


endlocal
```

## 使用第三方工具
>推荐使用适合个人的第三方工具。
### WinMerge
[下载](https://winmerge.org/)安装后，打开软件、选择 “文件” -> “打开”，在弹出对话框输入要比较的两个目录路径，确定后、点击"Compare"，WinMerge以图形化界面展示差异。

### KDiff3 
[下载](https://kdiff3.sourceforge.net/)安装KDiff3后，打开软件，通过界面选择要比较的两个目录，KDiff3 以图形化方式展示差异，方便直观查看并处理不同之处。




#Windows #WinMerge