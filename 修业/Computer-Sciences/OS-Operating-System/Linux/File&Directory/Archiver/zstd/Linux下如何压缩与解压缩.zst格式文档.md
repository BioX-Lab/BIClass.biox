# Linux下如何压缩与解压缩.zst格式文档
`.zst`是 Zstandard 压缩格式的文件扩展名，Linux下可以使用`zstd`工具进行相应压缩与解压缩，以下为简明示例，如有需要可以通过`zstd --help`查看详细参数说明。
## 压缩操作
打开终端，进入文件所在的目录。假设要压缩一个名为`example.txt`的文件，使用命令`zstd -z example.txt`。
## 解压缩操作
如果要解压缩`example.txt.zst`文件，在终端中进入文件所在目录，使用命令`zstd -d example.txt.zst`。


#Linux #zstd #Archiver