# 使用renv配置R开发环境


## 安装R包
```R
## renv包
install.packages("renv")

```
## 初始化项目环境

进入R项目目录（如果是新创建的项目可先新建一个目录并进入它），然后在R控制台运行：
```R
renv::init()
```
## 配置.Rprofile 文件

打开R项目目录下的 .Rprofile 文件（如果没有可创建一个），在其中添加以下内容来指定要使用的R可执行文件路径：

`Sys.setenv(R_HOME = "/path/to/your/target/R/version")`


保存 .Rprofile 文件后，重新启动R会话（关闭当前R控制台并重新打开进入项目目录启动）。此时 renv 应该会识别到新的R版本并相应地调整项目环境（它会根据新R版本重新安装或更新相关包以适配新环境等）。


## 保存项目状态

```R
# 项目用到的R包会记录在`lockfile`中，被称为`renv.lock`。
renv::snapshot()
```

## 恢复项目状态

```R
# 如果需要将项目文件夹转移到新的电脑， 重装 lockfile文件记录到(项目需要的)的R包。
renv::restore()

```

## 移除项目特定的库

```R
# 关闭当前项目的 `renv` 环境
renv::deactivate()
```


#R #renv