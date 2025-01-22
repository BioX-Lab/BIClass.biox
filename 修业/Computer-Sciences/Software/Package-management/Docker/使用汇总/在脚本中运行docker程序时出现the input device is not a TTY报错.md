# 在脚本中运行docker程序时出现the input device is not a TTY报错

在脚本中使用Docker时遇到的“the input device is not a TTY”报错，一般是由于使用了`docker run -it`命令，而-t选项会分配一个伪终端，通过将命令中的-t去掉，仅保留-i，问题得以解决。


#Docker