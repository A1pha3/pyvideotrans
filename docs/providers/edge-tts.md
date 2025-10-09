# Edge TTS 配置指南

概述
- 适用场景：使用 Microsoft Edge TTS（开源 edge-tts 客户端）进行本地/在线合成（tts_type=0）
- 特点：语音丰富、无需复杂云端配置

准备
- Python 环境可用；网络可访问微软语音服务端点

在 pyvideotrans 中的配置
- GUI：设置 → 配音/语音合成 → Edge TTS
- 选择 voice_role（见 docs/api/api.md 的 edge-tts 语音映射）
- 可设置 voice_rate、volume、pitch

示例（调用 API /tts）
- 参见 docs/api/api.md，设置 tts_type=0 和对应 voice_role

常见问题
- 超时/网络错误：检查网络代理与防火墙
- 角色名无效：从映射表中拷贝合法名称，注意大小写与地区码

参考
- edge-tts 项目：https://github.com/rany2/edge-tts