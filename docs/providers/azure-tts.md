# Azure TTS 配置指南

## 概述

Azure TTS 是微软 Azure 认知服务提供的专业级文本转语音服务，支持多种语言和高质量的语音合成。

- **适用场景**：使用 Azure Speech 服务进行文本转语音
- **TTS 渠道编号**：5
- **先决条件**：Azure 订阅、创建 Speech 资源并获取 Key 与 Region

## 准备工作

### 1. 创建 Azure Speech 资源

1. 登录 [Azure 门户](https://portal.azure.com)
2. 搜索并创建 "Speech" 服务
3. 选择合适的定价层（F0 免费层有使用限制）
4. 创建完成后获取 API Key 和 Region

### 2. 获取配置信息

- **API Key**：在资源概览页面的 "Keys and Endpoint" 中获取
- **Region**：如 `eastus`、`westus`、`southeastasia` 等

## 在 PyVideoTrans 中的配置

### GUI 配置

1. 打开 PyVideoTrans 设置
2. 选择 "配音/语音合成" → "Azure-TTS"（渠道编号：5）
3. 填写以下必填项：
   - **API Key**：Azure Speech 服务的密钥
   - **Region**：Azure 资源所在区域
   - **语音角色**：选择 Azure 支持的语音角色

### API 调用示例

```json
POST /tts
{
  "name": "C:/videos/sample.srt",
  "tts_type": 5,
  "voice_role": "zh-CN-XiaoxiaoNeural",
  "target_language_code": "zh-cn"
}
```

## 支持的语音角色

Azure TTS 提供丰富的语音角色选择，以下是一些常用角色：

### 中文语音
- `zh-CN-XiaoxiaoNeural` - 晓晓（女性，通用）
- `zh-CN-YunxiNeural` - 云希（男性，通用）
- `zh-CN-YunyangNeural` - 云扬（男性，新闻播报）
- `zh-CN-XiaoyiNeural` - 小艺（女性，聊天）

### 英语语音
- `en-US-AriaNeural` - 艾瑞亚（女性，通用）
- `en-US-GuyNeural` - 盖伊（男性，通用）
- `en-US-JennyNeural` - 珍妮（女性，聊天）

### 日语语音
- `ja-JP-NanamiNeural` - 七海（女性，通用）
- `ja-JP-KeitaNeural` - 圭太（男性，通用）

## 高级配置

### 语音参数

Azure TTS 支持以下高级参数：

- **语速**：`+0%` 到 `±50%`
- **音量**：`+0%` 到 `±50%`
- **音调**：`+0Hz` 到 `±20Hz`

### 输出格式

支持多种音频格式：
- `mp3`（默认）
- `wav`
- `flac`
- `aac`

## 常见问题与解决方案

### 1. 认证错误 (401/403)

**问题**：API Key 或 Region 错误
**解决方案**：
- 检查 API Key 是否正确
- 确认 Region 与资源创建时选择的区域一致
- 检查订阅状态是否有效

### 2. 频率限制 (429)

**问题**：请求频率超过限制
**解决方案**：
- 降低并发请求数
- 升级到更高的定价层
- 实现请求间隔控制

### 3. 语音不可用

**问题**：所选语音在指定区域不可用
**解决方案**：
- 确认语音角色名称拼写正确
- 检查语音是否在当前区域支持
- 尝试使用其他语音角色

### 4. 网络连接问题

**问题**：无法连接到 Azure 服务
**解决方案**：
- 检查网络连接
- 确认防火墙设置
- 尝试使用代理

## 成本优化建议

### 1. 选择合适的定价层

- **F0 免费层**：适合测试和小规模使用
- **标准层**：适合生产环境，提供更高配额

### 2. 批量处理

- 合并多个短句为较长的文本
- 减少 API 调用次数
- 利用本地缓存机制

### 3. 监控使用量

1. 在 Azure 门户监控使用量
2. 设置使用量预警
3. 定期检查账单

## 性能优化

### 1. 并发控制

- 合理设置并发请求数
- 避免超过服务限制
- 实现指数退避重试机制

### 2. 缓存策略

- 利用 PyVideoTrans 内置缓存
- 相同文本不会重复合成
- 可手动清理缓存文件

## 技术支持

### 官方资源

- [Azure Speech 服务文档](https://learn.microsoft.com/azure/ai-services/speech-service/)
- [语音角色列表](https://learn.microsoft.com/azure/ai-services/speech-service/language-support?tabs=tts)
- [API 参考](https://learn.microsoft.com/azure/ai-services/speech-service/rest-text-to-speech)

### PyVideoTrans 支持

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)

---

通过正确配置 Azure TTS 服务，您可以获得专业级的语音合成效果。建议在生产环境中使用标准层以获得更好的性能和稳定性。