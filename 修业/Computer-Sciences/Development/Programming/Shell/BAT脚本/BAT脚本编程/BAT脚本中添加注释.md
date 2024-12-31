# BAT脚本中添加注释

## 单行注释
在`BAT`脚本中，使用`rem`关键字或者`::`来添加单行注释。
### 示例程序
```bat
@echo off
rem 这是一个注释，用于说明下面的变量dir1的用途
set "dir1=C:\path\to\directory1"
:: 这也是一个注释，同样可以说明变量的用途
set "dir2=C:\path\to\directory2"
```
## 多行注释
`BAT`脚本没有专门的多行注释语法，但可以通过使用`goto`语句和标签来模拟多行注释。

### 示例程序
```bat
@echo off
:comment
这是第一行注释内容
这是第二行注释内容
这是第三行注释内容
goto:eof
rem 下面开始是实际的脚本代码
set "dir1=C:\path\to\directory1"
set "dir2=C:\path\to\directory2"
```
在这里，定义了一个标签`:comment`，然后在标签下面写了多行想要注释的内容。`goto:eof`语句会让脚本直接跳转到文件末尾（`eof`代表`End - Of - File`），从而跳过了这些注释内容，使得这些内容不会被当作脚本命令执行。不过这种方法会增加脚本的复杂性，并且如果脚本本身已经有很多`goto`语句和标签，可能会引起混淆。所以对于简单的多行注释，更建议将`rem`或`::`放在每一行的开头来逐行注释。


#BAT #Comment