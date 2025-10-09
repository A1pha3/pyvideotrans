# DeepL 配置指南

概述
- 适用场景：作为翻译渠道（translate_type=4），高质量通用翻译
- 区分 Free 与 Pro 版本，注意不同 Endpoint 与配额

准备
- 注册 DeepL 并获取 API Key（Free/Pro）
- 了解目标语言代码映射与限制

在 pyvideotrans 中的配置
- GUI：设置 → 翻译 → DeepL
- 填写 API Key、Endpoint（如必要）

示例（调用 API /translate_srt 或 /trans_video）
- translate_type=4，target_language 按 docs/api/api.md 支持列表填写

常见问题
- 456/429：限流/配额不足
- 403：Key/Endpoint 错误
- 翻译不稳定：添加重试与退避

参考
- DeepL API 文档：https://developers.deepl.com/