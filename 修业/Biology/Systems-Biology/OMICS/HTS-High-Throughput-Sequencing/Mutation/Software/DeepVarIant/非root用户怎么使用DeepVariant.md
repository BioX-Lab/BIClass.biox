# 非root用户怎么使用DeepVariant

## 推荐使用Docker
建议联系管理员，将个人用户添加到docker组，如`sudo usermod -aG docker <your_user_name>`。

``` bash

BIN_VERSION="1.6.1"
# Docker拉取镜像
docker pull google/deepvariant:"${BIN_VERSION}"
# 运行DeepVariant
docker run google/deepvariant:"${BIN_VERSION}" /opt/deepvariant/bin/run_deepvariant --helpfull
```

## 使用Singularity
Docker确实无法正常使用的话，可以使用singularity (现为Apptainer；可通过`conda`在`base`环境安装`conda install conda-forge::apptainer`)
``` bash
BIN_VERSION="1.6.1"
## 方案1
# 使用singularity直接拉取docker镜像
singularity pull docker://google/deepvariant:"${BIN_VERSION}"
# 运行DeepVariant
singularity run -B /usr/lib/locale/:/usr/lib/locale/ \
  docker://google/deepvariant:"${BIN_VERSION}" \
  /opt/deepvariant/bin/run_deepvariant --helpfull

## 方案2
# 如果网络等原因，可以先将docker镜像打包，并转换为singularity镜像文件
# 打包docker镜像
docker save <IMAGE ID> -o deepvariant-"${BIN_VERSION}".tar
# 保存为sigularity镜像文件
singularity build deepvariant-"${BIN_VERSION}".sif docker-archive://deepvariant-"${BIN_VERSION}".tar
# 运行DeepVariant
singularity run deepvariant-"${BIN_VERSION}".sif /opt/deepvariant/bin/run_deepvariant --helpfull
```

## Conda安装
Conda目前只能安装DeepVariant至1.5.0版本，由于依赖关系等历史问题，不建议使用。

``` bash
# 创建deepvariant-1.5.0环境、安装DeepVariant
conda create -c bioconda -n deepvariant-1.5.0 deepvariant=1.5.0
```
## 源码安装

如果是本软件的重度用户，建议研究从源码安装，对细节、依赖关系等有清晰的了解。

## 参考资料
- [deepvariant/docs/deepvariant-quick-start.md at r1.6.1 · google/deepvariant](https://github.com/google/deepvariant/blob/r1.6.1/docs/deepvariant-quick-start.md)
- 


#DeepVariant #HTS 
