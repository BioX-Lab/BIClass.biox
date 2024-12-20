# 使用`samtools view`命令将SAM转换为BAM文件时遇到“no SQ lines present in the header”报错

在使用samtools将SAM文件转换为BAM文件时（如使用`samtools view -bS your_sam.sam > your_bam.bam`命令），如有报错提示“no SQ lines present in the header”，是由于SAM文件头中缺少头SQ 行，SQ行在 SAM 文件头中是用于描述参考序列（比如染色体等信息）的相关内容，如果缺少 SQ 行，samtools 在解析 SAM 文件时就无法得知参考序列的相关情况，进而报错。

## 方案1
尝试重新获取这个 SAM 文件，如果是自己生成的，可以重新运行生成该 SAM 文件的流程（例如重新进行序列比对等操作来生成新的、完整无损坏的 SAM 文件）。

## 方案2


``` bash
samtools faidx hg38.fasta
#生成hg38.fai的索引文件
samtools view -bt hg38.fasta.fai chr5_pair_nos.sam >chr5_pair_nos.bam
```


#samtools #SAM #BAM