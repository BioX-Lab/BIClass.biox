# WSL下安装PyTorch

在WSL Ubuntu中的BIClass_py310 Conda环境下安装最新稳定版PyTorch（CPU版）的命令如下：

``` bash
# 激活BIClass_py310环境
conda activate BIClass_py310
# 使用Conda或者pip安装PyTorch (二选一即可)
conda install pytorch torchvision torchaudio cpuonly -c pytorch
# pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```

## 验证PyTorch安装
在Conda环境中运行`python` 、打开Python控制台，输入如下代码进行验证。

``` python
import torch
#查看 Torch版本
print(torch.__version__)
```

#Deep-Learning #PyTorch 

