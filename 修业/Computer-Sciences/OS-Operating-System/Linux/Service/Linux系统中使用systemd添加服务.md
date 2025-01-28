# Linux系统中使用systemd添加服务

systemd是Linux系统中常用的初始化系统，用于管理系统服务。

## 创建服务脚本
服务脚本通常是一个可执行的shell脚本或其他可执行程序。
### 示例程序
创建一个简单的Python脚本作为服务示例。
```python
#!/usr/bin/env python3

print("Hello, this is a test service.")
```
将上述代码保存为`test_service.py`，并确保该脚本具有可执行权限，可使用命令`chmod +x test_service.py`来添加权限。

## 创建服务单元文件
服务单元文件用于定义服务的各种属性和行为。在`/etc/systemd/system/`目录下创建一个以`.service`为后缀的文件，例如`test.service`。

### 示例“test.service”
```
[Unit]
Description=Test Service
After=network.target

[Service]
ExecStart=/path/to/test_service.py
Restart=always

[Install]
WantedBy=multi-user.target
```
#### Unit
`[Unit]`部分用于定义服务的基本信息和依赖关系。`Description`是服务的描述，`After`表示该服务在`network.target`启动后启动。
#### Service
`[Service]`部分定义了服务的启动命令和重启策略。`ExecStart`指定了服务的启动命令，这里是刚才创建的Python脚本的路径。`Restart=always`表示服务在任何情况下停止后都自动重启。
#### Install
`[Install]`部分定义了服务安装的相关信息。`WantedBy=multi-user.target`表示当系统进入多用户模式时，该服务应该被启动。

## 重载systemd配置
完成服务单元文件的创建后，需要重载systemd配置，使新的服务单元文件生效，可以使用`sudo systemctl daemon-reload`命令。
## 启动服务
使用`sudo systemctl start test.service`以下命令启动服务。
## 查看服务状态
可以使用`sudo systemctl status test.service`命令查看服务的运行状态，该命令会显示服务是否正在运行、启动时间、日志等信息。

## 设置开机自启
如果希望服务在系统开机时自动启动，可以使用`sudo systemctl enable test.service`命令。

#Linux #systemd