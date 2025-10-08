# macOS 源码安装指南

本指南详细说明如何在 macOS 系统上从源码安装 PyVideoTrans。

## 前置要求

### 系统要求

- macOS 10.14 或更高版本
- 至少 4GB RAM，推荐 8GB+
- 5GB 可用存储空间

### 1. 安装 Homebrew

如果尚未安装 Homebrew，请先安装：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

安装完成后配置环境：

```bash
eval $(brew --config)
```

### 2. 安装系统依赖

```bash
brew install libsndfile
brew install ffmpeg
brew install git
brew install python@3.10
```

### 3. 配置 Python 环境

```bash
export PATH="/usr/local/opt/python@3.10/bin:$PATH"
source ~/.bash_profile 
source ~/.zshrc
```

验证 Python 安装：

```bash
python3 -V
```

应该输出 `Python 3.10.x`

## 安装步骤

### 1. 获取源码

1. 创建一个**不含空格和中文字符**的目录
2. 在终端中进入该目录
3. 克隆仓库：
   ```bash
   git clone https://github.com/jianchang512/pyvideotrans
   ```
4. 进入项目目录：
   ```bash
   cd pyvideotrans
   ```

### 2. 创建虚拟环境

```bash
python3 -m venv venv
```

### 3. 激活虚拟环境

```bash
source ./venv/bin/activate
```

激活后，命令行提示符应该以 `(venv)` 开头。

### 4. 安装 Python 依赖

```bash
pip install -r requirements.txt
```

如果安装失败，尝试使用国内镜像：

```bash
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
pip config set install.trusted-host mirrors.aliyun.com
pip install -r requirements.txt
```

### 5. GPU 加速配置（可选）

macOS 支持 Metal Performance Shaders (MPS) 加速：

#### 对于 Apple Silicon (M1/M2/M3) Mac

PyTorch 会自动检测并使用 MPS 加速，无需额外配置。

#### 验证 MPS 支持

```python
python3 -c "import torch; print('MPS available:', torch.backends.mps.is_available())"
```

## 启动程序

```bash
python3 sp.py
```

## 常见问题

### Homebrew 安装问题

**错误**: Homebrew 安装失败或速度慢

**解决**: 使用国内镜像安装 Homebrew：

```bash
/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)"
```

### Python 版本问题

**错误**: 系统默认 Python 不是 3.10

**解决**: 
1. 确保 Homebrew 安装的 Python 在 PATH 中：
   ```bash
   echo 'export PATH="/usr/local/opt/python@3.10/bin:$PATH"' >> ~/.zshrc
   source ~/.zshrc
   ```
2. 或者使用完整路径：
   ```bash
   /usr/local/opt/python@3.10/bin/python3 -m venv venv
   ```

### 权限问题

**错误**: 权限被拒绝

**解决**: 
1. 确保对项目目录有写权限
2. 避免使用 `sudo` 安装 pip 包
3. 如果必要，修改目录权限：
   ```bash
   chmod -R 755 pyvideotrans
   ```

### 依赖编译问题

**错误**: 某些包编译失败（如 numpy, scipy）

**解决**: 
1. 安装 Xcode Command Line Tools：
   ```bash
   xcode-select --install
   ```
2. 更新 pip 和 setuptools：
   ```bash
   pip install --upgrade pip setuptools wheel
   ```

### FFmpeg 问题

**错误**: FFmpeg 相关错误

**解决**: 
1. 确认 FFmpeg 安装：
   ```bash
   ffmpeg -version
   ```
2. 如果未安装或版本过旧：
   ```bash
   brew reinstall ffmpeg
   ```

### 虚拟环境问题

**错误**: 虚拟环境激活失败

**解决**: 
1. 删除现有虚拟环境：
   ```bash
   rm -rf venv
   ```
2. 重新创建：
   ```bash
   python3 -m venv venv
   source ./venv/bin/activate
   ```

## 性能优化

### 针对 Apple Silicon 优化

1. 确保使用原生 ARM64 版本的依赖：
   ```bash
   pip install --upgrade --force-reinstall torch torchaudio
   ```

2. 启用 MPS 加速（在程序设置中）

### 内存优化

对于内存较小的 Mac：

1. 使用较小的模型（如 tiny、base）
2. 减少并发处理数量
3. 关闭不必要的应用程序

## 目录结构

安装完成后的目录结构：

```
pyvideotrans/
├── venv/                 # 虚拟环境
├── videotrans/          # 主程序代码
├── docs/                # 文档
├── models/              # 模型文件（需要单独下载）
├── sp.py               # 启动脚本
├── requirements.txt    # 依赖列表
└── README.md          # 说明文档
```

## 自动启动脚本

创建启动脚本以便快速启动：

```bash
#!/bin/bash
cd /path/to/pyvideotrans
source ./venv/bin/activate
python3 sp.py
```

保存为 `start_pyvideotrans.sh` 并添加执行权限：

```bash
chmod +x start_pyvideotrans.sh
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
- 参考 [详细部署方案](https://pyvideotrans.com/mac.html)

## 卸载

如需卸载 PyVideoTrans：

1. 删除项目目录：
   ```bash
   rm -rf pyvideotrans
   ```

2. 可选：卸载 Homebrew 依赖（如果不再需要）：
   ```bash
   brew uninstall python@3.10 ffmpeg git libsndfile