# DeepL 配置指南

## 概述

DeepL 提供高质量的机器翻译服务，以其准确性和自然度著称。PyVideoTrans 支持 DeepL 作为翻译渠道。

- **适用场景**：高质量通用翻译
- **翻译渠道编号**：4
- **版本区分**：支持 Free 与 Pro 版本，注意不同 Endpoint 与配额限制

## 准备工作

### 1. 注册 DeepL 账户

1. 访问 [DeepL 官网](https://www.deepl.com)
2. 注册免费账户或购买 Pro 版本
3. 在账户设置中获取 API Key

### 2. 获取 API Key

- **免费版**：每月 500,000 字符限制
- **Pro 版**：更高配额，支持更多功能

### 3. 了解语言支持

DeepL 支持以下主要语言：
- 英语、中文、日语、德语、法语、西班牙语、意大利语、荷兰语、波兰语、葡萄牙语、俄语等

## 在 PyVideoTrans 中的配置

### GUI 配置

1. 打开 PyVideoTrans 设置
2. 选择 "翻译" → "DeepL"（渠道编号：4）
3. 填写以下信息：
   - **API Key**：DeepL API 密钥
   - **Endpoint**（可选）：自定义 API 端点，通常使用默认值

### API 调用示例

```json
POST /translate_srt
{
  "name": "C:/videos/lecture.srt",
  "translate_type": 4,
  "target_language": "zh-cn"
}
```

```json
POST /trans_video
{
  "name": "C:/videos/demo.mp4",
  "translate_type": 4,
  "target_language": "en",
  "source_language": "zh-cn"
}
```

## 语言代码映射

DeepL 使用标准的语言代码，与 PyVideoTrans 的映射关系如下：

| 语言名称 | DeepL 代码 | PyVideoTrans 代码 |
|---------|------------|------------------|
| 简体中文 | ZH | zh-cn |
| 英语 | EN | en |
| 日语 | JA | ja |
| 德语 | DE | de |
| 法语 | FR | fr |
| 西班牙语 | ES | es |
| 意大利语 | IT | it |
| 荷兰语 | NL | nl |
| 波兰语 | PL | pl |
| 葡萄牙语 | PT | pt |
| 俄语 | RU | ru |

## 高级功能

### 1. 翻译质量优化

DeepL 提供多种翻译风格选项：
- **正式**：适合正式文档
- **非正式**：适合日常对话
- **技术文档**：适合技术内容

### 2. 术语表支持

Pro 版本支持自定义术语表：
- 上传术语表文件
- 确保专业术语翻译一致性
- 提高特定领域翻译质量

## 常见问题与解决方案

### 1. 频率限制 (429)

**问题**：请求频率超过限制
**解决方案**：
- 降低并发请求数
- 实现指数退避重试机制
- 升级到 Pro 版本获得更高配额

### 2. 配额不足 (456)

**问题**：月度字符配额已用完
**解决方案**：
- 等待下月重置或购买更多配额
- 优化翻译内容，减少不必要翻译
- 使用缓存机制避免重复翻译

### 3. 认证错误 (403)

**问题**：API Key 无效或过期
**解决方案**：
- 检查 API Key 是否正确
- 确认账户状态正常
- 重新生成 API Key

### 4. 翻译质量不稳定

**问题**：翻译结果不一致
**解决方案**：
- 添加重试机制
- 使用术语表功能
- 调整翻译风格参数

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

1. 定期检查 DeepL 账户使用情况
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

## 技术支持

### 官方资源

- [DeepL API 文档](https://developers.deepl.com/)
- [API 参考](https://www.deepl.com/docs-api)
- [语言支持列表](https://www.deepl.com/docs-api/translating-text/)

### PyVideoTrans 支持

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)

---

DeepL 提供业界领先的翻译质量，适合对翻译准确性要求较高的场景。建议根据实际需求选择合适的版本和配额。