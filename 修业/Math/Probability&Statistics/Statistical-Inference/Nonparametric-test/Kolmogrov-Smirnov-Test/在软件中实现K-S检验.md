# 在软件中实现K-S检验

Kolmogorov-Smirnov检验（简称K-S检验）是一类常见的一元非参数检验方法，特别是当数据的分布未知或者不满足常见的参数分布假设时。在许多统计软件中都可以进行K-S检验，如R与Python等。
## R语言

在R中可以使用`ks.test()`函数进行单（或双）样本K-S检验。

``` R
## 单样本K-S检验
# 生成一个正态分布样本x,可以替换为实际样本
x <- rnorm(100)
# 检验x是否服从正态分布
ks.test(x, "pnorm", mean(x), sd(x))
# 结果中p值较大，说明在给定的显著性水平下，不太容易拒绝原假设，样本符合正态分布

## 双样本K-S检验
# 正态分布样本x和均匀分布样本y，可以替换为实际样本数据
x <- rnorm(60)
y <- runif(40)
# 检验两个样本是否来自同一个分布
ks.test(x,y)
# 结果中p值小，代表拒绝原假设的证据越强，两个样本来自不同分布

```
## Python
`scipy.stats`模块中的`kstest()`函数可以用于单样本K-S检验，`ks_2samp()`函数用于双样本K-S检验。
### 单样本K-S检验

``` python
!pip install scipy
import numpy as np
from scipy.stats import kstest

# 生成100个符合均值为0，标准差为1的正态分布的随机数样本x
x = np.random.normal(loc=0, scale=1, size=100)  
# 进行单样本K-S检验，检验数据是否服从正态分布
# 这里使用 'norm' 表示正态分布，同时需要指定正态分布的参数（均值和标准差）
# 对于来自已知分布的数据，通常可以用样本均值和样本标准差作为参数估计值
result = kstest(x, 'norm', args=(np.mean(x), np.std(x)))

print("检验统计量:", result.statistic)
print("p值:", result.pvalue)
if result.pvalue > 0.05:
    print("在显著性水平0.05下，不能拒绝数据来自正态分布的原假设")
else:
    print("在显著性水平0.05下，拒绝数据来自正态分布的原假设")
    
```
### 双样本K-S检验

``` python
import numpy as np
from scipy.stats import ks_2samp

# 生成两组不同的正态分布数据样本x1和小
x1 = np.random.normal(loc=0, scale=1, size=80)  # 均值为0，标准差为1，共80个数据
x2 = np.random.normal(loc=1, scale=1.2, size=100)  # 均值为1，标准差为1.2，共100个数据

# 进行双样本K-S检验
result = ks_2samp(x1, x2)

print("检验统计量:", result.statistic)
print("p值:", result.pvalue)
if result.pvalue > 0.05:
    print("在显著性水平0.05下，不能拒绝两组数据来自相同分布的原假设")
else:
    print("在显著性水平0.05下，拒绝两组数据来自相同分布的原假设")
    
```

#非参检验 #K-S检验 #R #Python 