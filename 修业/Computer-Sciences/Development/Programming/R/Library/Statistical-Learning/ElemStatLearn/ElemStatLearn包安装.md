# ElemStatLearn包安装


ElemStatLearn（https://github.com/cran/ElemStatLearn）是The-Elements-of-Statistical-Learning-Data-Mining-Inference-and-Prediction-2nd-edition_2016_Springer图书的配套R包，该包目前已不再提供更新支持；本示例在BIClass_py310环境中安装该包。

``` R
#在Conda环境中打开R控制台
install.packages("devtools")
library(devtools)

devtools::install_github("cran/ElemStatLearn")
```

#R #ElemStatLearn