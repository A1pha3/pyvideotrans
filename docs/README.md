# PyVideoTrans - 视频翻译和配音工具

[English](locales/en/readme.md) | [Español](locales/es/readme.md) | [Português](locales/pt-br/readme.md) | [Italiano](locales/it/readme.md)

PyVideoTrans 是一个开源的视频翻译和配音工具，致力于为用户提供高质量的多语言视频处理解决方案。

## ✨ 核心特性

- **🎯 一键翻译**: 自动将视频从一种语言翻译为另一种语言
- **🎙️ 语音克隆**: 在翻译音频中保留原始说话者的特征
- **🎵 背景音乐保留**: 智能分离人声和背景音乐
- **📝 字幕生成**: 生成多种格式的准确字幕 (SRT, VTT, ASS)
- **🌍 30+ 语言**: 支持超过 30 种语言的识别、翻译和合成
- **🚀 GPU 加速**: CUDA 和 MPS 硬件加速支持
- **📦 批量处理**: 同时处理多个视频文件
- **🎨 友好界面**: 基于 PySide6 构建的直观图形界面

## 🎬 演示视频

[![PyVideoTrans 演示](https://img.youtube.com/vi/your-video-id/0.jpg)](https://www.youtube.com/watch?v=your-video-id)

## 🚀 快速开始

### 方法一：下载预构建包（推荐）

1. **下载**: 访问 [Releases](https://github.com/jianchang512/pyvideotrans/releases) 下载适合您系统的最新版本
2. **解压**: 解压下载的文件
3. **运行**: 执行 `sp.exe` (Windows) 或 `sp` (macOS/Linux)

### 方法二：从源码安装

#### 系统要求

- Python 3.10.x
- FFmpeg
- Git

#### 安装步骤

```bash
# 克隆仓库
git clone https://github.com/jianchang512/pyvideotrans.git
cd pyvideotrans

# 创建虚拟环境
python -m venv venv

# 激活虚拟环境
# Windows
.\venv\Scripts\activate
# macOS/Linux
source ./venv/bin/activate

# 安装依赖
pip install -r requirements.txt

# 运行程序
python sp.py
```

## 📖 详细文档

### 🚀 入门指南
- [安装指南](guides/installation.md) - 详细的安装说明
- [用户指南](guides/user-guide.md) - 完整使用教程
- [常见问题](guides/faq.md) - 常见问题解答

### 🔧 服务配置
- [OpenAI 配置](providers/openai.md) - ChatGPT 翻译和 TTS 配置
- [Azure TTS 配置](providers/azure-tts.md) - Azure 语音服务配置
- [DeepL 配置](providers/deepl.md) - DeepL 翻译服务配置
- [Google Cloud TTS](providers/google-cloud-tts.md) - Google 云端语音合成配置（英文）
- [Gemini 配置](providers/gemini.md) - Gemini 翻译渠道配置

### 💻 开发者资源
- [API 文档](api/api.md) - 完整的 API 参考
- [贡献指南](contributing.md) - 参与项目开发
- [更新日志](changelog.md) - 版本更新记录

## 🌍 支持的语言

PyVideoTrans 支持超过 30 种语言：

**主要语言**: 中文（简体/繁体）、英语、日语、韩语、法语、德语、西班牙语、俄语、阿拉伯语等

**完整列表**: 
- 🇨🇳 中文（简体/繁体）
- 🇺🇸 英语
- 🇯🇵 日语
- 🇰🇷 韩语
- 🇫🇷 法语
- 🇩🇪 德语
- 🇪🇸 西班牙语
- 🇷🇺 俄语
- 🇸🇦 阿拉伯语
- 🇹🇷 土耳其语
- 🇮🇳 印地语
- 🇺🇦 乌克兰语
- 🇰🇿 哈萨克语
- 🇮🇩 印尼语
- 🇲🇾 马来语
- 🇨🇿 捷克语
- 🇵🇱 波兰语
- 🇳🇱 荷兰语
- 🇸🇪 瑞典语
- 更多...

## 📋 系统要求

### 最低要求
- **操作系统**: Windows 10/11, macOS 10.15+, Ubuntu 18.04+
- **内存**: 4GB (推荐 8GB)
- **存储**: 2GB 可用空间
- **网络**: 在线服务需要网络连接

### 推荐配置
- **内存**: 16GB 或更多
- **GPU**: 支持 CUDA 的 NVIDIA 显卡或 Apple Silicon
- **存储**: SSD 硬盘，10GB+ 可用空间

## 🛠️ 故障排除

### 常见问题

#### 安装问题
```bash
# 如果 pip 安装失败，尝试：
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir

# Windows 用户遇到 SSL 错误：
pip install --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host files.pythonhosted.org -r requirements.txt
```

#### FFmpeg 未找到
- **Windows**: 从 [FFmpeg 官网](https://ffmpeg.org/download.html) 下载
- **macOS**: `brew install ffmpeg`
- **Linux**: `sudo apt install ffmpeg` (Ubuntu/Debian)

#### GPU 加速问题
- 确保安装了 NVIDIA CUDA 驱动
- 检查 GPU 与 PyTorch 的兼容性
- 验证 GPU 内存可用性

### 性能优化

#### 提升处理速度
- 使用较小的 Whisper 模型 (tiny, base, small)
- 启用 GPU 加速
- 关闭不必要的应用程序
- 使用 SSD 存储临时文件

#### 提升质量
- 使用较大的 Whisper 模型 (medium, large)
- 选择高质量翻译服务 (DeepL, ChatGPT)
- 使用高质量 TTS 服务 (Azure, OpenAI)

## 🤝 参与贡献

我们欢迎各种形式的贡献！请查看我们的 [贡献指南](contributing.md) 获取详细信息。

### 贡献方式
- 🐛 报告问题和错误
- 💡 提出新功能建议
- 📝 改进文档
- 🌍 添加语言翻译
- 💻 提交代码改进

## 💰 支持项目

如果 PyVideoTrans 对您有帮助，请考虑支持项目发展：

### 💰 资金支持

您的支持将帮助我们：
- 持续改进软件功能
- 维护服务器和基础设施
- 开发新特性和优化
- 建设更好的社区

**支持方式**:
- [Ko-fi 捐赠](https://ko-fi.com/jianchang512)
- 微信赞赏
- 支付宝捐赠

### 🌟 其他支持方式

- **GitHub Star**: 给项目点星支持
- **分享推荐**: 向朋友推荐 PyVideoTrans
- **反馈建议**: 提供使用体验和改进建议
- **参与开发**: 贡献代码和文档

## 📄 许可证

本项目采用 [GPL-3.0 许可证](https://github.com/jianchang512/pyvideotrans/blob/main/LICENSE) 开源发布。

## 🔗 相关链接

- **GitHub**: https://github.com/jianchang512/pyvideotrans
- **官方网站**: https://pyvideotrans.com
- **Discord 社区**: https://discord.gg/y9gUweVCCJ
- **文档中心**: [查看所有文档](index.md)

## 📞 联系我们

- **邮箱**: jianchang512@gmail.com
- **Discord**: https://discord.gg/y9gUweVCCJ
- **Issues**: https://github.com/jianchang512/pyvideotrans/issues

---

**免责声明**: PyVideoTrans 按"现状"提供，仅供教育和研究目的。使用本工具时请尊重版权和知识产权。

感谢您选择 PyVideoTrans！让我们一起打破语言障碍！🌍✨