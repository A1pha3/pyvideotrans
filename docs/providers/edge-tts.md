# Edge TTS 配置指南

## 概述

Edge TTS 是基于微软 Edge 浏览器的免费文本转语音服务，提供丰富的语音选择和高质量的语音合成效果。

- **适用场景**：免费、高质量的语音合成
- **TTS 渠道编号**：0
- **特点**：语音丰富、无需复杂云端配置、完全免费

## 准备工作

### 1. 网络要求

- 需要能够访问微软语音服务端点
- 支持代理配置（如有需要）
- 稳定的网络连接

### 2. 系统要求

- Python 3.7+
- 支持的操作系统：Windows、macOS、Linux

## 在 PyVideoTrans 中的配置

### GUI 配置

1. 打开 PyVideoTrans 设置
2. 选择 "配音/语音合成" → "Edge-TTS(免费)"（渠道编号：0）
3. 选择语音角色（voice_role）
4. 可选设置语音参数：
   - **语速**：`+0%` 到 `±50%`
   - **音量**：`+0%` 到 `±50%`
   - **音调**：`+0Hz` 到 `±20Hz`

### API 调用示例

```json
POST /tts
{
  "name": "C:/videos/sample.srt",
  "tts_type": 0,
  "voice_role": "zh-CN-XiaoxiaoNeural",
  "target_language_code": "zh-cn",
  "voice_rate": "+0%",
  "volume": "+0%",
  "pitch": "+0Hz"
}
```

## 支持的语音角色

Edge TTS 提供丰富的语音选择，以下是一些常用角色：

### 中文语音
- `zh-CN-XiaoxiaoNeural` - 晓晓（女性，通用）
- `zh-CN-YunxiNeural` - 云希（男性，通用）
- `zh-CN-YunyangNeural` - 云扬（男性，新闻播报）
- `zh-CN-XiaoyiNeural` - 小艺（女性，聊天）
- `zh-CN-YunyeNeural` - 云野（男性，讲故事）

### 英语语音
- `en-US-AriaNeural` - 艾瑞亚（女性，通用）
- `en-US-GuyNeural` - 盖伊（男性，通用）
- `en-US-JennyNeural` - 珍妮（女性，聊天）
- `en-US-AnaNeural` - 安娜（女性，儿童）

### 日语语音
- `ja-JP-NanamiNeural` - 七海（女性，通用）
- `ja-JP-KeitaNeural` - 圭太（男性，通用）
- `ja-JP-AoiNeural` - 葵（女性，聊天）

### 其他语言
- 德语、法语、西班牙语、意大利语、韩语等

## 高级功能

### 1. 语音参数调节

Edge TTS 支持精细的语音参数调节：

- **语速调节**：`-50%`（慢速）到 `+50%`（快速）
- **音量调节**：`-50%`（轻声）到 `+50%`（大声）
- **音调调节**：`-20Hz`（低沉）到 `+20Hz`（高亢）

### 2. 输出格式

支持多种音频格式：
- `mp3`（默认）
- `wav`
- `flac`
- `aac`

### 3. 自动语速对齐

启用 `voice_autorate` 参数可自动调节语速以贴合字幕时轴。

## 常见问题与解决方案

### 1. 网络连接超时

**问题**：无法连接到微软语音服务
**解决方案**：
- 检查网络连接状态
- 配置代理设置（如有需要）
- 尝试更换网络环境

### 2. 语音角色无效

**问题**：选择的语音角色名称错误
**解决方案**：
- 从语音映射表中复制正确的角色名称
- 注意大小写和地区码格式
- 确认语音在当前区域可用

### 3. 合成速度慢

**问题**：语音合成速度较慢
**解决方案**：
- 检查网络连接质量
- 减少并发请求数
- 使用本地缓存机制

### 4. 音频质量不佳

**问题**：合成的音频质量不理想
**解决方案**：
- 调整语音参数（语速、音量、音调）
- 尝试不同的语音角色
- 检查音频输出格式设置

## 性能优化建议

### 1. 批量处理优化

- 合理设置并发请求数
- 利用本地缓存避免重复合成
- 合并多个短句为较长的文本

### 2. 网络优化

- 使用稳定的网络连接
- 配置合适的代理设置
- 实现请求重试机制

### 3. 资源管理

- 监控内存和CPU使用情况
- 及时清理临时文件
- 优化音频文件存储

## 与其他 TTS 服务的比较

| 特性 | Edge TTS | Azure TTS | OpenAI TTS |
|------|----------|-----------|------------|
| 费用 | 免费 | 按使用量收费 | 按字符数收费 |
| 语音质量 | 高 | 非常高 | 高 |
| 语音选择 | 丰富 | 非常丰富 | 有限 |
| 网络要求 | 需要联网 | 需要联网 | 需要联网 |
| 配置复杂度 | 简单 | 中等 | 简单 |

## 技术支持

### 官方资源

- [edge-tts 项目](https://github.com/rany2/edge-tts)
- [微软语音服务](https://azure.microsoft.com/services/cognitive-services/text-to-speech/)

### PyVideoTrans 支持

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)

---

Edge TTS 是 PyVideoTrans 中性价比最高的语音合成方案，适合大多数免费使用场景。对于有更高要求的用户，可以考虑 Azure TTS 或 OpenAI TTS 等付费服务。