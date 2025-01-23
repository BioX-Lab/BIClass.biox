# 使用nohup命令在后台执行程序

 `nohup` 命令（“no hang up”）允许用户运行一个命令，并且该命令在用户退出登录或关闭终端后仍然继续运行。
## 示例 1
```bash
nohup sleep 10 > nohup.out 2>&1 &
# 其中，`sleep 10` 是想要执行的命令（可进行相应替换）；
# `> nohup.out 2>&1` 是将标准输出和标准错误输出重定向到 `nohup.out` 文件，这样可以记录命令的输出信息。如果不进行重定向，输出信息会默认重定向到 `nohup.out` 文件。
# `&` 操作符将命令置于后台运行；
```
## 示例 2
可以写成脚本（如"run_in_background.sh"脚本），便于后续重复使用。
``` bash
#!/usr/bin/bash

# 检查是否传入命令作为参数

if [ $# -eq 0 ]; then
  echo "请提供一个命令作为参数。"
  exit 1
fi

# 获取当前目录的绝对路径
current_dir=$(pwd)

# 检查是否传入日志文件作为参数
if [ $# -gt 1 ]; then
  log_file=$2
else
  log_file=${current_dir}/run.log # 设置默认日志文件名
fi

# 确保日志文件路径存在
log_dir=$(dirname "$log_file")
if [ ! -d "$log_dir" ]; then
  mkdir -p "$log_dir"
fi

# 使用 nohup 执行传入的命令并将其放入后台运行，同时将输出重定向到指定的日志文件
nohup $1 >> $log_file 2>&1 &

# 输出进程ID到日志文件
echo "后台进程ID: $!" >> $log_file
```

#Linux #Process #nohup