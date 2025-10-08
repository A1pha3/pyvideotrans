# 安装指南

本文档提供 PyVideoTrans 在不同操作系统上的详细安装指南。

## 系统要求

- **操作系统**: Windows 10/11, macOS 10.14+, Linux (Ubuntu 18.04+, CentOS 7+)
- **Python**: 3.10.x (推荐 3.10.4)
- **内存**: 最低 4GB RAM，推荐 8GB+
- **存储**: 至少 5GB 可用空间
- **GPU**: 可选，支持 NVIDIA GPU 加速 (CUDA 11.8+)

## 快速安装

### Windows 预打包版本

最简单的安装方式，适合普通用户：

1. 访问 [Releases 页面](https://github.com/jianchang512/pyvideotrans/releases)
2. 下载最新版本的预打包文件
3. 解压到**英文路径**且**不含空格**的目录
4. 双击 `sp.exe` 启动程序

> **注意**: 
> - 必须解压后使用，不能直接在压缩包内运行
> - 如遇权限问题，右键以管理员身份运行
> - 杀毒软件可能误报，请添加到白名单

### 源码安装

适合开发者和高级用户，支持所有平台：

- [Windows 源码安装](installation-windows.md)
- [macOS 源码安装](installation-macos.md)
- [Linux 源码安装](installation-linux.md)

## 模型下载

PyVideoTrans 需要下载语音识别模型才能正常工作：

1. 访问 [模型下载页面](https://pyvideotrans.com/model.html)
2. 根据需要下载对应的模型文件
3. 将模型文件放置到 `models` 目录下

详细说明请参考 [模型下载指南](model-download.md)

## GPU 加速配置

如果您有 NVIDIA 显卡，可以启用 GPU 加速来提高处理速度：

### CUDA 环境要求

- NVIDIA 显卡 (GTX 1060 或更高)
- CUDA 11.8 或更高版本
- 对应的 cuDNN 库

### 安装 CUDA 支持

```bash
# 卸载 CPU 版本的 PyTorch
pip uninstall -y torch torchaudio

# 安装 GPU 版本的 PyTorch
pip install torch==2.2.0 torchaudio==2.2.0 --index-url https://download.pytorch.org/whl/cu118

# 安装 CUDA 库 (Linux/Windows)
pip install nvidia-cublas-cu11 nvidia-cudnn-cu11
```

详细的 GPU 配置指南请参考：[CUDA 加速支持](https://pyvideotrans.com/gpu.html)

## 常见问题

### 安装问题

**Q: pip 安装依赖失败怎么办？**

A: 尝试切换到国内镜像源：
```bash
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
pip config set install.trusted-host mirrors.aliyun.com
```

**Q: ctranslate2 版本兼容问题？**

A: 如果 CUDA 版本低于 12.x：
```bash
pip uninstall -y ctranslate2
pip install ctranslate2==3.24.0
```

**Q: 模块找不到错误？**

A: 打开 `requirements.txt`，找到对应模块，删除版本号重新安装：
```bash
# 例如：将 numpy==1.26.4 改为 numpy
pip install numpy
```

### 运行问题

**Q: 程序启动后闪退？**

A: 检查以下几点：
1. 确保 Python 版本为 3.10.x
2. 检查是否缺少必要的依赖
3. 查看日志文件 `logs/app-log-*.txt`

**Q: GPU 加速不生效？**

A: 验证 CUDA 安装：
```bash
# 检查 CUDA 版本
nvcc -V

# 检查 PyTorch GPU 支持
python -c "import torch; print(torch.cuda.is_available())"
```

## 验证安装

安装完成后，可以通过以下方式验证：

1. 启动程序：`python sp.py`
2. 检查版本信息：程序标题栏应显示 "pyVideoTrans v3.80"
3. 测试基本功能：尝试加载一个小的音频文件进行识别

## 获取帮助

如果遇到安装问题，可以通过以下方式获取帮助：

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)
- [官方文档](https://pyvideotrans.com)

## 下一步

安装完成后，建议阅读：

- [用户使用指南](user-guide.md)
- [模型下载指南](model-download.md)
- [API 文档](../api/api.md)