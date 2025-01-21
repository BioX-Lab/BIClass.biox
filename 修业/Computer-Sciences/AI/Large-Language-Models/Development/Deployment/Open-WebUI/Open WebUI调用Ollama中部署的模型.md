# Open WebUI调用Ollama中部署的模型

## 设置环境变量
>以Linux CentOS系统为例。

如果以systemd服务形式运行Ollama，可以使用`systemctl`设置环境变量。

通过运行`sudo systemctl edit ollama.service`命令或者直接使用VI编辑器打开服务配置。
在`[Service]`部分下添加以下行：
``` /etc/systemd/system/ollama.service
Environment="OLLAMA_MODELS=/new/path/to/models"
```
保存文件，然后重新加载 systemd 并重新启动服务。
``` bash
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

## 运行Open WebUI
可以使用Docker运行Open WebUI。
``` bash
# 如果Ollama在本地计算机
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

# 如果Ollama在其它计算机
docker run -d -p 3000:8080 -e OLLAMA_BASE_URL=https://example.com -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```


#Open-WebUI #Ollama