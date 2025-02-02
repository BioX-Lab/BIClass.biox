# 使用update_blastdb.pl下载或更新本地BLAST数据库

BLAST（Basic Local Alignment Search Tool）是一种常用的生物信息学工具，用于序列比对和相似性搜索。为了进行本地 BLAST 搜索，需要下载并维护本地的 BLAST 数据库，NCBI 提供了一个Perl脚本`update_blastdb.pl`，用于方便地下载或更新本地的BLAST数据库。

## 安装 `update_blastdb.pl`
`update_blastdb.pl` 是 NCBI BLAST+ 工具包的一部分。如果你还没有安装 BLAST+，可以从 NCBI 的 FTP 站点下载并安装。

### 下载 BLAST+
根据本地系统类型选择[NCBI BLAST+](https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/)相应版本进行下载（推荐使用预编译版本）。
### 安装BLAST+
解压下载的文件，并将其中的`bin`目录添加到系统的 `PATH` 环境变量中。

## 使用 `update_blastdb.pl` 下载或更新数据库

`update_blastdb.pl` 脚本可以用于下载或更新本地的 BLAST 数据库。

### 下载单个数据库

要下载单个数据库（例如 `nr` 数据库），可以使用`update_blastdb.pl --decompress nr`命令，其中，`--decompress`：自动解压下载的数据库文件，`nr`: 要下载的数据库名称。

### 下载多个数据库

可以一次性下载多个数据库，例如 `nr` 和 `nt` 数据库`update_blastdb.pl --decompress nr nt`。
### 更新本地数据库
如果已经下载了某个数据库，并且想要更新到最新版本，可以使用`update_blastdb.pl --decompress --force nr`命令，其中，`--force`: 强制更新数据库，即使本地已经存在该数据库。

### 下载特定版本的数据库

如果需要下载特定版本的数据库，可以使用 `--version` 参数`update_blastdb.pl --decompress nr --version 5`，其中`--version 5`: 下载第 5 版的 nr 数据库。

## 其他常用选项

- `--quiet`: 静默模式，不显示下载进度信息。
- `--verbose`: 显示详细的下载信息。
- `--passive`: 使用被动 FTP 模式下载。

## 注意事项
- **网络连接**: 由于 BLAST 数据库文件通常较大，确保你有稳定的网络连接。
- **磁盘空间**: 下载前检查磁盘空间，确保有足够的空间存储数据库文件。
- **权限**: 确保有权限在指定的目录中下载和解压文件。


#BLAST
