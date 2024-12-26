# 使用Samtools基于位置信息提取SAM文件子集


## 安装Samtools
Samtools是处理SAM和BAM（二进制的SAM）文件的常用工具。可以从官方网站（http://www.htslib.org/）下载源代码并按照说明进行编译安装，或者使用包管理器进行安装。

## 按染色体和位置范围提取

假设要从input.sam文件中提取比对到chr1染色体上，位置在 1000 到 2000 之间的读段。
如果输入的 SAM 文件是未压缩的 SAM 文件（比如你这里的 input.sam），`samtools` 会期望该文件有对应的索引文件存在，以便能够快速定位到指定位置去提取对应的读段信息；可以采用如下方案。
### 转换为合适格式并建立索引
- 将 `SAM` 文件转换为 `BAM` 文件：使用 `samtools view` 命令将现有的 `SAM` 文件转换为 `BAM` 文件，示例命令`samtools view -Sb input.sam > input.bam`，这里 `-Sb` 选项表示输入是 `SAM` 文件（`-S`），输出要转换为 `BAM` 文件（`-b`），这样就把原始的 `SAM` 文件转换成了二进制的 `BAM` 文件，其处理效率通常比 `SAM` 文件更高，且后续方便建立索引。
- 为 `BAM` 文件建立索引：使用 `samtools index` 命令为刚生成的 `BAM` 文件建立索引，示例命令`samtools index SRR8433690_Aligned.out.bam`，执行完这个命令后，会生成和 `BAM` 文件同名但后缀为 `.bai` 的索引文件（比如 `input.bam` 对应的索引文件就是 `input.bam.bai`）。
- 执行提取子集命令：使用已经有索引的 `BAM` 文件来进行基于位置的读段提取了，使用命令`samtools view -h input.bam chr1:1000-2000 > output.sam`
### 压缩 `SAM` 文件并建立索引（如果想保留 `SAM` 格式）
- 压缩 `SAM` 文件为 `SAM.gz` 格式：使用 `gzip` 工具来压缩 `SAM` 文件，示例命令`gzip input.sam`，执行后会生成 `input.sam.gz` 的压缩文件。
- 为 `SAM.gz` 文件建立索引：使用 `samtools index` 命令同样可以为 `SAM.gz` 文件建立索引，示例命令`samtools index input.sam.gz`,会生成对应的 `input.sam.gz.bai` 索引文件。
- 执行提取子集命令：用有索引的 `SAM.gz` 文件来提取子集，示例命令`samtools view -h input.sam.gz chr1:1000-2000 > output.sam`

## 仅按位置提取（不指定染色体）
如果不关心染色体信息，只关注读段的位置范围，例如提取位置在500到1500之间的读段（假设文件中染色体名称统一），可以先将SAM文件转换为BAM文件（因为BAM文件处理更高效），然后进行提取。
- 转换为BAM文件：`samtools view -Sb input.sam > input.bam`
- 对BAM文件进行索引（这是为了加快提取速度）：`samtools index input.bam`
- 提取子集：`samtools view -h input.bam 500 - 1500 > output.sam`

#SAM #samtools 