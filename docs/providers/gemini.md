# Gemini 配置指南

## 概述

Gemini 是 Google 推出的大语言模型，提供高质量的翻译服务。PyVideoTrans 支持 Gemini 作为翻译渠道。

- **适用场景**：大语言模型翻译，高质量通用翻译
- **翻译渠道编号**：12
- **特点**：基于 Google 最新 AI 技术，翻译质量高

## 准备工作

### 1. 获取 API Key

1. 访问 [Google AI Studio](https://aistudio.google.com/)
2. 注册并创建项目
3. 获取 API Key
4. 或者使用 [Google Cloud Console](https://console.cloud.google.com/) 创建服务账号

### 2. 了解配额限制

- 免费配额：每月有一定免费使用量
- 付费配额：按使用量计费
- 速率限制：注意并发请求限制

## 在 PyVideoTrans 中的配置

### GUI 配置

1. 打开 PyVideoTrans 设置
2. 选择 "翻译" → "Gemini AI"（渠道编号：12）
3. 填写以下信息：
   - **API Key**：Gemini API 密钥
   - **模型名称**（可选）：如 `gemini-pro`
   - **温度**（可选）：控制创造性，0.1-1.0
   - **最大长度**（可选）：输出文本最大长度

### API 调用示例

```json
POST /translate_srt
{
  "name": "C:/videos/lecture.srt",
  "translate_type": 12,
  "target_language": "en"
}
```

```json
POST /trans_video
{
  "name": "C:/videos/demo.mp4",
  "translate_type": 12,
  "target_language": "zh-cn",
  "source_language": "en"
}
```

## 支持的模型

Gemini 提供多种模型选择：

| 模型 | 描述 | 适用场景 |
|------|------|----------|
| `gemini-pro` | 通用模型 | 日常翻译、对话 |
| `gemini-pro-vision` | 支持多模态 | 图像+文本翻译 |

## 高级配置

### 1. 翻译参数优化

```json
{
  "temperature": 0.3,
  "max_output_tokens": 2048,
  "top_p": 0.95,
  "top_k": 40
}
```

**参数说明**：
- `temperature`：创造性程度，0.1-1.0，翻译建议 0.1-0.3
- `max_output_tokens`：最大输出长度
- `top_p`：核心采样参数
- `top_k`：Top-K 采样参数

### 2. 提示词优化

PyVideoTrans 使用优化的提示词：

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

## 常见问题与解决方案

### 1. 认证错误 (401)

**问题**：API Key 无效或权限不足
**解决方案**：
- 检查 API Key 是否正确
- 确认 API Key 有足够权限
- 检查项目配额状态

### 2. 频率限制 (429)

**问题**：请求频率超过限制
**解决方案**：
- 降低并发请求数
- 实现指数退避重试机制
- 升级到更高的配额层级

### 3. 翻译质量不稳定

**问题**：翻译结果不一致
**解决方案**：
- 调整温度参数（建议 0.1-0.3）
- 优化提示词
- 添加重试机制

### 4. 网络连接问题

**问题**：无法连接到 Gemini API
**解决方案**：
- 检查网络连接
- 确认防火墙设置
- 尝试使用代理

## 成本优化建议

### 1. 合理使用免费配额

- 优先用于重要内容翻译
- 避免翻译重复内容
- 利用本地缓存机制

### 2. 批量处理优化

- 合并多个短句为较长的文本
- 减少 API 调用次数
- 利用上下文提高翻译质量

### 3. 监控使用量

1. 定期检查 Google Cloud 控制台使用情况
2. 设置使用量预警
3. 优化翻译策略

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
- 相同文本不会重复翻译
- 定期清理缓存文件

## 与其他翻译服务的比较

| 特性 | Gemini | DeepL | ChatGPT |
|------|--------|-------|---------|
| 翻译质量 | 非常高 | 非常高 | 高 |
| 费用 | 按使用量 | 按字符数 | 按 token |
| 语言支持 | 广泛 | 有限但精 | 广泛 |
| 响应速度 | 快 | 非常快 | 中等 |
| 配置复杂度 | 中等 | 简单 | 简单 |

## 技术支持

### 官方资源

- [Google AI Studio](https://aistudio.google.com/)
- [Gemini API 文档](https://ai.google.dev/)
- [Google Cloud Console](https://console.cloud.google.com/)

### PyVideoTrans 支持

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)

---

Gemini 提供基于 Google 最新 AI 技术的翻译服务，适合对翻译质量要求较高的场景。建议根据实际需求合理配置参数和使用配额。