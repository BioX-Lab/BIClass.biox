# 基因名到Entrez ID映射不成功

[BI2022/BJ/20241106]

## 原始代码

```R
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("org.Mm.eg.db")

library(org.Mm.eg.db)

x0=read.table("test_input.txt",sep="\t",header=T,check.names=F)
gene_symbols=as.vector(x0[,1])
entrezIDs=mget(gene_symbols, org.Mm.egSYMBOL2EG, ifnotfound=NA) 

```
### test_input.txt示例

``` 
SYMBOL,log2FC       
Acsf2 ,  5.531904157      
Agpat3 , 7.160551664  
Agps ,   -8.139358252   
```
## 问题
执行完原始代码后entrezIDs为空。

## 问题解析

``` R
## 出现上述问题的原因主要有两处
# 第1处：test_input.txt每一行数据由","分隔，但代码中sep设置为了"\t"
x0=read.table("test_input.txt",sep="\t",header=T,check.names=F)
# 第2处：使用sep=","将每行数据分隔后，每一列的字符串前后依然有空白字符，需要将其去掉
gene_symbols=as.vector(x0[,1])
# 添加下面的代码通过trimws将gene_symbols每个元素前后的空格去掉
gene_symbols=trimws(gene_symbols)

```
## 小结
- 数据预处理（或整理）在数据分析过程中非常基础和重要，本案例主要是由于test_input.txt在准备过程中过于粗糙或者没有弄清楚要保存的格式。
- R函数相关的参数要明白相关意义，如不清楚本案例read.table函数中sep参数的意义。

#ID-Mapping
