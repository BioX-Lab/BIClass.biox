# 使用crontab定期执行脚本
`crontab` 是一个用于在 Linux 和 Unix 系统上定期执行任务的工具。
## 准备脚本
首先，需要有一个要定期执行的脚本。这里以一个简单的 Bash 脚本为例，创建一个名为 `test_script.sh` 的脚本，该脚本会将当前时间写入一个日志文件。

``` bash
#!/bin/bash
echo "Script executed at $(date)" >> /path/to/your/logfile.log
```
### 脚本权限设置
确保脚本具有可执行权限`chmod +x test_script.sh`。
## 编辑`crontab`文件
### 为当前用户编辑
使用`crontab -e`命令打开当前用户的 `crontab` 文件，如果是第一次使用，系统会让你选择一个文本编辑器，选择你熟悉的编辑器（如 `nano` 或 `vim`）即可。
### 为系统全局编辑
编辑 `/etc/crontab` 文件，但这种方式通常用于系统级任务，需要 root 权限，`sudo vi /etc/crontab`。
## 添加定时任务
在打开的 `crontab` 文件中，按照 `crontab` 的语法添加定时任务。
``` plaintext
* * * * * command_to_execute
- - - - -
| | | | |
| | | | +----- 星期 (0 - 7) (0 or 7 表示周日)
| | | +------- 月份 (1 - 12)
| | +--------- 日期 (1 - 31)
| +----------- 小时 (0 - 23)
+------------- 分钟 (0 - 59)
```
例如，如果想让脚本每小时执行一次，可以在 `crontab` 文件中添加以下行：
```plaintext
0 * * * * /path/to/your/test_script.sh
```
如果想让脚本每天凌晨 2 点执行，可以添加：
```plaintext
0 2 * * * /path/to/your/test_script.sh
```
## 保存并退出
编辑完成后，保存并退出文本编辑器。如果你使用的是 `nano`，可以按 `Ctrl + X`，然后按 `Y` 确认保存，最后按 `Enter` 退出。如果你使用的是 `vim`，可以按 `Esc` 键，然后输入 `:wq` 保存并退出。
## 验证定时任务
可以使用`crontab -l`命令查看当前用户的 `crontab` 列表。
## 日志查看
`cron` 任务的执行日志通常记录在 `/var/log/syslog` 或 `/var/log/cron` 文件中，可以使用`tail -f /var/log/syslog`命令查看日志。


#Linux #crontab