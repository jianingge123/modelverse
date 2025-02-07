# 场景实践

在 ModelVerse 大模型服务平台，DeepSeek 推理服务提供强大的模型推理能力，广泛适用于各种应用场景，如文本分析、数据挖掘等。以下将为您提供详细的操作指南和 API 调用示例，帮助您快速集成 DeepSeek 推理服务。

## 调用 DeepSeek 推理服务

### 操作指南

访问「Modelverse 模型服务平台」—— 访问「模型广场」—— 选择需要的「DeepSeek」模型 —— 点击「API 文档」—— 申请获取 API Key。

### 三步快速接入

1. **获取 API Key**
   - 登录到您的 DeepSeek 账户。
   - 导航到 API 管理页面。
   - 创建一个新的 API Key 并记录下该 Key，您将在后续步骤中使用它。

2. **安装必要的库**
   - 确保您已经安装了必要的库，例如 `requests` 库，用于发送 HTTP 请求。如果尚未安装，可以使用以下命令安装：
     ```bash
     pip install requests
     ```

3. **发送推理请求**
   - 以下是一个使用 Python 发送推理请求的示例代码：
     ```python
     import requests

     # 1. 获取 API 密钥
     DEEPSEEK_API_KEY = "sk-xxxxxxxxxxxxxxxx"  # 替换成你的密钥

     # 2. 创建请求
     headers = {
         "Authorization": f"Bearer {DEEPSEEK_API_KEY}",
         "Content-Type": "application/json"
     }

     data = {
         "model": "deepseek-chat",
         "messages": [
             {"role": "user", "content": "你好！"}
         ],
         "temperature": 0.7
     }

     # 3. 发送请求
     response = requests.post(
         "https://api.deepseek.com/v1/chat/completions",
         headers=headers,
         json=data
     )

     print(response.json()["choices"][0]["message"]["content"])
     ```

### 核心参数说明

```json
{
  "model": "deepseek-chat",  # 可用模型：deepseek-chat / deepseek-coder
  "messages": [              # 对话历史
    {"role": "system", "content": "你是有帮助的 AI 助手"},
    {"role": "user", "content": "请解释量子计算"}
  ],
  "temperature": 0.7,        # 创造性 (0-2)
  "max_tokens": 1024,        # 最大输出长度
  "top_p": 0.9,              # 采样阈值
  "stream": true             # 启用流式输出
}
