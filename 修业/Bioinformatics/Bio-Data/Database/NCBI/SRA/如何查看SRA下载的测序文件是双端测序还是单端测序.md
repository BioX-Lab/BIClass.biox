# 如何查看SRA下载的测序文件是双端测序还是单端测序

SRA（Sequence Read Archive, https://www.ncbi.nlm.nih.gov/sra ）是NCBI（National Center for Biotechnology Information）提供的一个存储高通量测序数据的数据库。要查看从SRA下载的测序文件是双端测序（paired-end）还是单端测序（single-end）可以采取如下方法。

## 使用SRA的网页界面
1. 访问NCBI的SRA数据库网页。
2. 搜索并找到您感兴趣的SRA编号，如SRR7433687等。
3. 点击进入该SRA编号的页面。
4. 在“Library”信息部分，查看“Layout”字段，它将显示是“SINGLE”还是“PAIRED”。

## 使用fastq-dump命令
如果已经从SRA下载了数据，可以使用SRA Toolkit中的fastq-dump查看：
```bash
fastq-dump --split-3 SRR7433687
```
如果输出两个.fastq文件，则表示是双端测序（通常是SRRXXXXXXX_1.fastq和SRRXXXXXXX_2.fastq）。如果只输出一个文件，则是单端测序。

#SRA #NCBI #HTS 