# 如何使用BLAST比对两条序列

[BI2023/MJY/20241118]

BLAST常用场景为快速搜索序列数据库，此外，也可以进行两条序列的比对，特别是查看两条序列的局部相似情况，以下为示例命令。

``` bash
#假设有两条核酸序列，分别在H5.fasta和B2.fasta文件中
#用blastn对两条核酸序列进行比对
#将输出结果设置为BLAST XML格式
blastn -query H5.fasta -subject B2.fasta -outfmt 5 -evalue 1 -out result.xml
#如果需要调整其它参数，可以查阅帮助文档
blastn -help
```

#BLAST 