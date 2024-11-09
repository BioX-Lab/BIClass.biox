# R版本与升级

## 查看R版本

打开R控制台，输入命令`version`，即可查看。

```R
version
```

## R升级

### 使用installr包
> 通过R控制台升级

```R
# 安装installr包
install.packages("installr")
# 加载包，升级
library(installr)
updateR()
```

```R
# 查看升级后版本
version
```
#R 
