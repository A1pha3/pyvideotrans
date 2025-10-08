# 模型下载指南

PyVideoTrans 需要下载语音识别模型才能正常工作。本指南详细说明如何下载和配置各种模型。

## 模型概述

### 模型类型

1. **Faster Whisper 模型** - 推荐使用，速度快，质量好
2. **OpenAI Whisper 模型** - 原版模型，质量高
3. **UVR5 模型** - 用于音频分离，保留背景音乐
4. **CUDA 库** - 用于 GPU 加速

### 模型大小对比

| 模型 | Faster Whisper | OpenAI Whisper | 速度 | 精度 | 推荐用途 |
|------|----------------|----------------|------|------|----------|
| tiny | 64MB | 66MB | 最快 | 一般 | 快速预览 |
| base | 124MB | 142MB | 快 | 良好 | 日常使用 |
| small | 415MB | 500MB | 中等 | 很好 | **推荐** |
| medium | 1.27GB | 1.5GB | 慢 | 优秀 | 高质量 |
| large-v3 | 2.9GB | 3GB | 最慢 | 最佳 | 专业用途 |

## 快速下载

### 一键下载所有模型

访问 [模型下载页面](https://github.com/jianchang512/stt/releases/tag/0.0) 下载完整的模型包。

### 推荐配置

对于大多数用户，推荐下载：
- **small** 模型（平衡速度和质量）
- **UVR5** 模型（背景音乐分离）
- **CUDA 库**（如果有 NVIDIA 显卡）

## Faster Whisper 模型

### 下载地址

| 模型名称 | 大小 | GitHub 下载 | 备用下载 |
|----------|------|-------------|----------|
| tiny | 64MB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/faster-tiny.7z) | - |
| tiny.en | 64MB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/faster-tiny.en.7z) | - |
| base | 124MB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/faster-base.7z) | - |
| base.en | 124MB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/faster-base.en.7z) | - |
| small | 415MB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/faster-small.7z) | [百度网盘](https://pan.baidu.com/s/1ROjy-UOjz_2a7I_cyzUj2g?pwd=frth) |
| small.en | 415MB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/faster-small.en.7z) | - |
| medium | 1.27GB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/faster-medium.7z) | - |
| medium.en | 1.27GB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/faster-medium.en.7z) | - |
| large-v1 | 2.9GB | [下载](https://huggingface.co/spaces/mortimerme/s4/resolve/main/faster-large-v1.7z?download=true) | [百度网盘](https://pan.baidu.com/s/1IS5y0Pyo1okPQOW2uNaLbw?pwd=428z) |
| large-v2 | 2.9GB | [下载](https://huggingface.co/spaces/mortimerme/s4/blob/main/largev2-jieyao-dao-models.7z) | [百度网盘](https://pan.baidu.com/s/1pQiexsXSCtdN5yBeFAtwLw?pwd=yjmg) |
| large-v3 | 2.9GB | [下载](https://huggingface.co/spaces/mortimerme/s4/resolve/main/largeV3Model-extract-models-folder-%E8%A7%A3%E5%8E%8B%E5%88%B0models%E7%9B%AE%E5%BD%95%E4%B8%8B.7z?download=true) | [百度网盘](https://pan.baidu.com/s/11a5NYCdRSW6VBOlGmeZdhg?pwd=he2w) |

### Distilled 模型（优化版）

| 模型名称 | 大小 | 下载链接 | 特点 |
|----------|------|----------|------|
| distil-whisper-small.en | 282MB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/distil-whisper-small.en.7z) | 英语优化 |
| distil-whisper-medium.en | 671MB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/distil-whisper-medium.en.7z) | 英语优化 |
| distil-whisper-large-v2 | 1.27GB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/distil-whisper-large-v2.7z) | 速度优化 |
| distil-whisper-large-v3 | 1.3GB | [下载](https://github.com/jianchang512/stt/releases/download/0.0/distil-whisper-large-v3.7z) | 最新优化 |

### 安装步骤

1. **下载模型文件**
   - 选择需要的模型下载
   - 文件格式为 .7z 压缩包

2. **解压模型**
   ```bash
   # Windows
   右键 -> 解压到当前文件夹
   
   # Linux/macOS
   7z x faster-small.7z
   ```

3. **放置模型**
   - 将解压后的文件夹复制到 `models` 目录
   - 确保目录结构正确

### 目录结构

正确的 Faster Whisper 模型目录结构：

```
models/
├── models--Systran--faster-whisper-tiny/
├── models--Systran--faster-whisper-base/
├── models--Systran--faster-whisper-small/
├── models--Systran--faster-whisper-medium/
├── models--Systran--faster-whisper-large-v2/
└── models--Systran--faster-whisper-large-v3/
```

## OpenAI Whisper 模型

### 下载地址

| 模型名称 | 大小 | 下载链接 |
|----------|------|----------|
| tiny | 66MB | [下载](https://openaipublic.azureedge.net/main/whisper/models/65147644a518d12f04e32d6f3b26facc3f8dd46e5390956a9424a650c0ce22b9/tiny.pt) |
| tiny.en | 74MB | [下载](https://openaipublic.azureedge.net/main/whisper/models/d3dd57d32accea0b295c96e26691aa14d8822fac7d9d27d5dc00b4ca2826dd03/tiny.en.pt) |
| base | 142MB | [下载](https://openaipublic.azureedge.net/main/whisper/models/ed3a0b6b1c0edf879ad9b11b1af5a0e6ab5db9205f891f668f8b0e6c6326e34e/base.pt) |
| base.en | 155MB | [下载](https://openaipublic.azureedge.net/main/whisper/models/25a8566e1d0c1e2231d1c762132cd20e0f96a85d16145c3a00adf5d1ac670ead/base.en.pt) |
| small | 500MB | [下载](https://openaipublic.azureedge.net/main/whisper/models/9ecf779972d90ba49c06d968637d720dd632c55bbf19d441fb42bf17a411e794/small.pt) |
| small.en | 518MB | [下载](https://openaipublic.azureedge.net/main/whisper/models/f953ad0fd29cacd07d5a9eda5624af0f6bcf2258be67c92b79389873d91e0872/small.en.pt) |
| medium | 1.5GB | [下载](https://openaipublic.azureedge.net/main/whisper/models/345ae4da62f9b3d59415adc60127b97c714f32e89e936602e85993674d08dcb1/medium.pt) |
| medium.en | 1.6GB | [下载](https://openaipublic.azureedge.net/main/whisper/models/d7440d1dc186f76616474e0ff0b3b6b879abc9d1a4926b7adfa41db2d497ab4f/medium.en.pt) |
| large-v1 | 2.9GB | [下载](https://openaipublic.azureedge.net/main/whisper/models/e4b87e7e0bf463eb8e6956e646f1e277e901512310def2c24bf0e11bd3c28e9a/large-v1.pt) |
| large-v2 | 2.9GB | [下载](https://openaipublic.azureedge.net/main/whisper/models/81f7c96c852ee8fc832187b0132e569d6c3065a3252ed18e56effd0b6a73e524/large-v2.pt) |
| large-v3 | 3GB | [下载](https://openaipublic.azureedge.net/main/whisper/models/e5b1a55b89c1367dacf97e3e19bfd829a01529dbfdeefa8caeb59b3f1b81dadb/large-v3.pt) |

### 安装步骤

1. **下载模型文件**
   - 直接下载 .pt 文件
   - 如果下载的是 .zip 文件，重命名为 .pt

2. **放置模型**
   - 将 .pt 文件直接复制到 `models` 目录

### 目录结构

正确的 OpenAI Whisper 模型目录结构：

```
models/
├── tiny.pt
├── tiny.en.pt
├── base.pt
├── base.en.pt
├── small.pt
├── small.en.pt
├── medium.pt
├── medium.en.pt
├── large-v1.pt
├── large-v2.pt
└── large-v3.pt
```

## UVR5 模型

UVR5 用于音频分离，可以保留背景音乐。

### 下载安装

1. **下载模型**
   - [UVR5 模型下载](https://github.com/jianchang512/stt/releases/download/0.0/uvr5-model.7z)

2. **解压安装**
   ```bash
   # 解压到项目根目录
   7z x uvr5-model.7z
   ```

3. **目录结构**
   ```
   pyvideotrans/
   ├── uvr5_weights/
   │   ├── HP2-人声vocals+非人声instrumentals.pth
   │   ├── HP3-人声vocals+非人声instrumentals.pth
   │   └── ...
   └── ...
   ```

## CUDA 加速库

如果您有 NVIDIA 显卡，可以下载 CUDA 库来加速处理。

### 检查 CUDA 版本

```bash
nvcc -V
```

### 下载对应版本

| CUDA 版本 | 下载链接 |
|-----------|----------|
| CUDA 11.x | [下载](https://github.com/jianchang512/stt/releases/download/0.0/cuBLAS.and.cuDNN_CUDA11_win_v4.7z) |
| CUDA 12.x | [下载](https://github.com/jianchang512/stt/releases/download/0.0/cuBLAS.and.cuDNN_CUDA12_win_v1.7z) |

### 安装步骤

1. **下载对应版本的库文件**
2. **解压文件**
3. **复制 DLL 文件**
   - Windows: 复制到 `C:/Windows/System32` 或项目根目录
   - Linux: 复制到系统库目录

## 模型选择建议

### 根据硬件配置选择

| 硬件配置 | 推荐模型 | 说明 |
|----------|----------|------|
| 低配置 (4GB RAM) | tiny, base | 快速处理，基本质量 |
| 中等配置 (8GB RAM) | small, medium | 平衡速度和质量 |
| 高配置 (16GB+ RAM) | large-v3 | 最佳质量 |
| 有 GPU | large + GPU 加速 | 最快速度，最佳质量 |

### 根据用途选择

| 用途 | 推荐模型 | 理由 |
|------|----------|------|
| 快速预览 | tiny | 速度最快 |
| 日常使用 | small | 质量和速度平衡 |
| 专业制作 | large-v3 | 质量最好 |
| 英语内容 | .en 模型 | 针对英语优化 |
| 多语言 | 通用模型 | 支持多种语言 |

## 下载工具

### 推荐下载工具

1. **IDM (Internet Download Manager)** - Windows
2. **wget** - Linux/macOS
   ```bash
   wget -c [下载链接]
   ```
3. **curl** - 跨平台
   ```bash
   curl -L -o model.7z [下载链接]
   ```

### 断点续传

大文件下载建议使用支持断点续传的工具：

```bash
# wget 断点续传
wget -c -t 0 [下载链接]

# curl 断点续传
curl -C - -L -o model.7z [下载链接]
```

## 常见问题

### 下载失败

**问题**: 下载中断或失败
**解决**:
1. 使用断点续传工具
2. 更换下载源
3. 检查网络连接
4. 使用代理或 VPN

### 解压失败

**问题**: 7z 文件解压失败
**解决**:
1. 重新下载文件
2. 检查文件完整性
3. 使用最新版本的 7-Zip
4. 确保磁盘空间充足

### 模型不识别

**问题**: 程序无法识别已下载的模型
**解决**:
1. 检查目录结构是否正确
2. 确认文件名和路径无误
3. 重启程序
4. 清理缓存文件

### GPU 加速不生效

**问题**: 下载了 CUDA 库但加速不生效
**解决**:
1. 确认 CUDA 版本匹配
2. 检查 GPU 驱动是否最新
3. 验证 PyTorch CUDA 支持
4. 重新安装 CUDA 库

## 验证安装

### 检查模型

在程序中检查模型是否正确加载：

1. 启动 PyVideoTrans
2. 查看模型选择下拉菜单
3. 确认所有下载的模型都出现在列表中

### 测试功能

1. 使用小文件测试语音识别
2. 检查处理速度和质量
3. 验证 GPU 加速是否生效

## 模型更新

### 检查更新

定期检查是否有新版本的模型：

1. 访问 [模型发布页面](https://github.com/jianchang512/stt/releases)
2. 查看最新版本信息
3. 下载并替换旧模型

### 自动更新

未来版本可能支持自动更新功能，敬请期待。

## 获取帮助

如果在模型下载和安装过程中遇到问题：

- 查看 [常见问题解答](../faq.md)
- 提交 [GitHub Issue](https://github.com/jianchang512/pyvideotrans/issues)
- 加入 [Discord 社区](https://discord.gg/y9gUweVCCJ)
- 参考 [官方文档](https://pyvideotrans.com/model.html)