# PyVideoTrans 开发者指南规划

## 文档目标

- 为新贡献者提供快速上手的路径
- 说明开发环境、编码规范与常见调试手段
- 关联源码结构、任务队列和主要脚本

## 结构草案

### 1. 快速上手
- 环境准备：Python 3.10、`uv`/`venv`、FFmpeg、Node（可选）
- 常用脚本：`sp.py`（GUI）、`api.py`（本地 API）、`cli.py`（命令行）
- 运行模式说明：GUI 调试、API 调试、单元测试/集成测试

### 2. 代码结构导航
- `videotrans/` 顶层概览
- 关键子模块与职责矩阵
- 典型调用链：识别 → 翻译 → 配音 → 合成

### 3. 开发流程
- Issue → 功能分支 → PR → Code Review
- 代码风格：命名、Docstring、注释（参考仓库现有约定）
- 提交规范：Commit message、Changelog 更新与版本号同步

### 4. 调试与测试
- 日志位置与级别（`logs/app-log-*.txt`）
- API 调试：Postman/`requests` 示例
- GUI 调试：PySide6 日志、Qt Designer（如需）
- 模型/渠道调试技巧：最小化输入、缓存清理

### 5. 常见问题排查
- 依赖安装失败、FFmpeg 缺失、GPU 驱动问题
- API Key 读写、代理配置、速率限制
- 队列卡住或结果缺失的处理步骤

## 后续计划

- 根据此结构逐章补充细节
- 配合源码片段与流程图提升可读性
- 视社区反馈迭代 FAQ 与最佳实践
