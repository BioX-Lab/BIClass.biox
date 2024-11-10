# BiocManager安装Biocondutor包时下载速度太慢

在国内通过BiocManager安装Bioconductor相应包时，如果遇到下载速度慢的情形，可以通过设置国内Bioconductor镜像源解决。
在R控制台中执行`options(BioC_mirror = "https://mirrors.ustc.edu.cn/bioc/")`，也可以使用https://mirrors.tuna.tsinghua.edu.cn/bioconductor/等镜像源。


#R #Bioconductor #BiocManager
