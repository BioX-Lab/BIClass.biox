# 在BASH中创建文件（夹）

## 创建文件夹
### 使用`mkdir`命令
 `mkdir`命令用于创建目录。基本语法是`mkdir [选项] 目录名`，如`mkdir new_folder`命令。

 如果要创建多级目录，例如要创建`parent/child`这样的嵌套目录结构，可以使用`-p`选项，如`mkdir -p parent/child`命令， 其中`-p`选项会自动创建中间缺失的目录。
## 创建文件
### 使用`touch`命令
`touch`命令主要用于更新文件的访问时间和修改时间。如果文件不存在，它会创建一个空文件，如`touch new_file.txt`命令。
### 使用重定向操作符`>`
可以通过重定向操作符`>`来创建文件，如`echo "This is a test." > example_file.txt`命令。

如果只是想创建一个空文件，可以使用`> empty_file.txt`命令。
### 使用`cat`命令和重定向操作符`>`
`cat`命令用于连接文件并打印到标准输出。与重定向操作符`>`结合也可以创建文件，如`cat > file_from_cat.txt`命令会创建一个名为`file_from_cat.txt`的文件，并将用户输入的内容写入文件（用户需要按下`Ctrl + D`来结束输入）。



#BASH #File #Directory