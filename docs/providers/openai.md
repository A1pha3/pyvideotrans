# OpenAI 服务配置指南

本指南详细说明如何配置和使用 OpenAI 的各种服务，包括 ChatGPT 翻译和 OpenAI TTS 语音合成。

## 概述

OpenAI 提供了多种 AI 服务，PyVideoTrans 支持以下功能：

- **ChatGPT 翻译**: 使用 GPT 模型进行高质量文本翻译
- **OpenAI TTS**: 高质量的文本转语音服务
- **Whisper API**: 云端语音识别服务（可选）

## 获取 API Key

### 1. 注册 OpenAI 账户

1. 访问 [OpenAI 官网](https://openai.com)
2. 点击 "Sign up" 注册账户
3. 验证邮箱并完成注册流程

### 2. 获取 API Key

1. 登录后访问 [API Keys 页面](https://platform.openai.com/api-keys)
2. 点击 "Create new secret key"
3. 为密钥命名（如 "PyVideoTrans"）
4. 复制生成的 API Key（以 `sk-` 开头）
5. **重要**: 妥善保存 API Key，页面关闭后无法再次查看

### 3. 充值账户

1. 访问 [Billing 页面](https://platform.openai.com/account/billing)
2. 点击 "Add payment method" 添加支付方式
3. 充值账户余额（建议至少 $5）

## 配置 ChatGPT 翻译

### 基本配置

1. 在 PyVideoTrans 中选择翻译服务为 "ChatGPT"
2. 在设置中输入您的 OpenAI API Key
3. 选择合适的模型和参数

### 支持的模型

| 模型 | 描述 | 价格 (每1K tokens) | 推荐用途 |
|------|------|-------------------|----------|
| gpt-3.5-turbo | 快速、经济 | $0.0015 | 日常翻译 |
| gpt-4 | 高质量 | $0.03 | 专业翻译 |
| gpt-4-turbo | 平衡性能和成本 | $0.01 | 推荐选择 |

### 高级设置

```json
{
  "model": "gpt-4-turbo",
  "temperature": 0.3,
  "max_tokens": 2000,
  "top_p": 1.0,
  "frequency_penalty": 0.0,
  "presence_penalty": 0.0
}
```

**参数说明**:
- `temperature`: 创造性程度 (0-2)，翻译建议使用 0.1-0.3
- `max_tokens`: 最大输出长度
- `top_p`: 核心采样参数，建议保持 1.0
- `frequency_penalty`: 频率惩罚，减少重复
- `presence_penalty`: 存在惩罚，鼓励新话题

### 提示词优化

PyVideoTrans 使用优化的提示词来确保翻译质量：

```
你是一个专业的视频翻译专家。请将以下字幕文本从{source_language}翻译成{target_language}。

要求：
1. 保持原意准确性
2. 符合目标语言的表达习惯
3. 保持适当的语调和情感
4. 考虑视频内容的上下文
5. 保持字幕的时间同步性

原文：
{text}

请直接输出翻译结果，不要包含其他解释。
```

## 配置 OpenAI TTS

### 基本配置

1. 在语音合成设置中选择 "OpenAI TTS"
2. 输入 OpenAI API Key
3. 选择语音模型和声音

### 支持的模型

| 模型 | 质量 | 速度 | 价格 (每1M字符) |
|------|------|------|----------------|
| tts-1 | 标准 | 快 | $15.00 |
| tts-1-hd | 高清 | 慢 | $30.00 |

### 可用声音

| 声音 | 描述 | 适用语言 |
|------|------|----------|
| alloy | 中性，平衡 | 多语言 |
| echo | 男性，深沉 | 多语言 |
| fable | 英式，精致 | 英语为主 |
| onyx | 男性，深沉 | 多语言 |
| nova | 女性，年轻 | 多语言 |
| shimmer | 女性，温暖 | 多语言 |

### 音频格式设置

```json
{
  "model": "tts-1-hd",
  "voice": "nova",
  "response_format": "mp3",
  "speed": 1.0
}
```

**参数说明**:
- `response_format`: 输出格式 (mp3, opus, aac, flac)
- `speed`: 语速 (0.25-4.0)，1.0 为正常速度

## 使用 Whisper API

### 配置方法

1. 在语音识别设置中选择 "OpenAI Whisper API"
2. 输入 API Key
3. 选择模型和参数

### 支持的模型

| 模型 | 价格 (每分钟) | 特点 |
|------|---------------|------|
| whisper-1 | $0.006 | 高精度，支持多语言 |

### 配置参数

```json
{
  "model": "whisper-1",
  "language": "auto",
  "temperature": 0,
  "response_format": "srt"
}
```

## 成本优化建议

### 1. 选择合适的模型

- **翻译**: 对于一般内容使用 `gpt-3.5-turbo`，专业内容使用 `gpt-4-turbo`
- **TTS**: 日常使用 `tts-1`，高质量需求使用 `tts-1-hd`
- **语音识别**: `whisper-1` 是唯一选择，但精度很高

### 2. 批量处理

- 将多个短句合并为较长的文本进行翻译
- 减少 API 调用次数
- 利用上下文提高翻译质量

### 3. 缓存机制

PyVideoTrans 内置缓存机制：
- 相同文本不会重复翻译
- 缓存文件保存在本地
- 可手动清理缓存

### 4. 成本监控

1. 定期检查 [Usage 页面](https://platform.openai.com/account/usage)
2. 设置使用限额和预警
3. 监控每日/每月消费

## 错误处理

### 常见错误及解决方案

#### 1. API Key 无效
```
Error: Incorrect API key provided
```
**解决方案**: 检查 API Key 是否正确，确保以 `sk-` 开头

#### 2. 余额不足
```
Error: You exceeded your current quota
```
**解决方案**: 充值账户或检查计费信息

#### 3. 速率限制
```
Error: Rate limit reached
```
**解决方案**: 
- 降低并发请求数
- 增加请求间隔
- 升级到更高的使用层级

#### 4. 内容过滤
```
Error: Content filtered
```
**解决方案**: 检查内容是否违反 OpenAI 使用政策

### 网络问题

如果遇到网络连接问题：

1. **使用代理**:
   ```python
   # 在设置中配置代理
   proxy_settings = {
       "http": "http://proxy.example.com:8080",
       "https": "https://proxy.example.com:8080"
   }
   ```

2. **更换 API 端点**:
   - 默认: `https://api.openai.com`
   - 备用: 使用第三方代理服务

3. **检查防火墙设置**:
   - 确保允许访问 OpenAI API
   - 检查企业网络限制

## 最佳实践

### 1. 翻译质量优化

- **上下文提供**: 在提示词中包含视频主题信息
- **术语一致性**: 对专业术语建立词汇表
- **人工校对**: 对重要内容进行人工审核

### 2. 语音合成优化

- **语速调整**: 根据内容类型调整语速
- **声音选择**: 根据原始说话者特征选择合适声音
- **分段处理**: 长文本分段处理，避免单次请求过长

### 3. 安全性

- **API Key 保护**: 不要在代码中硬编码 API Key
- **访问控制**: 限制 API Key 的使用权限
- **定期轮换**: 定期更换 API Key

### 4. 性能优化

- **并发控制**: 合理设置并发请求数
- **重试机制**: 实现指数退避重试
- **缓存利用**: 充分利用本地缓存

## 故障排除

### 诊断工具

1. **API 测试**:
   ```bash
   curl https://api.openai.com/v1/models \
     -H "Authorization: Bearer $OPENAI_API_KEY"
   ```

2. **网络连通性**:
   ```bash
   ping api.openai.com
   nslookup api.openai.com
   ```

3. **日志检查**:
   - 查看 PyVideoTrans 日志文件
   - 检查错误信息和状态码

### 性能监控

- 监控 API 响应时间
- 跟踪成功率和错误率
- 记录使用量和成本

## 技术支持

### 官方资源

- [OpenAI 文档](https://platform.openai.com/docs)
- [API 参考](https://platform.openai.com/docs/api-reference)
- [社区论坛](https://community.openai.com)

### PyVideoTrans 支持

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)

---

通过正确配置 OpenAI 服务，您可以获得高质量的翻译和语音合成效果。记住要合理控制成本，并遵循最佳实践以获得最佳体验。