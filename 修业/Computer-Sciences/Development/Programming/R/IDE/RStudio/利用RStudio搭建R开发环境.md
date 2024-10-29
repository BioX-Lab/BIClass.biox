# 利用RStudio搭建R开发环境

> 本文主要以Windows操作系统为例。
>
## 下载并安装RStudio

从官网(https://posit.co/)下载RStudio，官网首页右上角提供下载链接，RStudio分为Desktop与Server版两种，这里选择Desktop桌面版，根据个人操作系统选择对应安装软件即可，一般选择最新版本即可。
 下载完成后，双击安装包、像其它软件一样根据提示，安装即可；有需要时可以调整安装路径，否则都采用默认值即可。



## 下载并安装R引擎

RStudio只是集成开发环境，如果需要运行R程序，需要安装R解释器或者引擎。
从[R官网](https://cran.r-project.org/)下载R引擎，根据个人操作系统选择相应版本，一般选择最新版本即可，安装过程按照提示进行，安装语言尽量用”English”，其中到了”Select Components”界面，大部分64位用户，可以把”32-bit files”取消选择，之后继续安装至完成。



## RStudio相关配置
打开RStudio，即可进行开发；如果桌面没有RStudio快捷图标，可以自己添加一下；其中RStudio会自动找出刚才安装的R解释器，使用默认即可，如果有多个R解释器，可以自己进行配置 (Tools->Global Options->General->Basic->R Sessions)，同时可以在该配置中设置一下工作目录，后续新建的项目默认都会在该目录下；配置了工作目录后，点击一下”Options”窗口的”Apply”按钮，完成配置。



## 新建R项目

选择”File”->”New Project”, 出现”New Project Wizard”窗口，选择”Existing Directory”目录, 点击”Create Project”按钮，完成新项目创建；项目创建后RStudio会自动切换到该项目，可以选择”File”->”New File”->”R Script”，新建一个R文件，保存为如”test.R”，可以在该文件进行开发，点击上方”Run”运行该程序，即可在控制台看到相关结果输出; 接下来就可以打开R书籍，边学、边去实践吧！
``` R
print("Hello World!")
126+124
```

#R #RStudio 


