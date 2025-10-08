# Windows 源码安装指南

本指南详细说明如何在 Windows 10/11 系统上从源码安装 PyVideoTrans。

## 前置要求

### 1. 安装 Python 3.10

1. 访问 [Python 官网](https://www.python.org/downloads/)
2. 下载 Python 3.10.x 版本
3. 运行安装程序，**务必勾选 "Add to PATH"**
4. 验证安装：
   ```cmd
   python -V
   ```
   应该输出 `Python 3.10.x`

### 2. 安装 Git

1. 下载 [Git for Windows](https://github.com/git-for-windows/git/releases/download/v2.45.0.windows.1/Git-2.45.0-64-bit.exe)
2. 运行安装程序，使用默认设置

## 安装步骤

### 1. 获取源码

1. 选择一个**不含空格和中文**的目录
2. 在地址栏输入 `cmd` 并按回车打开终端
3. 克隆仓库：
   ```cmd
   git clone https://github.com/jianchang512/pyvideotrans
   ```
4. 进入项目目录：
   ```cmd
   cd pyvideotrans
   ```

### 2. 创建虚拟环境

```cmd
python -m venv venv
```

### 3. 激活虚拟环境

```cmd
.\venv\scripts\activate
```

激活后，命令行提示符应该以 `(venv)` 开头。

### 4. 安装依赖

```cmd
pip install -r requirements.txt
```

如果安装失败，尝试使用国内镜像：

```cmd
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
pip config set install.trusted-host mirrors.aliyun.com
pip install -r requirements.txt
```

### 5. 配置 FFmpeg

#### 方法一：使用项目提供的 FFmpeg

如果项目根目录有 `ffmpeg.zip`：
1. 解压 `ffmpeg.zip` 到当前目录
2. 确保 `ffmpeg` 文件夹包含 `ffmpeg.exe`、`ffprobe.exe`、`ytwin32.exe`

#### 方法二：手动下载 FFmpeg

1. 下载 [FFmpeg](https://github.com/BtbN/FFmpeg-Builds/releases/download/autobuild-2023-11-30-12-55/ffmpeg-n6.0.1-win64-gpl-6.0.zip)
2. 解压后将 `bin` 目录下的 `ffmpeg.exe` 和 `ffprobe.exe` 复制到项目根目录的 `ffmpeg` 文件夹
3. 下载 [yt-dlp](https://github.com/yt-dlp/yt-dlp/releases/download/2024.07.16/yt-dlp.exe)
4. 重命名为 `ytwin32.exe` 并放入 `ffmpeg` 文件夹

### 6. GPU 加速配置（可选）

如果您有 NVIDIA 显卡并希望启用 GPU 加速：

#### 安装 CUDA

1. 检查显卡支持的 CUDA 版本
2. 下载并安装 [CUDA Toolkit 11.8+](https://developer.nvidia.com/cuda-downloads)
3. 验证安装：
   ```cmd
   nvcc -V
   ```

#### 安装 GPU 版本的 PyTorch

```cmd
pip uninstall -y torch torchaudio
pip install torch==2.2.0 torchaudio==2.2.0 --index-url https://download.pytorch.org/whl/cu118
```

详细的 GPU 配置请参考：[CUDA 加速支持](https://pyvideotrans.com/gpu.html)

## 启动程序

```cmd
python sp.py
```

## 常见问题

### Python 版本问题

**错误**: `python -V` 输出不是 3.10.x

**解决**: 
1. 重新安装 Python 3.10，确保勾选 "Add to PATH"
2. 重启命令行窗口
3. 如果系统有多个 Python 版本，使用 `python3.10 -V` 或 `py -3.10 -V`

### 虚拟环境激活失败

**错误**: 执行策略限制

**解决**: 以管理员身份运行 PowerShell，执行：
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### 依赖安装失败

**错误**: 某些包安装失败

**解决**:
1. 确保网络连接正常
2. 使用国内镜像源（见上文）
3. 单独安装失败的包：
   ```cmd
   pip install 包名
   ```

### FFmpeg 相关错误

**错误**: `ffmpeg not found`

**解决**:
1. 确保 `ffmpeg` 文件夹存在于项目根目录
2. 确保文件夹内有 `ffmpeg.exe` 和 `ffprobe.exe`
3. 检查文件权限，确保可执行

### GPU 加速问题

**错误**: CUDA 相关错误

**解决**:
1. 确认显卡支持 CUDA
2. 检查 CUDA 版本兼容性
3. 重新安装对应版本的 PyTorch
4. 如果问题持续，可以禁用 GPU 加速使用 CPU 模式

## 目录结构

安装完成后的目录结构应该如下：

```
pyvideotrans/
├── venv/                 # 虚拟环境
├── videotrans/          # 主程序代码
├── docs/                # 文档
├── ffmpeg/              # FFmpeg 工具
│   ├── ffmpeg.exe
│   ├── ffprobe.exe
│   └── ytwin32.exe
├── models/              # 模型文件（需要单独下载）
├── sp.py               # 启动脚本
├── requirements.txt    # 依赖列表
└── README.md          # 说明文档
```

## 下一步

安装完成后：

1. [下载必要的模型文件](model-download.md)
2. 阅读 [用户使用指南](user-guide.md)
3. 查看 [API 文档](../api/api.md)

## 获取帮助

如果遇到问题：

- 查看 [常见问题解答](../faq.md)
- 提交 [GitHub Issue](https://github.com/jianchang512/pyvideotrans/issues)
- 加入 [Discord 社区](https://discord.gg/y9gUweVCCJ)