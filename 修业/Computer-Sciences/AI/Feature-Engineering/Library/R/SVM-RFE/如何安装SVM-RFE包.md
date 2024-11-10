# 如何安装SVM-RFE包

SVM-RFE (https://github.com/johncolby/SVM-RFE)是一个R包，实现了支持向量机递归特征消除（mSVM-RFE）算法，用于特征选择和排序。本项目README文档中有安装说明，本文以BIClass_py310 Conda环境和Windows环境为例介绍如何安装SVM-RFE包。

## 获得安装包

``` bash
## 打开资源管理器、进入SVM-RFE需要安装的目录，在地址栏输入`cmd`，进入命令行窗口
## 如何没有安装git，也可以在项目地址下载压缩包、解压
git clone https://github.com/johncolby/SVM-RFE.git

```
## 软件安装

``` R
## 进入SVM-REF所在目录，启动cmd和BIClass_py310中的R控制台
## 安装e1071包
install.packages('e1071')

## 加载e1071包
library(e1071)

## 运行'msvmRFE.R'脚本
source('msvmRFE.R')

## 之后即可使用SVM-REF相关函数

```

## 写在后面

本软件包已很久没有更新，并且开发并不成熟，可以进一步优化、完善。


#Feature-Engineering #SVM-RFE #R

