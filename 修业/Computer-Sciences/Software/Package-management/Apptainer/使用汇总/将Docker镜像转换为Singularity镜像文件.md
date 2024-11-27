# 将Docker镜像转换为Singularity镜像文件

可以通过在线或者离线等方式进行转换，本文适用于不同操作系统平台（需适当调整）。

## 在线转换

可以直接进行从Docker Hub等镜像库在线拉取、构建singularity镜像。
```
# 构建名为your_singularity_image.sif的镜像
singularity build your_singularity_image.sif docker://your_docker_image:tag
```
如果存在网络问题或者需要转换本地镜像等情形，可以采取离线转换。
## 离线转换

``` bash
# 打包已有镜像
docker save <IMAGE ID> -o your_docker_image.tar
# 构建Singularity镜像
singularity build your_singularity_image.sif docker-archive://your_docker_image.tar
# 构建完成后可以删除Docker打包文件
rm your_docker_image.tar
```



#Docker #Singularity