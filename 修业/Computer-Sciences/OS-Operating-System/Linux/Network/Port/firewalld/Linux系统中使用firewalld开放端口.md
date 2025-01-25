# Linux系统中使用firewalld开放端口

在 CentOS 7 及更高版本中，`firewalld`是默认的防火墙管理工具。

## 检查firewalld状态
``` bash
sudo systemctl status firewalld
```
如果未运行，可以启动：
``` bash
sudo systemctl start firewalld
```
## 开放特定端口（以8080端口为例）
``` bash
sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent
```
## 重新加载防火墙规则
```bash
sudo firewall-cmd --reload
```
## 检查开放的端口
``` bash
sudo firewall-cmd --list-ports
```
在使用 **firewalld** 配置防火墙规则时，是否需要重启 `firewalld` 服务取决于你所做的更改和使用的命令。

## 重启 `firewalld`（可选）
在大多数情况下，建议使用 `firewall-cmd` 命令来管理防火墙规则，因为它会自动处理规则的加载和生效，无需手动重启服务。
### 不需要重启的情况
如果使用的是 `firewall-cmd` 命令，并且规则更改是通过 `--permanent` 选项完成的，那么通常不需要重启 `firewalld`。`sudo firewall-cmd --reload` 命令会重新加载防火墙规则，使更改立即生效，而无需重启 `firewalld`。

### 需要重启的情况
如果直接修改了防火墙配置文件（如 `/etc/firewalld/zones/public.xml`），而没有使用 `firewall-cmd` 命令，那么可能需要重启 `firewalld` 服务（`sudo systemctl restart firewalld`）以使更改生效。

#Linux #Port #firewalld