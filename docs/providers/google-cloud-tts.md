# Google Cloud TTS 配置指南

## 概述

Google Cloud Text-to-Speech 是 Google 提供的专业级文本转语音服务，支持多种语言和高质量的语音合成。PyVideoTrans 支持 Google Cloud TTS 作为语音合成渠道。

- **适用场景**：专业级语音合成，多语言支持
- **TTS 渠道编号**：15
- **特点**：语音质量高、语言支持广泛、企业级稳定性

## 准备工作

### 1. 创建 Google Cloud 项目

1. 访问 [Google Cloud Console](https://console.cloud.google.com)
2. 创建新项目或选择现有项目
3. 启用 Cloud Text-to-Speech API
4. 创建服务账号并下载凭据 JSON 文件

### 2. 获取配置信息

- **服务账号凭据**：下载的 JSON 文件路径
- **项目 ID**：Google Cloud 项目 ID
- **API 密钥**：如有需要，可配置 API 密钥

## 在 PyVideoTrans 中的配置

### GUI 配置

1. 打开 PyVideoTrans 设置
2. 选择 "配音/语音合成" → "Google Cloud TTS"（渠道编号：15）
3. 填写以下信息：
   - **凭据 JSON**：Google Cloud 服务账号凭据文件路径
   - **语音角色**：选择 Google Cloud TTS 支持的语音
   - **语言**：目标语言代码

### API 调用示例

```json
POST /tts
{
  "name": "C:/videos/sample.srt",
  "tts_type": 15,
  "voice_role": "en-US-Wavenet-A",
  "target_language_code": "en"
}
```

## 支持的语音角色

Google Cloud TTS 提供丰富的语音选择：

### 中文语音
- `cmn-CN-Wavenet-A` - 中文 WaveNet A（女性）
- `cmn-CN-Wavenet-B` - 中文 WaveNet B（男性）
- `cmn-CN-Wavenet-C` - 中文 WaveNet C（女性）
- `cmn-CN-Wavenet-D` - 中文 WaveNet D（男性）

### 英语语音
- `en-US-Wavenet-A` - 美式英语 WaveNet A（男性）
- `en-US-Wavenet-B` - 美式英语 WaveNet B（男性）
- `en-US-Wavenet-C` - 美式英语 WaveNet C（女性）
- `en-US-Wavenet-D` - 美式英语 WaveNet D（女性）
- `en-US-Wavenet-E` - 美式英语 WaveNet E（女性）
- `en-US-Wavenet-F` - 美式英语 WaveNet F（女性）

### 日语语音
- `ja-JP-Wavenet-A` - 日语 WaveNet A（女性）
- `ja-JP-Wavenet-B` - 日语 WaveNet B（女性）
- `ja-JP-Wavenet-C` - 日语 WaveNet C（男性）
- `ja-JP-Wavenet-D` - 日语 WaveNet D（男性）

### 其他语言支持
- 葡萄牙语、西班牙语、法语、德语、意大利语、韩语、俄语、印地语、阿拉伯语、土耳其语、泰语、越南语、印尼语等

## 高级功能

### 1. 语音参数调节

Google Cloud TTS 支持精细的语音参数调节：

- **语速**：`+0%` 到 `±50%`
- **音调**：`+0Hz` 到 `±20Hz`
- **音量增益**：调节输出音量

### 2. 输出格式

支持多种音频格式：
- `mp3`（默认）
- `wav`
- `flac`
- `aac`
- `ogg_opus`
- `linear16`

### 3. WaveNet 语音

Google Cloud TTS 提供两种语音类型：
- **Standard**：标准语音，成本较低
- **WaveNet**：高质量语音，更自然流畅

## 常见问题与解决方案

### 1. 凭据文件找不到

**问题**：无法找到凭据 JSON 文件
**解决方案**：
- 检查凭据文件路径是否正确
- 确认文件有读取权限
- 重新下载凭据文件

### 2. 语音不可用

**问题**：选择的语音在当前区域不可用
**解决方案**：
- 确认凭据有 Text-to-Speech API 访问权限
- 检查所选语言是否支持
- 查看日志获取详细错误信息

### 3. 语速参数无效

**问题**：语速参数格式错误
**解决方案**：
- 语速应为百分比格式（如 "+10%"、"-5%"）
- 默认值为 "+0%"
- 确保参数在有效范围内

### 4. 音调参数无效

**问题**：音调参数格式错误
**解决方案**：
- 音调应为 Hz 格式（如 "+2Hz"、"-1Hz"）
- 默认值为 "+0Hz"
- 确保参数在有效范围内

## 成本优化建议

### 1. 选择合适的语音类型

- **Standard 语音**：成本较低，适合一般用途
- **WaveNet 语音**：质量更高，适合专业用途

### 2. 批量处理优化

- 合并多个短句为较长的文本
- 减少 API 调用次数
- 利用本地缓存机制

### 3. 监控使用量

1. 定期检查 Google Cloud 控制台使用情况
2. 设置使用量预警
3. 优化合成策略

## 性能优化

### 1. 并发控制

- 合理设置并发请求数
- 避免超过 API 限制
- 实现请求队列管理

### 2. 错误处理

- 实现智能重试机制
- 记录失败请求
- 提供降级方案

### 3. 缓存策略

- 利用 PyVideoTrans 内置缓存
- 相同文本不会重复合成
- 定期清理缓存文件

## 与其他 TTS 服务的比较

| 特性 | Google Cloud TTS | Azure TTS | OpenAI TTS | Edge TTS |
|------|------------------|-----------|------------|----------|
| 语音质量 | 高 | 非常高 | 高 | 高 |
| 费用 | 按使用量 | 按使用量 | 按字符数 | 免费 |
| 语音选择 | 非常丰富 | 非常丰富 | 有限 | 丰富 |
| 语言支持 | 广泛 | 广泛 | 有限 | 广泛 |
| 企业级支持 | 优秀 | 优秀 | 良好 | 一般 |
| 配置复杂度 | 中等 | 中等 | 简单 | 简单 |

## 技术支持

### 官方资源

- [Google Cloud TTS 文档](https://cloud.google.com/text-to-speech)
- [API 参考](https://cloud.google.com/text-to-speech/docs/reference/rest)
- [语音列表](https://cloud.google.com/text-to-speech/docs/voices)

### PyVideoTrans 支持

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)

---

Google Cloud TTS 提供企业级的语音合成服务，适合对语音质量和稳定性要求较高的生产环境。建议根据实际需求选择合适的语音类型和配置。