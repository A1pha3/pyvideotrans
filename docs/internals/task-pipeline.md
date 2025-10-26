# 任务流水线深度解析

本文聚焦 `/trans_video` 端到端任务，从入队到产物落盘的实现细节。

## 入口与任务创建
- GUI/CLI/API 汇聚至 `videotrans/task/job.py` 统一创建任务 ID，准备输入文件与输出目录。
- 关键字段：`recogn_type`、`model_name`、`translate_type`、`tts_type`、`voice_role`、`subtitle_type`。

## 阶段编排
1. 识别（ASR）
   - 实现：`videotrans/task/_speech2text.py`
   - 产物：`*.srt`（源语言），必要时切片与对齐
2. 翻译（MT）
   - 实现：`videotrans/task/_translate_srt.py`
   - 产物：目标语言 `*.srt`，遵循语言映射与术语表（如配置）
3. 配音（TTS）
   - 实现：`videotrans/task/_dubbing.py`、`videotrans/task/_rate.py`
   - 产物：`voice.wav/mp3`，支持语速自适应与音量/音调调整
4. 合成（Mux）
   - 实现：`videotrans/task/trans_create.py`
   - 产物：`output.mp4`（可嵌入硬/软字幕），可附加背景音轨

## 队列与状态
- 队列：`prepare_queue` → `trans_queue` → `dubb_queue` → `merge`
- 状态落盘：`apidata/processinfo/<task_id>.json`，包含阶段名称、时间戳与可读提示

## 常见问题定位
- 识别准确率低：检查模型大小与音频质量，必要时预处理
- 翻译质量差：切换渠道或启用术语表；对长句做分句
- 配音不同步：启用 `voice_autorate`，或回调字幕微调时间轴
- 合成失败：统一转码后再合并，确认 FFmpeg 可用

## 二次开发建议
- 在各阶段入口加断点或日志，打印输入/输出路径
- 以短样本构建最小复现，验证参数组合
- 新增渠道时遵循适配器接口，编写最小 E2E 集成测试
