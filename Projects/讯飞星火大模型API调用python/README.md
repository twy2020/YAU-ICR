文档更新于2024-1-10
作者:Teng
# 一、项目说明
代码来自于讯飞星火大模型官方API调用手册，可以在个人项目中调用星火大模型完成一些功能开发。本项目使用Python开发。

# 二、关于星火大模型
- API申请官网：[https://xinghuo.xfyun.cn/sparkapi](https://xinghuo.xfyun.cn/sparkapi)
- 后台查看API接口信息：[https://console.xfyun.cn/services/bm3](https://console.xfyun.cn/services/bm3)
- 截止2024-1-10，目前可免费领取 10w tokens

# 三、使用方法
1. 前往讯飞星火官网申请API以及免费tokens
2. 在后台获取APPID、APISecret和APIKey并填入 `test.py` 的对应变量中
3. 确定你使用的模型版本（项目使用的是v3.0环境）
    - `Spark_url = "ws://spark-api.xf-yun.com/v3.1/chat"`  # v3.0环境的地址
    - `# Spark_url = "ws://spark-api.xf-yun.com/v1.1/chat"`  # v1.5环境的地址
    - `# Spark_url = "ws://spark-api.xf-yun.com/v2.1/chat"`  # v2.0环境的地址
4. 在用户发送对话中设定你的prompt（即预置提问模板和情景设置，以获取符合要求的回答）
5. 处理返回的消息并用于进一步的使用

# 四、有什么作用
- GPT评价：
在开发项目中接入星火大模型可以实现以下用途：

1. 自然语言处理（NLP）： 利用星火大模型的先进自然语言处理技术，实现对用户输入文本的深度理解，包括情感分析、关键词提取等功能。

2. 智能对话系统： 构建智能对话系统，通过设置合适的prompt，使得模型能够生成富有语境和上下文逻辑的回答，提高用户体验。

3. 信息检索与推荐： 利用大模型对海量文本数据进行分析，实现高效的信息检索和个性化推荐，为用户提供更有针对性的信息服务。

4. 语义匹配与问题解答： 利用模型的语义匹配能力，实现更准确的问题解答系统，能够处理用户提出的各种查询和问题。

5. 文本生成与创意应用： 借助星火大模型的生成能力，开发文本生成应用，如创作文学作品、生成新闻稿等，为创意领域提供支持。

6. 实时聊天与客服： 将大模型应用于实时聊天和客服系统，使得对话更加智能化，提高服务效率和质量。

- 通过以上应用，星火大模型为开发者提供了丰富的自然语言处理工具，可用于构建更智能、更灵活的文本相关应用，从而增强项目的交互性和用户体验。
