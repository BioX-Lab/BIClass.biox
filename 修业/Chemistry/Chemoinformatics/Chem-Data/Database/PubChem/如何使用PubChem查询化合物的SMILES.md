# 如何使用PubChem查询化合物的SMILES

## PubChem网站查询
### 访问PubChem网站
打开浏览器，进入 PubChem 的官方网站（https://pubchem.ncbi.nlm.nih.gov/）。

### 搜索化合物
在搜索框中输入想要查询的化合物的名称、CAS 号或其他标识符。例如，如果你想查询乙醇，可以直接在搜索框中输入“ethanol”。

### 查看化合物详情页面
点击搜索结果中你所关注的化合物，进入该化合物的详情页面。

### 找到SMILES信息
- 在化合物的详情页面中，通常可以在“Names and Identifiers”等类似的栏目下找到该化合物的 SMILES 信息（对于乙醇，其 Canonical SMILES 为 `CCO`）。


## PubChem网站API查询

### 示例程序

```python
import requests


def get_smiles_from_pubchem(compound_name):

    """

    根据化合物名称从PubChem数据库获取其SMILES表示。

  

    参数:

    compound_name (str): 化合物的名称。

  

    返回:

    str: 化合物的SMILES表示，如果请求成功并找到化合物则返回SMILES，否则返回None。

    """

    # 构建请求URL，将化合物名称插入到URL中以查询相应的SMILES

    url = f"https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/name/{compound_name}/property/CanonicalSMILES/TXT"

    # 发起GET请求到PubChem数据库

    response = requests.get(url)

    # 检查HTTP响应状态码，200表示请求成功

    if response.status_code == 200:

        # 从响应中提取SMILES信息，并去除可能的前后空格

        smiles = response.text.strip()

        # 返回化合物的SMILES表示

        return smiles

    else:

        # 如果请求未成功，打印错误信息

        print(f"Error: {response.status_code}")

        # 返回None表示未能获取SMILES信息

        return None

  

# 示例：查询乙醇的 SMILES

compound_name = "ethanol"

# 调用函数获取乙醇的SMILES表示

smiles = get_smiles_from_pubchem(compound_name)

# 检查是否成功获取SMILES，如果是，则打印出来

if smiles:

    print(f"The SMILES of {compound_name} is: {smiles}")
```



#PubChem #SMILES