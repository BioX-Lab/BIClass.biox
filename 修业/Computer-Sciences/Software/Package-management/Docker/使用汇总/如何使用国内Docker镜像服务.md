# 如何使用国内Docker镜像服务
在使用Docker时，从官方Docker Hub（https://hub.docker.com/）拉取镜像可能会因为网络原因（如网络带宽限制、网络不稳定等）导致速度很慢甚至拉取失败。国内镜像服务可以提供更快速、稳定的镜像拉取服务。

## 国内Docker镜像服务

可以使用TUNA（清华大学开源软件镜像站）、阿里云、腾讯云、网易蜂巢官网等提供的镜像加速服务，并获取Docker镜像加速器地址；接下来即可修改daemon配置文件、重启docker服务。本文以CentOS 7.9为例。
> 如果出现常用的国内镜像站无法使用时，可以网络搜索可用的镜像站和镜像加速地址（[[#参考资料]]）。


## 修改daemon配置文件
修改daemon配置文件`/etc/docker/daemon.json`。
``` json
{
    "registry-mirrors": [
		"https://docker.unsee.tech",
		"https://dockerpull.org",
        "https://docker.m.daocloud.io"
    ]
}
```
## 重启`docker`
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 检查加速是否生效
查看docker系统信息 `docker info`，如果从输出结果中看到了 registry mirror 刚配置的内容地址，说明配置成功。

## 参考资料
- [目前国内可用Docker镜像源汇总 - CoderJia](https://www.coderjia.cn/archives/dba3f94c-a021-468a-8ac6-e840f85867ea)


#Docker