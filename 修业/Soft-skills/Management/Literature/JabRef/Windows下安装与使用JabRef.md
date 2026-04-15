# Windows下安装与使用JabRef
> 这里以Windows为例介绍JabRef的安装与基本使用，其它操作系统类似。

JabRef 是一个用于管理参考文献的工具，特别适合：
- 管理 `$BibTeX$` / `$BibLaTeX$` 文献库
- 配合 LaTeX 写论文
- 整理论文条目和 PDF 文件
- 维护个人文献数据库
## 安装 JabRef

推荐直接从官网下载 Windows 安装包：
- 官网：<https://www.jabref.org/>
安装步骤：
- 打开官网
- 进入 Download 页面
- 下载 Windows 版本安装程序
- 双击安装包
- 按提示完成安装
安装完成后，就可以在开始菜单中启动 JabRef。
## 基本使用流程

### 新建文献库

打开 JabRef 后：
- 点击 `File -> New library`
- 保存为 `references.bib`
### 添加文献

最常用的方法是通过 DOI 导入。
操作思路：
- 在论文页面复制 DOI
- 在 JabRef 中选择通过标识符导入
- 粘贴 DOI
- 自动生成文献条目
如果没有 DOI，也可以：
- 手动新建条目
- 从 PDF 识别元数据
- 通过 ISBN、arXiv 等方式导入
### 关联 PDF
添加文献后，可以把对应 PDF 绑定到条目上。
建议做法：
- 所有 PDF 统一放在 `pdfs` 文件夹
- 一个条目尽量对应一个 PDF
- 文件名保持清晰统一
### 搜索和整理文献

当文献变多后，可以用 JabRef 来：
- 搜索作者
- 搜索标题关键词
- 按年份筛选
- 查看哪些条目还没有 PDF
如果有需要，也可以按主题建立分组，比如：
- 待读
- 已读
- 综述
- 方法类
- 某个项目相关

#JabRef