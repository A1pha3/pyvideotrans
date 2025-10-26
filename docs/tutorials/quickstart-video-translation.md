# 快速上手：将英文视频翻译成中文视频

1. 准备：安装程序与 FFmpeg，下载 Faster-Whisper `small` 模型到 `models/`
2. 启动：`sp.exe`（Windows）或 `python sp.py`（macOS/Linux）
3. 导入：选择英文视频，源语言 `English`，目标语言 `Chinese (Simplified)`
4. 模型：识别选 Faster-Whisper；翻译选 DeepL/ChatGPT；TTS 选 Edge/Azure 中文音色
5. 输出：勾选保留原声轨（可选），选择硬/软字幕，设置输出目录
6. 开始：点击“开始翻译”，完成后在输出目录查看 `*.mp4/*.srt/*.wav`

故障排除：若不同步，启用语速自适应；若识别不准，换更大模型或做降噪。
