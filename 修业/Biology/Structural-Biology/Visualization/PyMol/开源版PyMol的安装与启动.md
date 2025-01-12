# 开源版PyMol的安装与启动

PyMol可以在常见的操作系统中安装与使用，这里主要以Windows系统为例进行说明（其它操作系统类似）。

## 安装

可以根据[开源版PyMol](https://github.com/schrodinger/pymol-open-source)项目的[安装说明](https://github.com/schrodinger/pymol-open-source/blob/master/INSTALL)进行安装，安装过程比较简单，但由于依赖关系等问题、在安装过程中可能会遇到未知问题；这里建议通过[Conda进行安装](https://pymol.org/conda/)。

``` dos
# 可以直接在Conda `base`环境中安装，这里新建了"pymol_310"Conda环境专门用于PyMol的安装与使用
conda create -n pymol_310 -c conda-forge python=3.10 pymol-open-source
# 如果在base环境中安装，运行如下命令
# conda install -c conda-forge pymol-open-source

# 安装后，后续如果需要升级，运行如下命令
conda activate pymol_310
conda update -c conda-forge pymol-open-source
```

## 启动

安装完成后激活相应conda环境（如`conda activate pymol_310`）后，输入`pymol`即可打开PyMol。

为便于后续启动，可以创建一个`pymol.bat`脚本、并将其添加至环境变量。

``` pymol.bat
# 将"C:\..."替换为pymol_310环境的对应路径
"C:\...\envs\pymol_310\Scripts\\..\python.exe" "C:\...\envs\pymol_310\Scripts\\..\Lib\site-packages\pymol\__init__.py"
```



#PyMol #Conda 