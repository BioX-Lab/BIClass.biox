# Windows 下安装与配置 Cherry Studio
> 这里以Windows为例介绍Cherry Studio的安装与基本配置 ，其它系统类似。

Cherry Studio 是一个本地桌面端 AI 客户端，通常用于统一接入不同的大语言模型服务。 它的核心价值在于：
- 提供图形界面，降低调用模型的门槛
- 可以集中管理多个模型提供商
- 支持自定义 API 服务
- 适合日常对话、写作、翻译、代码辅助等场景
- 比直接手写 API 请求更方便
如果已经有模型服务的 API Key，Cherry Studio 可以作为一个比较顺手的统一入口。
## 安装前准备

开始前建议准备好以下内容：

- 一台 Windows 电脑
- 稳定的网络环境
- 可用的模型服务 API Key
- 明确你要接入的服务类型，例如：
	OpenAI 官方
	OpenAI 兼容接口
	DeepSeek
	SiliconFlow
	OpenRouter
	GitHub Copilot
	AGICTO
	本地模型中转服务

如果只是先体验客户端界面，也可以先安装，后面再配置模型接口。
## 下载安装 Cherry Studio
从[官网](https://www.cherry-ai.com/)下载安装包，下载时注意选择适合 Windows 的版本。下载完成后，双击安装包，按提示完成安装即可。  

## 首次启动

首次启动后，会提示登录CherryIN或者选择其它服务商，可以跳过引导。通常先不要急着折腾全部设置，建议按以下顺序操作。

- 先确认程序能正常打开
- 查看界面是否完整显示
- 再进入模型配置页面
- 先添加一个最常用的模型服务进行测试

## 模型添加与配置 

Cherry Studio 本身只是客户端，需要添加模型服务等。
点击界面右上角的设置，进入模型管理页面，添加一个新的模型提供商，已默认集成了常见的模型提供商，也可以自行添加。
通常需要填写以下信息：
- 名称
- API Key
- Base URL 或 Endpoint
- 模型名
- 是否启用该配置


#Cherry-Studio