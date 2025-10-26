# 调试与排错手册

## 日志与产物
- 应用日志：`logs/app-log-*.txt`
- 任务日志：`apidata/processinfo/<task_id>.json`
- 中间产物：`apidata/<task_id>/` 下的 `*.srt/*.wav/*.mp4`

## 常用技巧
- 先 GUI 复现，再定位阶段脚本；必要时直接调用本地 API
- 使用小模型/短样本快速迭代；确认参数后再跑全量
- 打开更细日志级别，打印渠道请求与返回摘要（勿包含敏感信息）

## 典型问题清单
- FFmpeg 不可用：检查可执行路径与版本
- CUDA/MPS 未启用：确认驱动与依赖，或切换 CPU 跑通
- 第三方 API 失败：检查 API Key/Region/速率限制，增加重试与超时

## 工具链
- Postman/curl 测试 `/trans_video`、`/task_status`
- VSCode/Breakpoints 在 `videotrans/task/*` 设置断点
- 音视频校验：`ffprobe`、`mediainfo`、`audacity`
