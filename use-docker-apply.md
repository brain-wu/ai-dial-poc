# 在MAC OS中部署DIAL(基于Podman)


## 一、准备运行环境
### 1. 创建VM

podman machine init --cpus 6 --memory 24576 --disk-size 200

# 参数详解：
•	--cpus: 设置虚拟机的 CPU 核心数。
•	--memory: 设置虚拟机的内存大小，单位为 MiB。24 GB 需要转换为 MiB (1 GB = 1024 MiB)，所以 24 GB = 24 * 1024 = 24576 MiB。
•	--disk-size: 设置虚拟机的磁盘大小，单位为 GB。

### 2. 启动VM

podman machine start

## 二、部署 DIAL- 使用Ollama
### 1. 获取 AI DIAL
拉取存储库中的代码，并将目录更改为以下文件夹：


cd ai-dial/dial-docker-compose/ollama
### 2.选择要运行的模型
按照 Ollama Search (https://ollama.com/search)中的特征标签（Embeddings、Code、Tools、Vision）找到合适的模型。
### 3. 启动AI DIAL Chat
#### 3.1 根据您选择的模型类型在当前目录中配置 .env 文件：
•	为文本模型的名称设置 OLLAMA_CHAT_MODEL。
•	为 Vision Model 的名称设置 OLLAMA_VISION_MODEL。
•	为嵌入模型的名称设置 OLLAMA_EMBEDDING_MODEL。
注： 无需配置所有模型。如果未设置模型，则不会下载该模型。

```
vim ai-dial/dial-docker-compose/ollama/.env
DIAL_DIR="./ollama"
CHAT_KEEP_ALIVE_TIMEOUT=600000

OLLAMA_CHAT_MODEL=llama3.1:8b-instruct-q4_0   # CHAT_MODEL
OLLAMA_VISION_MODEL=				# VISION_MODEL
OLLAMA_EMBEDDING_MODEL=			# EMBEDDING_MODEL
```
### 3.2 然后运行以下命令，将指定的模型拉取并加载到 Ollama 服务器的内存中：

podman compose up --abort-on-container-exit –build

 
### 3.3最后，在浏览器中打开 http://localhost:3000/ 以启动 AI DIAL Chat 应用程序并选择合适的 AI DIAL 部署进行对话


# 在Linux中部署

### 部署 DIAL- 使用Ollama
### 1. 获取 AI DIAL
拉取存储库中的代码，并将目录更改为以下文件夹：

cd ai-dial/dial-docker-compose/ollama
### 2.选择要运行的模型
按照 Ollama Search(https://ollama.com/search) 中的特征标签（Embeddings、Code、Tools、Vision）找到合适的模型。

### 3. 启动AI DIAL Chat
#### 3.1 根据您选择的模型类型在当前目录中配置 .env 文件：
•	为文本模型的名称设置 OLLAMA_CHAT_MODEL。
•	为 Vision Model 的名称设置 OLLAMA_VISION_MODEL。
•	为嵌入模型的名称设置 OLLAMA_EMBEDDING_MODEL。
注： 无需配置所有模型。如果未设置模型，则不会下载该模型。

```
vim ai-dial/dial-docker-compose/ollama/.env
DIAL_DIR="./ollama"
CHAT_KEEP_ALIVE_TIMEOUT=600000

OLLAMA_CHAT_MODEL=llama3.1:8b-instruct-q4_0,   # CHAT_MODEL
OLLAMA_VISION_MODEL=				# VISION_MODEL
OLLAMA_EMBEDDING_MODEL=			# EMBEDDING_MODEL
```
### 3.2 然后运行以下命令，将指定的模型拉取并加载到 Ollama 服务器的内存中：

docker compose up --abort-on-container-exit –build

 
### 3.3最后，在浏览器中打开 http://localhost:3000/ 以启动 AI DIAL Chat 应用程序并选择合适的 AI DIAL 部署进行对话