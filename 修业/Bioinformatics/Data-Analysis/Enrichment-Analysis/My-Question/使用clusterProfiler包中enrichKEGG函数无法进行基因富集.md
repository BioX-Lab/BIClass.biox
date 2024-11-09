# 使用clusterProfiler包中enrichKEGG函数无法进行基因富集

[BI2022/BJ/20241108]


## 原始代码

```R
library(clusterProfiler)
gene_list=c(264895,28169,228061)
enrichment_result=enrichKEGG(gene = gene_list,keyType = 'kegg', organism = "hsa", pvalueCutoff =0.05, qvalueCutoff =1,use_internal_data = FALSE)

```
## 问题
执行完原始代码后enrichment_result为空。

## 问题解析

``` R
## 出现问题的原因为不清楚个人的数据和函数相关参数的意义；本案例中gene_list为小鼠的基因列表，但enrichKEGG中organism参数却设置为了人类，应当更改为：
enrichment_result=enrichKEGG(gene = gene_list,keyType = 'kegg', organism = "mmu", pvalueCutoff =0.05, qvalueCutoff =1,use_internal_data = FALSE)

```
## 小结
- 数据分析过程中，对个人的数据要有非常清晰的认识；如本例gene_list为小鼠的基因列表。
- R函数相关的参数要明白相关意义，如不清楚本案例enrichKEGG函数中organism参数的意义。

#Enrichment #R #clusterProfiler
