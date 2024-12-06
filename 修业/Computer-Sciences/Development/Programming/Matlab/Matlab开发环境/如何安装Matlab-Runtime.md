# 如何安装Matlab Runtime

Matlab是商业化软件，但使用Matlab Runtime（曾用名MATLAB Compiler Runtime，简称MCR）可以在不安装 Matlab的情况下运行编译好的Matlab应用程序或组件。
- 首先根据相应的操作系统和Matlab版本下载相应Matlab Runtime文件（https://ww2.mathworks.cn/products/compiler/matlab-runtime.html）。
- 安装过程较为简单，比如在Windows下，双击安装程序，然后按照安装向导中的说明进行操作；在Linux下，可以在终端中切换到Runtime文件所在目录，然后运行程序`./install`，可以根据需求设置相关参数，如`./install -mode silent -agreeToLicense yes`，具体参数细节可参考`help`文档。

#Matlab #Runtime