# 配置Conda国内镜像源

由于网络问题，使用Conda进行开发环境配置过程中，有时需要配置国内的镜像源；主要通过修改`~/.condarc`配置文件完成。

## 还原默认源（可选）
在配置前可以使用如下命令还原为默认下载通道。
```bash
# 清除以前添加的镜像源路径，只保留默认的路径
conda config --remove-key channels
cat ~/.condarc
```

## TUNA镜像源
可使用`vi ~/.condarc`修改.condarc文档，国内可优先选择清华镜像源（TUNA），如下为`.condarc`文件的示例。
``` text
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

```
其中，`show_channel_urls: true`表示显示检索路径，每次安装包时会将包源路径显示出来，可通过`conda config --set show_channel_urls yes`命令单独进行设置。

## 添加其它镜像源
也可以通过`conda config --add channels http_url`配置其它镜像源。

``` bash

# 中科大镜像源
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/

```

## 删除镜像源
不需要的镜像源可通过如下命令删除。
``` bash
conda config --remove channels http_url
```

## 显示已添加的安装镜像源

``` bash
conda config --show-sources
# 或者
conda config --show
```

#Conda