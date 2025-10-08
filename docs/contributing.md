# 贡献指南

感谢您考虑为 PyVideoTrans 项目做出贡献！本指南将帮助您了解如何参与项目开发。

## 贡献方式

### 🐛 报告问题

如果您发现了 bug 或有功能建议：

1. **检查现有 Issues** - 确保问题未被报告过
2. **创建新 Issue** - 使用合适的模板
3. **提供详细信息** - 包括复现步骤、环境信息等

### 💡 功能请求

提出新功能建议：

1. **描述用例** - 说明为什么需要这个功能
2. **提供详细设计** - 如果可能，提供设计思路
3. **考虑兼容性** - 确保不会破坏现有功能

### 📝 改进文档

文档贡献包括：

- 修正错误和不准确信息
- 添加缺失的说明
- 改进文档结构和可读性
- 翻译文档到其他语言

### 💻 代码贡献

代码贡献是最直接的参与方式：

- 修复 bug
- 实现新功能
- 性能优化
- 代码重构

## 开发环境搭建

### 1. Fork 项目

1. 访问 [PyVideoTrans GitHub 页面](https://github.com/jianchang512/pyvideotrans)
2. 点击右上角 "Fork" 按钮
3. 克隆您的 fork 到本地：

```bash
git clone https://github.com/你的用户名/pyvideotrans.git
cd pyvideotrans
```

### 2. 设置开发环境

```bash
# 创建虚拟环境
python -m venv venv

# 激活虚拟环境
# Windows
.\venv\scripts\activate
# macOS/Linux
source ./venv/bin/activate

# 安装依赖
pip install -r requirements.txt

# 安装开发依赖
pip install -r requirements-dev.txt  # 如果存在
```

### 3. 配置 Git

```bash
# 添加原始仓库为上游
git remote add upstream https://github.com/jianchang512/pyvideotrans.git

# 配置用户信息
git config user.name "您的姓名"
git config user.email "您的邮箱"
```

## 开发流程

### 1. 创建功能分支

```bash
# 确保在最新主分支
git checkout main
git pull upstream main

# 创建新分支
git checkout -b feature/功能名称
# 或
git checkout -b fix/问题描述
```

### 2. 进行开发

- 遵循项目代码风格
- 添加必要的测试
- 更新相关文档
- 确保代码通过所有测试

### 3. 提交更改

```bash
# 添加更改的文件
git add .

# 提交更改（使用有意义的提交信息）
git commit -m "类型: 简短描述

详细描述更改内容和原因（如果需要）"
```

#### 提交信息格式

使用以下格式编写提交信息：

```
类型: 简短描述 (不超过50字符)

详细描述 (如果需要，每行不超过72字符)

- 解决的问题
- 实现的功能
- 注意事项
```

**提交类型**:
- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档更新
- `style`: 代码格式调整
- `refactor`: 代码重构
- `test`: 测试相关
- `chore`: 构建过程或辅助工具的变动

### 4. 推送更改

```bash
git push origin feature/功能名称
```

### 5. 创建 Pull Request

1. 访问您的 fork 页面
2. 点击 "New Pull Request"
3. 选择正确的分支
4. 填写 PR 描述
5. 提交 PR

## Pull Request 指南

### PR 标题格式

```
类型: 简短描述功能或修复
```

### PR 描述模板

```markdown
## 更改类型
- [ ] Bug 修复
- [ ] 新功能
- [ ] 文档更新
- [ ] 代码重构
- [ ] 性能优化

## 更改描述
简要描述此 PR 的更改内容。

## 相关 Issue
关闭 #issue号码

## 测试
- [ ] 已添加测试用例
- [ ] 所有测试通过
- [ ] 手动测试通过

## 检查清单
- [ ] 代码遵循项目规范
- [ ] 已更新相关文档
- [ ] 提交信息清晰明确
- [ ] 已解决所有冲突
```

### PR 审查过程

1. **自动检查**: CI/CD 会自动运行测试
2. **代码审查**: 维护者会审查您的代码
3. **讨论修改**: 根据反馈进行必要修改
4. **合并**: 审查通过后合并到主分支

## 代码规范

### Python 代码风格

遵循 PEP 8 标准：

```python
# 好的例子
def process_video(input_file: str, output_file: str) -> bool:
    """
    处理视频文件
    
    Args:
        input_file: 输入文件路径
        output_file: 输出文件路径
        
    Returns:
        处理是否成功
    """
    try:
        # 处理逻辑
        return True
    except Exception as e:
        logger.error(f"处理视频失败: {e}")
        return False
```

### 命名规范

- **文件名**: 使用小写字母和下划线 `video_processor.py`
- **类名**: 使用驼峰命名 `VideoProcessor`
- **函数名**: 使用小写字母和下划线 `process_video`
- **常量**: 使用大写字母和下划线 `MAX_FILE_SIZE`

### 注释规范

```python
class VideoProcessor:
    """
    视频处理器类
    
    负责处理视频文件的各种操作，包括转码、翻译等。
    """
    
    def __init__(self, config: dict):
        """
        初始化视频处理器
        
        Args:
            config: 配置字典
        """
        self.config = config
    
    def process(self, video_path: str) -> str:
        """
        处理视频文件
        
        Args:
            video_path: 视频文件路径
            
        Returns:
            处理后的文件路径
            
        Raises:
            VideoProcessError: 处理失败时抛出
        """
        # 实现逻辑
        pass
```

## 测试指南

### 运行测试

```bash
# 运行所有测试
python -m pytest

# 运行特定测试文件
python -m pytest tests/test_video_processor.py

# 运行带覆盖率的测试
python -m pytest --cov=videotrans
```

### 编写测试

```python
import unittest
from videotrans.processor import VideoProcessor

class TestVideoProcessor(unittest.TestCase):
    
    def setUp(self):
        """测试前的准备工作"""
        self.processor = VideoProcessor({})
    
    def test_process_valid_video(self):
        """测试处理有效视频文件"""
        result = self.processor.process("test_video.mp4")
        self.assertTrue(result)
    
    def test_process_invalid_video(self):
        """测试处理无效视频文件"""
        with self.assertRaises(VideoProcessError):
            self.processor.process("invalid.txt")
```

## 文档贡献

### 文档结构

```
docs/
├── guides/          # 使用指南
├── api/            # API 文档
├── locales/        # 多语言文档
├── providers/      # 服务商配置
└── README.md       # 项目说明
```

### Markdown 规范

```markdown
# 一级标题

## 二级标题

### 三级标题

- 使用 `-` 作为无序列表标记
- 代码块使用三个反引号包围
- 链接格式：[链接文本](URL)
- 图片格式：![替代文本](图片URL)

```python
# 代码示例
def example_function():
    return "Hello, World!"
```
```

## 发布流程

### 版本号规范

使用语义化版本控制 (SemVer)：

- **主版本号**: 不兼容的 API 修改
- **次版本号**: 向后兼容的功能性新增
- **修订号**: 向后兼容的问题修正

例如：`v3.80.1`

### 发布检查清单

- [ ] 所有测试通过
- [ ] 文档已更新
- [ ] 版本号已更新
- [ ] 更新日志已完善
- [ ] 依赖项已检查

## 社区行为准则

### 我们的承诺

为了营造一个开放且友好的环境，我们承诺：

- 使用友好和包容的语言
- 尊重不同的观点和经验
- 优雅地接受建设性批评
- 关注对社区最有利的事情
- 与其他社区成员友善相处

### 不当行为

不可接受的行为包括：

- 侮辱性/贬损性言论，人身攻击
- 公开或私下的骚扰
- 未经许可发布他人隐私信息
- 在专业环境中不当的其他行为

## 获得帮助

如果您在贡献过程中遇到问题：

### 技术问题
- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)

### 贡献相关
- 查看现有的 Issues 和 PRs
- 在 Discord 中询问
- 发送邮件至 jianchang512@gmail.com

## 感谢贡献者

感谢所有为 PyVideoTrans 做出贡献的开发者！您的每一份贡献都让项目变得更好。

### 贡献者名单

项目的贡献者列表可以在 [Contributors 页面](https://github.com/jianchang512/pyvideotrans/graphs/contributors) 查看。

### 贡献类型

贡献不仅限于代码，还包括：

- 📝 文档改进
- 🐛 问题报告
- 💡 功能建议
- 🌍 翻译工作
- 🎨 界面设计
- 📢 项目推广
- 💬 社区支持

---

再次感谢您的贡献！让我们一起让 PyVideoTrans 变得更好！