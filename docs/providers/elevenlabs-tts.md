# ElevenLabs TTS 指南（骨架）

概述
- 适用场景：使用 ElevenLabs 提供的高质量语音（tts_type=9）

准备
- 注册 ElevenLabs，获取 API Key
- 了解计费与模型/语音库

在 pyvideotrans 中的配置
- GUI：设置 → 配音/语音合成 → ElevenLabs
- 配置 API Key、选择 Voice ID/Name（如支持）

示例（调用 API /tts）
- 参见 docs/api/api.md，设置 tts_type=9，voice_role 对应 ElevenLabs 的语音名称/ID

常见问题
- 授权失败：检查 API Key
- 额度不足：检查账户计费/配额
- 语音选择失败：确认 Voice ID 是否存在并可用

参考
- ElevenLabs API 文档：https://api.elevenlabs.io/docs