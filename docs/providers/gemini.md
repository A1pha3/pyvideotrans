# Gemini 指南（骨架）

概述
- 适用场景：作为翻译渠道（translate_type 可映射至 Gemini，详见 docs/api/api.md）
- 特点：大语言模型翻译，需合理控制成本与速率

准备
- 开通 Google AI Studio / Google Cloud，对应 API Key 或服务账号
- 熟悉配额/地域限制

在 pyvideotrans 中的配置
- GUI：设置 → 翻译 → Gemini
- 配置 API Key/Endpoint（如需）
- 可选：模型名称、温度、最大长度等

示例（调用 API /translate_srt 或 /trans_video）
- translate_type 设为 Gemini 对应数值，填写 target_language

常见问题
- 401：鉴权失败；确认 Key 与权限
- 429：限流；降低并发或增加配额
- 翻译质量：调整系统提示或参数

参考
- Google AI Studio：https://aistudio.google.com/