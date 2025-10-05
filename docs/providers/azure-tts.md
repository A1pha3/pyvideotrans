# Azure TTS 指南（骨架）

概述
- 适用场景：使用 Azure Speech 服务进行文本转语音，供配音流程（tts_type=5）；
- 先决条件：Azure 订阅、创建 Speech 资源并获取 Key 与 Region。

准备
- 获取 Key 与 Region：参见 Azure 官方文档（Speech service keys and location/region）
- 网络与计费：确保账户可用、配额充足。

在 pyvideotrans 中的配置
- GUI 路径：设置 → 配音/语音合成 → Azure TTS
- 必填项：
  - API Key
  - Region（例如 eastus）
  - 语音角色 voice_role（见 docs/api/api.md 或下方映射）
- 可选项：
  - 语速/音量/音调（与 edge-tts 相同参数格式）

示例（调用 API /tts）
- 参照 docs/api/api.md，设置 tts_type=5、voice_role 为 Azure 角色名（如 zh-CN-XiaoxiaoNeural）

常见问题
- 401/403：Key、Region 或签名错误；检查订阅与密钥有效期
- 429：频率限制；降低并发或提升配额
- 语音不可用：确认所选 voice 在对应 Region 可用

参考
- Azure Speech 官方文档：https://learn.microsoft.com/azure/ai-services/speech-service/