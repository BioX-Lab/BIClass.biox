# 使用Gawk测试正则表达式

## 创建测试文件test.txt并写入测试字符串（每行一个）
``` test.txt
10N
30N
4M
6S
```
## 使用gawk命令进行测试

``` bash
re="<your_regular_expression>" # 如"[0-9]+N"
gawk --re-interval -v re="$re" '{if (match($0, re)) {print "字符串 \"" $0 "\" 匹配成功"} else {print "字符串 \"" $0 "\" 匹配失败"}}' test.txt
# 或使用如下命令
#gawk --re-interval -v re="$re" '$0 ~ re {print "字符串 \"" $0 "\" 匹配成功"}!($0 ~ re) {print "字符串 \"" $0 "\" 匹配失败"}' test.txt
```

#gawk #Regular-Expression