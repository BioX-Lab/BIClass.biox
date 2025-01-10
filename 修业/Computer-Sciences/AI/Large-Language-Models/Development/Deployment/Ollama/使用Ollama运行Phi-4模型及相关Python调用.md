# 使用Ollama运行Phi-4模型及相关Python调用


## 安装 Ollama
根据个人操作系统选择合适的安装方式，以 Linux CentOS为例。
使用`curl -fsSL https://ollama.com/install.sh | sh`命令安装（需要具备sudo权限），安装完成后，可以通过 `ollama --version` 命令来验证是否安装成功。
### 启动Ollama
安装成功后，启动 Ollama 服务（不同操作系统启动方式略有不同，一般安装完成后会自动配置好相关的服务启动项，或者可以手动在终端输入相应命令启动，例如在 Linux 下可以直接输入 `ollama serve` 启动服务）。

### 添加Ollama为系统服务（可选）
可以通过`systemd`添加Ollama为系统服务。

#### 示例配置文件

``` /etc/systemd/system/ollama.service
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
ExecStart=/usr/local/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3
Environment="OLLAMA_HOST=0.0.0.0" 


[Install]
WantedBy=default.target
```
#### 服务重载和重启

``` bash
# 重载配置文件
sudo systemctl daemon-reload
# 重启ollama服务
sudo systemctl restart ollama
# 查看ollama服务状态
sudo systemctl status ollama.service
```

## 下载 Phi-4 模型
在终端（命令提示符、PowerShell 或者 Linux/macOS 下的 Shell 等）中，输入以下命令来下载 `Phi-4` 模型（前提是 Ollama 服务已正常启动）。
```bash
ollama pull phi4
```
这个过程会从对应的模型源下载 `Phi-4` 模型到本地计算机，下载时间取决于服务器的网络带宽以及模型的大小等因素。
模型默认存放位置在"/usr/share/ollama/.ollama/models"(`macOS为~/.ollama/models, Windows为C:\Users\<username>\.ollama\models`)。

## 使用Python 调用 Ollama API（以 `requests` 库为例）
在`BIClass_py310` conda环境中，安装 `requests` 库（如未安装、可以通过 `pip install requests` 命令安装）。

### 调用 Ollama 中`Phi-4`模型的 API 来生成文本示例
``` python
import json

import requests

# Ollama API 的默认本地地址和端口，可根据实际配置修改
url = "http://localhost:11434/api/chat"

headers = {
    "Content-Type": "application/json"
}
# 要发送的数据
data = {
    "model": "phi4",
    "messages": [
        {"role":"system","content": "你是一位有爱心的高等教育学家。"},
        {"role": "user","content": "不该上大学的学生上了大学会有什么收获或变化"}
    ],
    "stream": False
}

# 将字典转换为JSON格式的字符串
json_data = json.dumps(data)

# 发送POST请求
response = requests.post(url, data=json_data, headers=headers)

# 打印响应内容
print(response.text)

```


#LLMs #Ollama #Phi-4