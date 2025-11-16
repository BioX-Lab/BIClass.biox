# 使用SSH克隆GitHub仓库时遇到22端口连接被拒绝的解决方案


由于校园网等特殊网络环境可能存在限制了22端口访问的情形，当使用SSH方式克隆GitHub仓库时，可能会遇到`port 22: Connection refused`错误。可以通过443端口（HTTPS常用端口，通常不会被限制）连接GitHub解决。

## 创建/编辑SSH配置文件
创建或编辑`~/.ssh/config`文件，在`config`文件中添加以下内容。
``` plaintext
Host github.com
	HostName ssh.github.com
	Port 443
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa #如果本地不存在私钥文件`id_rsa`，可以通过`ssh-keygen`生成；并确保公钥（`id_rsa.pub`中的内容）已添加到GitHub账户的SSH keys中（Settings->SSH and GPG keys->New SSH key）
```

## 测试连接
执行`ssh -T git@github.com`命令验证是否能成功连接，如果看到类似`Hi <你的用户名>! You've successfully authenticated...`的提示，说明配置成功。

如果仍出现连接失败，可尝试删除`.ssh`目录下的`known_hosts`文件（清除旧连接记录），再重新测试。

#GitHub #SSH 