# PyVideoTrans 架构文档规划

## 文档目标

- 建立对核心组件、运行时流程与关键依赖的统一理解
- 帮助开发者在 GUI 与本地 API 两种形态之间建立关联
- 为后续的设计原则、开发者指南与源码导读提供结构化入口

## 章节结构草案

### 1. 系统总览
- 运行模式：GUI、命令行、本地 API
- 关键依赖：PySide6、Faster-Whisper、FFmpeg、UVR5、第三方翻译/语音服务
- 部署拓扑：本地单机、GPU/CPU 协同

### 2. 模块分层
- `videotrans/configure`：全局配置、状态、缓存
- `videotrans/task`：任务调度管线与队列模型
- `videotrans/recognition`、`translator`、`tts`：各渠道与本地模型适配层
- `videotrans/winform`：GUI 界面与事件触发
- `api.py`：Flask 服务与 Waitress 托管

### 3. 数据与任务流
- 处理流程：输入 → 预处理 → 识别 → 翻译 → 合成 → 输出
- 队列状态：`prepare_queue`、`trans_queue`、`dubb_queue` 等
- 中间产物：`TEMP_DIR`、`apidata/<task_id>` 与日志

### 4. 关键交互
- GUI 与任务调度的通信
- API 接口复用 GUI 管线的方式
- 外部服务调用节流与重试策略

### 5. 可扩展性要点
- 新增翻译/识别/tts 渠道的流程
- 模型管理与缓存策略
- 平台兼容性（Windows/macOS/Linux）注意事项

## 交付节奏建议

1. 先完成系统总览与模块分层，配合示意图
2. 再补充任务流时序与关键交互细节
3. 最后整理扩展性章节，结合最佳实践

## 端到端流程示意
- 提交任务：GUI/CLI/API → `videotrans/task/job.py::submit`
- 队列流转：`prepare_queue` → `trans_queue` → `dubb_queue` → `merge`
- 核心阶段：识别(`_speech2text.py`) → 翻译(`_translate_srt.py`) → 配音(`_dubbing.py`) → 合成(`trans_create.py`)
- 产物输出：`apidata/<task_id>/` 下生成 `.srt/.wav/.mp4` 等文件

## 附录：关键代码索引
- 任务调度与生命周期：`videotrans/task/job.py`, `videotrans/task/_base.py`
- 识别实现：`videotrans/task/_speech2text.py`
- 字幕翻译：`videotrans/task/_translate_srt.py`
- 配音与语速：`videotrans/task/_dubbing.py`, `videotrans/task/_rate.py`
- 合成与导出：`videotrans/task/trans_create.py`
- 配置中心：`videotrans/configure/config.py`
- TTS/翻译/识别渠道枚举：`videotrans/tts/__init__.py`, `videotrans/translator/__init__.py`, `videotrans/recognition/__init__.py`

---

延伸阅读：
- [设计原则与技术取舍](design-principles.md)
- [任务流水线深度解析](../internals/task-pipeline.md)
