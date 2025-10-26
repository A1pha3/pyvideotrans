# PyVideoTrans 文档风格指南

本文档定义了 PyVideoTrans 项目文档的命名规范、格式标准和风格要求。

## 文件命名规范

### 1. 基本规则

- **全部小写**：文件名必须使用小写字母
- **使用连字符**：单词之间使用连字符 `-` 分隔
- **避免特殊字符**：不要使用空格、下划线或其他特殊字符
- **描述性命名**：文件名应准确描述文档内容

### 2. 命名模式

| 文档类型 | 命名模式 | 示例 |
|---------|---------|------|
| 主文档 | `index.md` | `index.md` |
| 指南文档 | `主题-描述.md` | `installation-guide.md` |
| API 文档 | `api/模块名.md` | `api/translation.md` |
| 教程文档 | `tutorials/主题.md` | `tutorials/quickstart.md` |
| 配置文档 | `providers/服务名.md` | `providers/openai.md` |

### 3. 目录结构规范

```
docs/
├── index.md                    # 主索引文档
├── README.md                   # 项目说明
├── about.md                    # 关于项目
├── changelog.md               # 更新日志
├── contributing.md            # 贡献指南
├── documentation-style-guide.md # 本文档
├── api/                       # API 文档
│   ├── index.md
│   ├── translation.md
│   └── tts.md
├── architecture/              # 架构文档
│   ├── index.md
│   └── design-principles.md
├── developer-guide/          # 开发者指南
│   ├── index.md
│   └── debugging.md
├── guides/                    # 用户指南
│   ├── installation.md
│   ├── user-guide.md
│   ├── model-download.md
│   ├── voice-translation.md
│   └── faq.md
├── internals/                # 源码导读
│   ├── index.md
│   └── task-pipeline.md
├── providers/                # 服务商配置
│   ├── openai.md
│   ├── azure-tts.md
│   ├── deepl.md
│   ├── edge-tts.md
│   ├── elevenlabs-tts.md
│   ├── gemini.md
│   └── google-cloud-tts.md
├── tutorials/               # 教程
│   ├── quickstart-video-translation.md
│   └── batch-subtitle-tts.md
└── locales/                # 多语言文档
    └── ...
```

## 内容格式规范

### 1. 标题层级

```markdown
# 一级标题（文档标题）

## 二级标题（主要章节）

### 三级标题（子章节）

#### 四级标题（小节）
```

### 2. 代码块格式

- 使用三个反引号包裹代码
- 指定语言类型
- 包含行号引用（如适用）

```python
# Python 代码示例
def example_function():
    return "Hello World"
```

```json
{
  "key": "value",
  "number": 123
}
```

### 3. 表格格式

使用标准的 Markdown 表格格式：

```markdown
| 列1 | 列2 | 列3 |
|-----|-----|-----|
| 数据1 | 数据2 | 数据3 |
```

### 4. 链接格式

- 使用相对路径链接
- 链接文本应描述目标内容
- 避免使用裸 URL

```markdown
[链接文本](relative/path/to/file.md)
```

## 写作风格

### 1. 语言风格

- **简洁明了**：避免冗长复杂的句子
- **专业准确**：使用准确的术语和描述
- **用户导向**：从用户角度出发编写文档
- **一致性**：保持术语和表达方式的一致性

### 2. 技术术语

- 首次出现的技术术语应简要解释
- 保持术语的一致性
- 使用行业标准术语

### 3. 示例和代码

- 提供完整可运行的示例
- 代码应有适当的注释
- 示例应贴近实际使用场景

## 文档结构

### 1. 标准文档结构

每个文档应包含以下基本结构：

```markdown
# 文档标题

[可选：文档概述]

## 目录（如文档较长）

## 主要内容

### 子章节1

### 子章节2

## 常见问题

## 相关链接

## 更新日志
```

### 2. API 文档结构

API 文档应包含：

```markdown
# API 名称

## 概述

## 接口说明

### 请求参数

### 响应格式

### 错误代码

## 使用示例

## 注意事项
```

## 维护指南

### 1. 更新文档

- 修改代码时同步更新相关文档
- 保持文档与代码的一致性
- 记录重要的变更

### 2. 版本控制

- 使用语义化版本号
- 在更新日志中记录变更
- 保持向后兼容性说明

### 3. 质量检查

- 检查链接有效性
- 验证代码示例
- 确保格式一致性

## 贡献指南

### 1. 提交新文档

1. 遵循命名规范
2. 使用标准文档结构
3. 包含必要的示例
4. 更新相关索引文档

### 2. 修改现有文档

1. 保持向后兼容性
2. 更新相关链接
3. 记录变更内容
4. 通知相关维护者

---

本文档将根据项目发展定期更新。如有疑问或建议，请参考 [贡献指南](contributing.md)。