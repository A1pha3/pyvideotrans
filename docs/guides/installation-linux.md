# Linux 源码安装指南

本指南详细说明如何在 Linux 系统上从源码安装 PyVideoTrans。

## 支持的发行版

- Ubuntu 18.04+
- Debian 10+
- CentOS 7+
- RHEL 7+
- Fedora 30+
- openSUSE Leap 15+

## 前置要求

### 系统要求

- Linux 内核 4.0+
- 至少 4GB RAM，推荐 8GB+
- 5GB 可用存储空间
- 可选：NVIDIA GPU (支持 CUDA 11.8+)

## 安装步骤

### Ubuntu/Debian 系统

#### 1. 更新系统

```bash
sudo apt update && sudo apt upgrade -y
```

#### 2. 安装系统依赖

```bash
sudo apt install software-properties-common -y
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt-get install libxcb-cursor0
sudo apt install python3.10 python3.10-venv python3.10-dev
sudo apt-get install ffmpeg git build-essential
```

#### 3. 安装 pip

```bash
curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10
```

#### 4. 配置 Python 默认版本

```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.10 1
sudo update-alternatives --config python
```

验证安装：

```bash
python3 -V
```

应该输出 `Python 3.10.x`

### CentOS/RHEL 系统

#### 1. 更新系统

```bash
sudo yum update
```

#### 2. 安装开发工具

```bash
sudo yum groupinstall "Development Tools"
sudo yum install openssl-devel bzip2-devel libffi-devel
```

#### 3. 编译安装 Python 3.10

```bash
cd /tmp
wget https://www.python.org/ftp/python/3.10.4/Python-3.10.4.tgz
tar xzf Python-3.10.4.tgz
cd Python-3.10.4
./configure --enable-optimizations
sudo make && sudo make install
sudo alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.10 1
```

#### 4. 安装 FFmpeg

```bash
# 启用 EPEL 仓库
sudo yum install epel-release
sudo yum install ffmpeg
```

或者编译安装最新版本：

```bash
# 安装依赖
sudo yum install nasm yasm-devel

# 编译 FFmpeg
cd /tmp
wget https://ffmpeg.org/releases/ffmpeg-6.0.tar.xz
tar xf ffmpeg-6.0.tar.xz
cd ffmpeg-6.0
./configure --enable-gpl --enable-libx264 --enable-libx265
make -j$(nproc)
sudo make install
```

## 通用安装步骤

### 1. 获取源码

```bash
# 创建项目目录
mkdir -p ~/projects
cd ~/projects

# 克隆仓库
git clone https://github.com/jianchang512/pyvideotrans
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

如果您有 NVIDIA 显卡并希望启用 GPU 加速：

#### 安装 NVIDIA 驱动

```bash
# Ubuntu/Debian
sudo apt install nvidia-driver-470

# CentOS/RHEL
sudo yum install nvidia-driver
```

#### 安装 CUDA Toolkit

1. 访问 [NVIDIA CUDA 下载页面](https://developer.nvidia.com/cuda-downloads)
2. 选择对应的 Linux 发行版
3. 按照说明安装 CUDA 11.8+

#### 验证 CUDA 安装

```bash
nvcc -V
nvidia-smi
```

#### 安装 GPU 版本的 PyTorch

```bash
pip uninstall -y torch torchaudio
pip install torch==2.2.0 torchaudio==2.2.0 --index-url https://download.pytorch.org/whl/cu118
pip install nvidia-cublas-cu11 nvidia-cudnn-cu11
```

## 启动程序

```bash
python sp.py
```

## 常见问题

### Python 编译问题

**错误**: Python 编译失败

**解决**: 
1. 确保安装了所有开发依赖：
   ```bash
   # Ubuntu/Debian
   sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev
   
   # CentOS/RHEL
   sudo yum install gcc gcc-c++ make zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel expat-devel
   ```

### 权限问题

**错误**: 权限被拒绝

**解决**: 
1. 确保对项目目录有写权限
2. 避免使用 `sudo` 运行程序
3. 修改目录权限：
   ```bash
   chmod -R 755 ~/projects/pyvideotrans
   ```

### 依赖安装问题

**错误**: 某些包安装失败

**解决**: 
1. 更新 pip：
   ```bash
   pip install --upgrade pip setuptools wheel
   ```
2. 安装系统级依赖：
   ```bash
   # Ubuntu/Debian
   sudo apt install python3.10-dev libportaudio2 libportaudiocpp0 portaudio19-dev
   
   # CentOS/RHEL
   sudo yum install python3-devel portaudio-devel
   ```

### 音频处理问题

**错误**: 音频库相关错误

**解决**: 
```bash
# Ubuntu/Debian
sudo apt install libasound2-dev libpulse-dev

# CentOS/RHEL
sudo yum install alsa-lib-devel pulseaudio-libs-devel
```

### 显示问题

**错误**: GUI 相关错误

**解决**: 
1. 安装 X11 依赖：
   ```bash
   # Ubuntu/Debian
   sudo apt install libxcb-xinerama0 libxcb-cursor0
   
   # CentOS/RHEL
   sudo yum install libxcb-devel xcb-util-cursor-devel
   ```

2. 如果使用 SSH，启用 X11 转发：
   ```bash
   ssh -X username@hostname
   ```

### CUDA 问题

**错误**: CUDA 相关错误

**解决**: 
1. 检查 CUDA 版本兼容性
2. 确认环境变量：
   ```bash
   export PATH=/usr/local/cuda/bin:$PATH
   export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
   ```
3. 重新安装对应版本的 PyTorch

## 系统服务配置（可选）

创建系统服务以便自动启动：

### 1. 创建服务文件

```bash
sudo nano /etc/systemd/system/pyvideotrans.service
```

### 2. 添加服务配置

```ini
[Unit]
Description=PyVideoTrans Service
After=network.target

[Service]
Type=simple
User=your_username
WorkingDirectory=/home/your_username/projects/pyvideotrans
Environment=PATH=/home/your_username/projects/pyvideotrans/venv/bin
ExecStart=/home/your_username/projects/pyvideotrans/venv/bin/python sp.py
Restart=always

[Install]
WantedBy=multi-user.target
```

### 3. 启用服务

```bash
sudo systemctl daemon-reload
sudo systemctl enable pyvideotrans
sudo systemctl start pyvideotrans
```

## 性能优化

### 系统级优化

1. 增加文件描述符限制：
   ```bash
   echo "* soft nofile 65536" | sudo tee -a /etc/security/limits.conf
   echo "* hard nofile 65536" | sudo tee -a /etc/security/limits.conf
   ```

2. 优化内存使用：
   ```bash
   echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
   ```

### 应用级优化

1. 使用较小的模型以减少内存使用
2. 调整并发处理数量
3. 启用 GPU 加速（如果可用）

## 目录结构

安装完成后的目录结构：

```
~/projects/pyvideotrans/
├── venv/                 # 虚拟环境
├── videotrans/          # 主程序代码
├── docs/                # 文档
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

## 卸载

如需卸载 PyVideoTrans：

1. 停止服务（如果配置了）：
   ```bash
   sudo systemctl stop pyvideotrans
   sudo systemctl disable pyvideotrans
   sudo rm /etc/systemd/system/pyvideotrans.service
   ```

2. 删除项目目录：
   ```bash
   rm -rf ~/projects/pyvideotrans
   ```

3. 可选：卸载系统依赖（如果不再需要）