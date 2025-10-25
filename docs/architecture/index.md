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
