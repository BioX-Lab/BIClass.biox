# 如何安装GitHub中的R包

可以使用`devtools`包在线安装GitHub等多种来源的R包；可以在R控制台通过命令`install.packages("devtools")`从CRAN（Comprehensive R Archive Network）安装；可以通过如下方案安装相应包。

假设要安装的GitHub R包的用户名为`username`，包名为`package - name`，仓库路径格式通常为`username/package - name`。

## 使用`install_github`函数

``` r
     library(devtools)
     install_github("username/package - name")
```

## 指定引用方式安装（适用于特殊情况）

### 安装某个特定分支`branch - name`的包

``` r
     library(devtools)
     install_github(repo = "username/package - name", ref = "branch - name")
```
### 安装某个提交（假设提交哈希值为`commit - hash`）的包

``` r
     library(devtools)
     install_github(repo = "username/package - name", ref = "commit - hash")
```

## 注意事项

### 权限问题
如果是私有仓库，需要设置认证信息，首先在GitHub上生成个人访问令牌（Personal Access Token），在GitHub设置中的“Developer settings” - >“Personal access tokens”中生成；然后在R控制台中配置令牌、安装。

``` r
    library(devtools)
    # 假设token是你的个人访问令牌
     Sys.setenv(GITHUB_PAT = "token")
     install_github("username/package - name")
```
### 依赖问题
如果安装过程中提示缺少依赖包，需要先安装依赖包。这些依赖包可能来自CRAN，也可能来自其他GitHub仓库。

#GitHub #R