# 使用biomaRt获取基因的启动子序列

在个人R开发环境中，确保`biomaRt`已安装。

``` R

# 加载biomaRt包
library(biomaRt)

# 连接到Ensembl数据库，这里以人类基因组为例
mart <- useMart("ensembl", dataset = "hsapiens_gene_ensembl")

# 提取基因"IL17A"（Entrez Gene ID: 3605）的启动子序列，此例设置为基因上游500bp
getSequence(id = 3605, type="entrezgene_id",seqType="gene_flank",upstream=500, mart=ensembl)
```



#Promoter #biomaRt