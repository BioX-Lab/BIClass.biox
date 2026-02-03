# 解决Windows系统中出现Git项目文件名过长问题

在 Git 项目中，文件名过长的问题主要源于Windows 系统默认的文件路径长度限制，以及 Git 自身的默认配置限制，简要汇总几种解决方案。
## 即时解决当前报错
### 开启 Git 长文件名支持
在仓库目录下执行，仅对当前仓库生效：
``` bash
git config core.longpaths true
```
如果需要全局生效（所有仓库都支持长文件名）：
``` bash
git config --global core.longpaths true
```
这个配置会让 Git 允许处理超过默认长度限制的文件名。

### 重命名现有超长文件
如果已经出现回滚/提交失败，先通过命令行改短文件名：
``` bash
git mv "超长文件名.pdf" "缩写文件名.pdf"
```
建议采用[GYD文献资料命名法](https://gitee.com/biox-lab/biclass.biox/blob/master/%E4%BF%AE%E4%B8%9A/Soft-skills/Management/GYD%E6%96%87%E7%8C%AE%E8%B5%84%E6%96%99%E5%91%BD%E5%90%8D%E6%B3%95.md)，再重新执行回滚或提交操作。

### 用命令行绕过图形界面限制**
部分Git GUI工具可能会额外限制文件名长度，改用终端执行回滚/提交操作会更可靠。
``` bash
git revert <commit-id>
# 或
git commit -m "提交信息"
```

## 长期预防方案
### 制定文件名规范

建议采用[GYD文献资料命名法](https://gitee.com/biox-lab/biclass.biox/blob/master/%E4%BF%AE%E4%B8%9A/Soft-skills/Management/GYD%E6%96%87%E7%8C%AE%E8%B5%84%E6%96%99%E5%91%BD%E5%90%8D%E6%B3%95.md)。

### 启用 Windows 系统级长路径支持

- 打开「组策略编辑器」（`gpedit.msc`）
- 定位到：`计算机配置 > 管理模板 > 系统 > 文件系统`
- 启用「启用 Win32 长路径」选项

### 在 .gitignore 中过滤不必要的长文件
如果某些自动生成的超长文件不需要纳入版本控制，可以在 `.gitignore` 中添加规则排除它们。

#Git