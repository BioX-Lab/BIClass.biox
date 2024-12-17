# 使用prefetch从SRA下载测序数据

从NCBI SRA数据库下载相关数据时，建议安装、使用SRA Toolkit（https://github.com/ncbi/sra-tools），使用其中的`prefetch`命令下载相关数据。
安装SRA Toolkit时推荐根据个人操作系统下载预编译版本（https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/）。

## 确定下载对象
SRA包含不同类型（层次）的数据，根据研究目的，选择相应的下载对象，如BioProject或SRA Run等。

## 示例
### 下载某一BioProject的全部数据
``` bash
# prefetch工具就会根据SRA数据库中与‘PRJNA779153’关联的所有相关数据（比如包含的各个 `BioSample` 对应的测序数据、不同 `Experiment` 产生的数据等，也就是对应的 `SRR` 等相关数据文件）尝试进行下载
# -X 100G表示限制下载的数据量最多占用100GB的磁盘空间
# 可以通过`prefetch --help`查看帮助文档，如通过--output-directory指定下载目录
prefetch -X 100G  PRJNA779153
```
### 下载某一SRA Run的测序数据文件

``` bash
prefetch SRR000002
```

#NCBI #HTS #SRA #prefetch
