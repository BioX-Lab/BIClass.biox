# 使用Perlbrew管理Perl版本
Perlbrew（https://perlbrew.pl/）是一个用于在类Unix系统上安装和管理多个Perl版本的工具，它允许用户在同一系统中轻松切换不同的Perl版本，而不会相互干扰。
## 安装Perlbrew
可以通过运行`curl -L https://install.perlbrew.pl | bash`命令从命令行安装Perlbrew，或者运行`wget -qO- https://install.perlbrew.pl | bash`命令进行安装。
### 配置环境变量
为了能够在任意目录下使用`perlbrew`，需要配置环境变量。perlbrew默认安装在`~/perl5/perlbrew/`，在`~/.bashrc`中添加`source ~/perl5/perlbrew/etc/bashrc`，重新打开一个终端即可正常使用`perlbrew`。
## 使用Perlbrew管理Perl版本
### 安装Perl版本
安装特定版本的Perl，例如安装Perl 5.32.1，可以运行`perlbrew install 5.32.1`命令。
### 切换Perl版本
使用`perlbrew switch`命令来切换Perl版本。例如，要切换到刚刚安装的5.32.1版本，使用`perlbrew switch 5.32.1`命令。
### 列出已安装的Perl版本
可以使用`perlbrew list`命令查看当前系统中已安装的所有Perl版本。

#Perl #Perlbrew
