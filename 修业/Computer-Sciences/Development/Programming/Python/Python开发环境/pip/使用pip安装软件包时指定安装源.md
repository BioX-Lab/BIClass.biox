# 使用pip安装软件包时指定安装源

在使用pip安装软件包时，如果遇到网络问题，可以通过`-i http_url`指定（国内）安装源。
``` bash
# 使用清华镜像源（TUNA）进行安装
pip install <your_package> -i https://pypi.tuna.tsinghua.edu.cn/simple
## 使用其它镜像源
# 阿里镜像源
# https://mirrors.aliyun.com/pypi/simple/

# 豆瓣的镜像的源
# http://pypi.douban.com/simple/ 
```


#pip #Python 