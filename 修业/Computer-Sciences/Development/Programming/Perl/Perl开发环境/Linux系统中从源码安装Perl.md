# Linux系统中从源码安装Perl

## 安装前准备
确保你的系统中已经安装了wget、tar、make以及编译所需的工具（如gcc等编译器及相关开发库）。如果没有安装，在 Debian 或 Ubuntu 系统中，可以使用以下命令安装：
``` bash
sudo apt - get update
sudo apt - get install wget tar make build - essential
```

在 CentOS 系统中，可以使用以下命令安装：
``` bash
sudo yum update
sudo yum install wget tar make gcc
```

### 确认安装路径
本次安装将 Perl 安装到用户主目录下的localperl目录（$HOME/localperl）。如果需要安装到其他目录，请修改./Configure命令中的-Dprefix参数。
## 下载 Perl 安装包
打开终端，执行`wget https://www.cpan.org/src/5.0/perl-5.40.1.tar.gz`命令下载 Perl 5.40.1 的压缩包。
##  解压安装包
下载完成后，执行`tar -xzf perl-5.40.1.tar.gz`命令解压压缩包，解压后会在当前目录生成一个名为`perl-5.40.1`的目录。
## 配置编译选项
``` bash
# 进入解压后的perl-5.40.1目录：
cd perl-5.40.1

# 执行配置命令
./Configure -des -Dprefix=$HOME/localperl
#-des选项含义如下：
#-d：使用默认配置。
#-e：启用扩展。
#-s：静默模式，减少输出信息。
#-Dprefix=$HOME/localperl指定了 Perl 的安装目录为用户主目录下的localperl目录。
```
## 编译Perl
执行`make`命令进行编译。编译过程可能需要一些时间，期间会输出编译信息。如果编译过程中出现错误，可能是缺少依赖库或其他问题，可以根据错误提示进行排查和解决。
## 测试编译结果
编译完成后，执行`make test`命令进行测试。如果所有测试用例都通过，会显示一系列测试成功的信息；如果有测试失败，会显示失败的测试用例和相关错误信息。如果测试失败，请根据错误提示进行调试和修复，可能需要重新检查依赖库或编译选项。
## 安装Perl
测试通过后，执行`make install`命令进行安装。安装完成后，Perl 5.40.1 就会安装到$HOME/localperl目录下。
## 配置环境变量
为了能够在任意目录下使用新安装的 Perl，需要配置环境变量。在终端中编辑.bashrc文件（如`vi ~/.bashrc`命令，如果使用的是其他 Shell，编辑相应的配置文件），在文件末尾添加以下内容`export PATH=$HOME/localperl/bin:$PATH`。保存并退出编辑器，然后执行`source ~/.bashrc`命令使配置生效。
至此，Perl 5.40.1 安装完成。你可以在终端中执行perl -v命令来验证安装是否成功。如果成功安装，会显示 Perl 的版本信息。

#Perl #Installation