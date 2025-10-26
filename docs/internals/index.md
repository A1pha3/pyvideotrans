# PyVideoTrans 源码导读规划

## 文档定位

- 作为深入源码的入口，承接架构文档与开发者指南
- 对关键模块提供进一步的类/函数级说明
- 收录常用的调用路径与调试断点建议

## 拟包含内容

1. **任务调度内核**
   - `videotrans/task` 目录的核心流程
   - 队列处理、状态标记、异常管理
   - `_listen_queue` 与 `start_thread` 的协同

2. **识别/翻译/配音适配层**
   - `recognition` / `translator` / `tts` 入口函数
   - `is_allow_lang`、`is_input_api` 规则
   - 新增渠道的抽象约束

3. **GUI 事件到任务的映射**
   - `videotrans/winform` 关键窗体与信号
   - 参数收集、校验与任务入队

4. **本地 API 复用逻辑**
   - `api.py` 如何复用桌面端任务队列
   - 资源落盘、日志记录与 Waitress 发布

5. **配置与缓存**
   - `videotrans/configure/config.py` 状态字段
   - 模型缓存、临时目录、语言/渠道枚举

## 后续步骤

- 补充模块截图与类图
- 引入代码片段并标注行号
- 结合典型场景（如 `/trans_video`）做端到端说明

## 关键模块与入口速览
- 任务创建与调度：`videotrans/task/job.py`、`videotrans/task/_base.py`
- 一体化创建流程：`videotrans/task/trans_create.py`
- 识别与字幕生成：`videotrans/task/_speech2text.py`
- 字幕翻译：`videotrans/task/_translate_srt.py`
- 配音与语速对齐：`videotrans/task/_dubbing.py`、`videotrans/task/_rate.py`
- 配置中心：`videotrans/configure/config.py`
- GUI 映射：`videotrans/winform/*`

## 典型调用链（/trans_video）
1. 接收请求（GUI/API/CLI）并落盘输入
2. 拆分阶段：识别 → 翻译 → 配音 → 媒体合成
3. 产物写入 `apidata/<task_id>/`，并更新 `processinfo` 日志

## 调试建议
- 先在 GUI 复现，再定位到对应任务阶段脚本
- 打开更高日志级别，观察各阶段的输入输出与耗时
- 对长视频先裁一小段验证参数与口型对齐

## 延伸阅读
- [任务流水线深度解析](task-pipeline.md)
- [架构设计原则](../architecture/design-principles.md)
- [开发者调试手册](../developer-guide/debugging.md)
