# PyVideoTrans 文档中心

欢迎来到 PyVideoTrans 官方文档！这里包含了使用 PyVideoTrans 所需的所有信息。

## 📚 文档导航

### 🚀 快速开始
- [项目介绍](README.md) - 了解 PyVideoTrans 的基本信息
- [安装指南](guides/installation.md) - 快速安装和配置
- [用户指南](guides/user-guide.md) - 详细使用说明
- [常见问题](guides/faq.md) - 解决常见问题

### 📖 详细指南
- [Windows 安装](guides/installation-windows.md) - Windows 系统安装指南
- [macOS 安装](guides/installation-macos.md) - macOS 系统安装指南  
- [Linux 安装](guides/installation-linux.md) - Linux 系统安装指南
- [模型下载](guides/model-download.md) - 语音识别模型下载
- [视频翻译实战](guides/voice-translation.md) - 从零到交付的全流程
- [语言包](guides/language-packs.md) - 多语言支持说明

### 🔧 服务配置
- [OpenAI 配置](providers/openai.md) - ChatGPT 翻译和 OpenAI TTS 配置
- [Azure TTS 配置](providers/azure-tts.md) - Azure 语音服务配置
- [DeepL 配置](providers/deepl.md) - DeepL 翻译服务配置
- [Google Cloud TTS](providers/google-cloud-tts.md) - Google 云端语音合成配置（英文）
- [Gemini 配置](providers/gemini.md) - Gemini 翻译渠道配置

### 💻 开发者资源
- [API 文档](api/api.md) - 完整的 API 参考
- [API 文档 (English)](api/api-en.md) - English API Reference
- [架构文档](architecture/index.md) - 模块分层、任务流与关键索引
- [设计原则](architecture/design-principles.md) - 关键设计取舍与扩展点
- [开发者指南](developer-guide/index.md) - 开发环境、运行与提交规范
- [调试与排错](developer-guide/debugging.md) - 日志、常见问题与工具链
- [源码导读](internals/index.md) - 关键模块与典型调用链
- [关于项目](about.md) - 项目详细信息

### 🧪 教程与实战
- [快速上手：英译中视频](tutorials/quickstart-video-translation.md)
- [实战：字幕批量中文配音](tutorials/batch-subtitle-tts.md)

### 🌍 多语言文档
- [English Documentation](locales/en/index.md)
- [Documentación en Español](locales/es/index.md)
- [Documentação em Português](locales/pt-br/index.md)
- [Documentazione Italiana](locales/it/index.md)

## 🎯 根据需求选择文档

### 我是新用户
1. 先阅读 [项目介绍](README.md) 了解基本功能
2. 根据系统选择对应的 [安装指南](guides/installation.md)
3. 跟随 [用户指南](guides/user-guide.md) 开始使用
4. 遇到问题查看 [常见问题](guides/faq.md)

### 我要配置服务
1. 查看 [服务配置](#-服务配置) 部分
2. 根据需要的服务选择对应配置指南
3. 按照步骤完成配置

### 我是开发者
1. 阅读 [API 文档](api/api.md) 了解接口
2. 查看 [贡献指南](contributing.md) 参与开发
3. 了解项目架构和设计理念

### 我需要其他语言
1. 选择对应的 [多语言文档](#-多语言文档)
2. 所有主要功能都有多语言版本

## 📋 文档版本

- **当前版本**: v3.80
- **最后更新**: 2025 年 10 月
- **适用构建**: 桌面版 GUI 与本地 API 9011
- **文档语言**: 中文（简体）

## 🔍 搜索和导航

### 快速查找
- 使用浏览器的搜索功能 (Ctrl+F / Cmd+F)
- 查看各文档的目录结构
- 利用文档间的交叉引用链接

### 文档结构
```
docs/
├── README.md                    # 项目主文档
├── about.md                     # 项目详细信息
├── contributing.md              # 贡献指南
├── index.md                     # 文档索引 (本页面)
├── api/                         # API 文档
│   ├── api.md                   # 中文 API 文档
│   └── api.en.md                # 英文 API 文档
├── guides/                      # 使用指南
│   ├── installation.md          # 安装指南总览
│   ├── installation-windows.md  # Windows 安装
│   ├── installation-macos.md    # macOS 安装
│   ├── installation-linux.md    # Linux 安装
│   ├── user-guide.md            # 用户指南
│   ├── model-download.md        # 模型下载
│   ├── language-packs.md        # 语言包
│   └── faq.md                   # 常见问题
├── providers/                   # 服务提供商配置
│   ├── openai.md                # OpenAI 配置
│   ├── azure-tts.md             # Azure TTS 配置
│   └── deepl.md                 # DeepL 配置
├── internals/                # 源码导读
│   ├── index.md              # 源码导读
│   └── task-pipeline.md      # 任务流水线
└── locales/                     # 多语言文档
    ├── en/index.md              # 英文
    ├── es/index.md              # 西班牙文
    ├── pt-br/index.md           # 葡萄牙文
    └── it/index.md              # 意大利文
```

## 💡 使用建议

### 阅读顺序建议
1. **新手**: README → 安装指南 → 用户指南 → 常见问题
2. **进阶**: 用户指南 → 服务配置 → API 文档
3. **开发者**: API 文档 → 贡献指南 → 项目详情

### 获取帮助
- 📖 首先查看相关文档
- 🔍 搜索 [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- 💬 加入 [Discord 社区](https://discord.gg/y9gUweVCCJ)
- 📧 发送邮件至 jianchang512@gmail.com

## 🔄 文档更新

### 更新频率
- 跟随软件版本同步更新
- 重要功能变更及时更新
- 用户反馈问题及时修正

### 贡献文档
欢迎帮助改进文档：
- 报告文档错误或不清楚的地方
- 提供更好的示例和说明
- 翻译文档到其他语言
- 添加缺失的内容

查看 [贡献指南](contributing.md) 了解如何参与。

## 📞 联系我们

- **项目主页**: https://github.com/jianchang512/pyvideotrans
- **Discord**: https://discord.gg/y9gUweVCCJ
- **邮箱**: jianchang512@gmail.com

---

感谢使用 PyVideoTrans！希望这些文档能帮助您更好地使用我们的产品。