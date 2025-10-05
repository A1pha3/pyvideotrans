# 文档总览

本目录收录 pyvideotrans 的用户指南、API 参考、第三方服务使用说明及多语言文档。本文档已完成结构与命名规范化，后续新增内容请遵循下述约定。

## 目录结构

- api/
  - api.md（中文 API 参考）
  - api.en.md（英文 API 参考）
- guides/
  - language-packs.md（语言包/支持语言说明）
- providers/
  - google-cloud-tts.md（Google Cloud TTS 指南）
- locales/
  - en/readme.md（英文使用说明）
  - es/readme.md（西班牙语使用说明）
  - it/readme.md（意大利语使用说明）
  - pt-br/readme.md（葡萄牙语-BR 使用说明）
  - pt-br/download-models.md、ffmpeg-download.md、language.md（对应子文档）
- about.md（关于/捐助）

## 命名与风格规范

- 统一小写命名：目录与文件名采用小写；多词使用连字符（kebab-case），例如 google-cloud-tts.md。
- Markdown 语法统一：一级标题以 # 开始，段落前后空行；列表使用 - 或 1.；代码块使用 ``` 标记并注明语言（如 ```bash、```python）。
- 链接规范：优先使用相对路径；跨目录使用 ../ 前缀；外链需可访问并附带清晰锚文本。
- 术语一致：参数名、取值与界面术语需与代码实现保持一致（例如 target_language、split_type: all/avg）。
- 禁止含糊/过时描述：如安装命令、版本号、示例输出需真实可用；发现变更应同步更新。

## 快速导航

- API 参考
  - 中文：api/api.md
  - English: api/api.en.md
- 使用指南
  - 语言与语音：guides/language-packs.md
  - 第三方服务（示例）：providers/google-cloud-tts.md
- 多语言文档
  - English：locales/en/readme.md
  - Español：locales/es/readme.md
  - Italiano：locales/it/readme.md
  - Português (Brasil)：locales/pt-br/readme.md
- 关于/捐助：about.md

## 贡献与本地化

- 请阅读 docs/contributing.md 以了解提交流程、规范与检查清单。
- 新增语言时在 locales/<lang>/ 下创建 readme.md，遵循现有语言页结构与链接风格；必要时新增子文档并使用小写命名。