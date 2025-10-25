# 关于 PyVideoTrans

PyVideoTrans 是一个开源的视频翻译和配音工具，致力于为用户提供高质量的多语言视频处理解决方案。

## 项目愿景

我们的目标是打破语言障碍，让优质的视频内容能够触达更广泛的受众。通过先进的AI技术，PyVideoTrans 让视频翻译变得简单、高效、准确。

## 核心特性

- **多模型支持**: 集成多种先进的语音识别模型
- **多服务商翻译**: 支持主流翻译服务，确保翻译质量
- **高质量语音合成**: 提供自然流畅的多语言配音
- **背景音乐保留**: 智能分离人声和背景音，保持原有音效
- **批量处理**: 支持大规模视频批量处理
- **开源免费**: 完全开源，用户可自由使用和修改

## 技术架构

PyVideoTrans 主要由以下部分组成：

- **桌面端 GUI**：基于 PySide6，采用多线程队列分发任务
- **任务调度器**：`videotrans/task` 目录负责队列管理、日志与结果落盘
- **音频与字幕管线**：FFmpeg、UVR5 完成音轨拆分、混合与字幕生成
- **模型与服务集成**：统一的 `recognition`、`translator`、`tts` 模块封装本地模型与外部 API
- **本地 API 服务**：`api.py` 暴露 HTTP 接口，复用 GUI 同步的任务管线
- **配置系统**：`videotrans/configure` 维护全局状态、缓存与渠道凭据

## 支持的语言

PyVideoTrans 支持超过 30 种语言的识别、翻译和语音合成：

### 语音识别
- **本地 Faster-Whisper**：多语种，含中/英/日/韩/法/德/西班牙等
- **FunASR**：`paraformer-zh` 支持中文、粤语；`SenseVoiceSmall` 覆盖中/英/日/韩/粤
- **云端渠道**：Google Speech、Gemini、302.AI、ElevenLabs、Qwen3-ASR 等

### 文本翻译
- 覆盖 Google、DeepL、ChatGPT、Gemini、DeepSeek、OpenRouter 等多通道
- `LANG_CODE` 映射详见 `videotrans/translator/__init__.py`，已对齐 GUI 展示

### 语音合成
- Edge-TTS、Azure、OpenAI、Gemini、ElevenLabs、FishTTS、本地 GPT-SoVITS 等
- 某些渠道仅支持特定语种，调用前请参考 `videotrans/tts/__init__.py`

## 应用场景

### 教育培训
- 在线课程多语言化
- 教学视频翻译
- 学术讲座配音

### 商业营销
- 产品宣传片多语言配音与字幕
- 企业内部培训的快速本地化
- 营销直播/短视频的跨语种分发

### 内容创作
- YouTube/哔哩哔哩 等平台的视频本地化
- 播客、采访、纪录片的多语言扩展
- 教程、课程与知识付费内容的国际化

### 个人使用
- 家庭视频翻译
- 旅行记录配音
- 学习资料制作

## 开发与维护

PyVideoTrans 由核心维护者与社区贡献者共同推进：

- **核心目标**：保持稳定、高质量的视频翻译体验
- **发布节奏**：主分支持续集成 + GitHub Releases 定期归档
- **协作方式**：GitHub Issue / PR、Discord、邮件反馈
- **保障措施**：任务日志、异常追踪与社区回访机制

## 社区支持

### 获取帮助
- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues) - 问题反馈和功能请求
- [Discord 社区](https://discord.gg/y9gUweVCCJ) - 实时交流和讨论
- [官方文档](https://pyvideotrans.com) - 详细使用指南

### 参与贡献
- 代码贡献：提交 Pull Request
- 文档改进：完善使用文档
- 问题反馈：报告 Bug 和建议
- 社区建设：帮助其他用户

## 支持项目

如果 PyVideoTrans 对你有帮助，可以考虑以下方式支持：

### 💰 资金支持
- [GitHub Sponsors](https://github.com/sponsors/jianchang512)
- [Ko-fi 捐赠](https://ko-fi.com/jianchang512)

每一份赞助都会用于：
- 服务器与构建环境维护
- 新特性研发与性能优化
- 文档与社区运营

### 🌟 其他支持
- 给仓库点一颗 Star，提升曝光度
- 向身边的创作者/团队推荐 PyVideoTrans
- 在 Issue 或 Discord 提供建议、提交 PR
- 协助改进文档或翻译

## 许可证

PyVideoTrans 采用 [GPL-3.0 许可证](https://github.com/jianchang512/pyvideotrans/blob/main/LICENSE) 开源发布。

这意味着您可以：
- ✅ 自由使用软件
- ✅ 查看和修改源代码
- ✅ 分发软件副本
- ✅ 分发修改后的版本

但需要遵守：
- 📋 保留原始许可证和版权声明
- 📋 开源您的修改版本
- 📋 说明您所做的更改

## 免责声明

PyVideoTrans 是一个开源工具，仅供学习和研究使用。使用本软件时请遵守：

- 尊重版权和知识产权
- 遵守当地法律法规
- 不用于非法或有害目的
- 理解软件按"现状"提供，无任何担保

## 联系我们

- **项目主页**: https://github.com/jianchang512/pyvideotrans
- **官方网站**: https://pyvideotrans.com
- **邮箱**: jianchang512@gmail.com
- **Discord**: https://discord.gg/y9gUweVCCJ

---

感谢您选择 PyVideoTrans！让我们一起打破语言障碍，让世界更加互联互通。