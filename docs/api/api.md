# PyVideoTrans API 文档

PyVideoTrans 提供了丰富的 API 接口，支持程序化调用各种功能。本文档详细介绍了所有可用的 API。

## API 概述

### 基本信息

- **版本**: v3.80
- **基础路径**: `/api/v1`
- **内容类型**: `application/json`
- **字符编码**: UTF-8

### 认证方式

目前 API 主要用于本地调用，暂不需要认证。未来版本可能会添加 API Key 认证。

## 核心 API

### 1. 视频翻译 API

#### 开始翻译任务

```http
POST /api/v1/translate
Content-Type: application/json

{
  "input_file": "path/to/input.mp4",
  "output_dir": "path/to/output",
  "source_language": "zh",
  "target_language": "en",
  "model_name": "small",
  "translate_service": "google",
  "voice_service": "edge-tts",
  "voice_name": "en-US-AriaNeural",
  "subtitle_type": "srt",
  "keep_background_music": true,
  "voice_rate": 0,
  "voice_volume": 100,
  "background_music_volume": 50
}
```

**参数说明**:

| 参数 | 类型 | 必需 | 描述 |
|------|------|------|------|
| `input_file` | string | 是 | 输入视频文件路径 |
| `output_dir` | string | 是 | 输出目录路径 |
| `source_language` | string | 是 | 源语言代码 |
| `target_language` | string | 是 | 目标语言代码 |
| `model_name` | string | 否 | 语音识别模型名称 (默认: small) |
| `translate_service` | string | 否 | 翻译服务提供商 (默认: google) |
| `voice_service` | string | 否 | 语音合成服务 (默认: edge-tts) |
| `voice_name` | string | 否 | 语音名称 |
| `subtitle_type` | string | 否 | 字幕格式 (srt/vtt/ass) |
| `keep_background_music` | boolean | 否 | 是否保留背景音乐 |
| `voice_rate` | integer | 否 | 语音速度调整 (-50 到 50) |
| `voice_volume` | integer | 否 | 语音音量 (0-100) |
| `background_music_volume` | integer | 否 | 背景音乐音量 (0-100) |

**响应示例**:

```json
{
  "success": true,
  "task_id": "task_123456789",
  "message": "翻译任务已开始",
  "estimated_time": 300
}
```

#### 查询任务状态

```http
GET /api/v1/task/{task_id}
```

**响应示例**:

```json
{
  "success": true,
  "task_id": "task_123456789",
  "status": "processing",
  "progress": 45,
  "current_step": "语音识别",
  "estimated_remaining": 180,
  "output_files": []
}
```

**状态值**:
- `pending`: 等待中
- `processing`: 处理中
- `completed`: 已完成
- `failed`: 失败
- `cancelled`: 已取消

### 2. 语音识别 API

#### 音频转文字

```http
POST /api/v1/speech-to-text
Content-Type: application/json

{
  "input_file": "path/to/audio.wav",
  "model_name": "small",
  "language": "zh",
  "output_format": "srt"
}
```

**参数说明**:

| 参数 | 类型 | 必需 | 描述 |
|------|------|------|------|
| `input_file` | string | 是 | 输入音频/视频文件路径 |
| `model_name` | string | 否 | 识别模型名称 |
| `language` | string | 否 | 语言代码 (auto 表示自动检测) |
| `output_format` | string | 否 | 输出格式 (srt/txt/json) |

**响应示例**:

```json
{
  "success": true,
  "task_id": "stt_123456789",
  "text": "识别出的文本内容",
  "subtitle_file": "path/to/output.srt",
  "segments": [
    {
      "start": 0.0,
      "end": 2.5,
      "text": "第一段文字"
    }
  ]
}
```

### 3. 文本翻译 API

#### 翻译文本

```http
POST /api/v1/translate-text
Content-Type: application/json

{
  "text": "要翻译的文本",
  "source_language": "zh",
  "target_language": "en",
  "service": "google"
}
```

**参数说明**:

| 参数 | 类型 | 必需 | 描述 |
|------|------|------|------|
| `text` | string | 是 | 要翻译的文本 |
| `source_language` | string | 是 | 源语言代码 |
| `target_language` | string | 是 | 目标语言代码 |
| `service` | string | 否 | 翻译服务提供商 |

**响应示例**:

```json
{
  "success": true,
  "original_text": "要翻译的文本",
  "translated_text": "Text to translate",
  "source_language": "zh",
  "target_language": "en",
  "service": "google"
}
```

### 4. 语音合成 API

#### 文字转语音

```http
POST /api/v1/text-to-speech
Content-Type: application/json

{
  "text": "要合成的文本",
  "language": "en",
  "voice_name": "en-US-AriaNeural",
  "service": "edge-tts",
  "rate": 0,
  "volume": 100,
  "output_file": "path/to/output.wav"
}
```

**参数说明**:

| 参数 | 类型 | 必需 | 描述 |
|------|------|------|------|
| `text` | string | 是 | 要合成的文本 |
| `language` | string | 是 | 语言代码 |
| `voice_name` | string | 否 | 语音名称 |
| `service` | string | 否 | TTS 服务提供商 |
| `rate` | integer | 否 | 语速调整 (-50 到 50) |
| `volume` | integer | 否 | 音量 (0-100) |
| `output_file` | string | 否 | 输出文件路径 |

**响应示例**:

```json
{
  "success": true,
  "audio_file": "path/to/output.wav",
  "duration": 5.2,
  "voice_info": {
    "name": "en-US-AriaNeural",
    "language": "en-US",
    "gender": "Female"
  }
}
```

### 5. 系统信息 API

#### 获取系统状态

```http
GET /api/v1/system/status
```

**响应示例**:

```json
{
  "success": true,
  "version": "v3.80",
  "system": {
    "os": "Windows 10",
    "python_version": "3.10.4",
    "cpu_count": 8,
    "memory_total": "16 GB",
    "memory_available": "8 GB"
  },
  "gpu": {
    "available": true,
    "name": "NVIDIA RTX 3080",
    "memory": "10 GB",
    "cuda_version": "11.8"
  },
  "models": {
    "loaded": ["small", "medium"],
    "available": ["tiny", "base", "small", "medium", "large"]
  }
}
```

#### 获取支持的语言

```http
GET /api/v1/system/languages
```

**响应示例**:

```json
{
  "success": true,
  "languages": [
    {
      "code": "zh",
      "name": "中文",
      "english_name": "Chinese"
    },
    {
      "code": "en",
      "name": "English",
      "english_name": "English"
    }
  ]
}
```

#### 获取可用模型

```http
GET /api/v1/system/models
```

**响应示例**:

```json
{
  "success": true,
  "models": {
    "speech_recognition": [
      {
        "name": "tiny",
        "size": "64MB",
        "languages": ["multilingual"],
        "loaded": false
      },
      {
        "name": "small",
        "size": "415MB",
        "languages": ["multilingual"],
        "loaded": true
      }
    ],
    "translation": [
      {
        "name": "google",
        "type": "online",
        "languages": 100
      },
      {
        "name": "deepl",
        "type": "online",
        "languages": 30
      }
    ],
    "text_to_speech": [
      {
        "name": "edge-tts",
        "type": "online",
        "voices": 200
      }
    ]
  }
}
```

## 批量处理 API

### 批量翻译

```http
POST /api/v1/batch/translate
Content-Type: application/json

{
  "files": [
    "path/to/video1.mp4",
    "path/to/video2.mp4"
  ],
  "output_dir": "path/to/output",
  "config": {
    "source_language": "zh",
    "target_language": "en",
    "model_name": "small"
  }
}
```

### 批量字幕生成

```http
POST /api/v1/batch/subtitles
Content-Type: application/json

{
  "files": [
    "path/to/audio1.wav",
    "path/to/video2.mp4"
  ],
  "output_dir": "path/to/output",
  "config": {
    "model_name": "small",
    "language": "auto",
    "format": "srt"
  }
}
```

## 错误处理

### 错误响应格式

```json
{
  "success": false,
  "error_code": "INVALID_FILE",
  "message": "指定的文件不存在或无法访问",
  "details": {
    "file": "path/to/missing.mp4",
    "timestamp": "2024-01-01T12:00:00Z"
  }
}
```

### 常见错误代码

| 错误代码 | HTTP 状态码 | 描述 |
|----------|-------------|------|
| `INVALID_FILE` | 400 | 文件不存在或格式不支持 |
| `INVALID_LANGUAGE` | 400 | 不支持的语言代码 |
| `MODEL_NOT_FOUND` | 404 | 指定的模型未找到 |
| `INSUFFICIENT_MEMORY` | 500 | 内存不足 |
| `PROCESSING_ERROR` | 500 | 处理过程中发生错误 |
| `NETWORK_ERROR` | 503 | 网络连接错误 |

## 使用示例

### Python 示例

```python
import requests
import json

class PyVideoTransAPI:
    def __init__(self, base_url="http://localhost:8080"):
        self.base_url = base_url
    
    def translate_video(self, input_file, output_dir, source_lang, target_lang):
        """翻译视频"""
        url = f"{self.base_url}/api/v1/translate"
        data = {
            "input_file": input_file,
            "output_dir": output_dir,
            "source_language": source_lang,
            "target_language": target_lang
        }
        
        response = requests.post(url, json=data)
        return response.json()
    
    def get_task_status(self, task_id):
        """获取任务状态"""
        url = f"{self.base_url}/api/v1/task/{task_id}"
        response = requests.get(url)
        return response.json()
    
    def speech_to_text(self, audio_file, language="auto"):
        """语音转文字"""
        url = f"{self.base_url}/api/v1/speech-to-text"
        data = {
            "input_file": audio_file,
            "language": language,
            "output_format": "srt"
        }
        
        response = requests.post(url, json=data)
        return response.json()

# 使用示例
api = PyVideoTransAPI()

# 开始翻译任务
result = api.translate_video(
    input_file="example.mp4",
    output_dir="./output",
    source_lang="zh",
    target_lang="en"
)

if result["success"]:
    task_id = result["task_id"]
    print(f"任务已开始，ID: {task_id}")
    
    # 查询任务状态
    status = api.get_task_status(task_id)
    print(f"任务状态: {status['status']}")
```

### JavaScript 示例

```javascript
class PyVideoTransAPI {
    constructor(baseUrl = 'http://localhost:8080') {
        this.baseUrl = baseUrl;
    }
    
    async translateVideo(inputFile, outputDir, sourceLang, targetLang) {
        const response = await fetch(`${this.baseUrl}/api/v1/translate`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                input_file: inputFile,
                output_dir: outputDir,
                source_language: sourceLang,
                target_language: targetLang
            })
        });
        
        return await response.json();
    }
    
    async getTaskStatus(taskId) {
        const response = await fetch(`${this.baseUrl}/api/v1/task/${taskId}`);
        return await response.json();
    }
    
    async speechToText(audioFile, language = 'auto') {
        const response = await fetch(`${this.baseUrl}/api/v1/speech-to-text`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                input_file: audioFile,
                language: language,
                output_format: 'srt'
            })
        });
        
        return await response.json();
    }
}

// 使用示例
const api = new PyVideoTransAPI();

async function translateExample() {
    try {
        const result = await api.translateVideo(
            'example.mp4',
            './output',
            'zh',
            'en'
        );
        
        if (result.success) {
            console.log(`任务已开始，ID: ${result.task_id}`);
            
            // 轮询任务状态
            const checkStatus = async () => {
                const status = await api.getTaskStatus(result.task_id);
                console.log(`任务状态: ${status.status}`);
                
                if (status.status === 'processing') {
                    setTimeout(checkStatus, 5000); // 5秒后再次检查
                }
            };
            
            checkStatus();
        }
    } catch (error) {
        console.error('API 调用失败:', error);
    }
}
```

## 语言代码参考

### 支持的语言代码

| 语言 | 代码 | 语言 | 代码 |
|------|------|------|------|
| 中文(简体) | zh | 英语 | en |
| 中文(繁体) | zh-TW | 日语 | ja |
| 韩语 | ko | 法语 | fr |
| 德语 | de | 西班牙语 | es |
| 俄语 | ru | 意大利语 | it |
| 葡萄牙语 | pt | 阿拉伯语 | ar |
| 泰语 | th | 越南语 | vi |
| 土耳其语 | tr | 荷兰语 | nl |

## 服务提供商配置

### 翻译服务

| 服务商 | 代码 | 配置要求 |
|--------|------|----------|
| Google Translate | google | 无需配置 |
| Microsoft Translator | microsoft | API Key |
| DeepL | deepl | API Key |
| ChatGPT | chatgpt | OpenAI API Key |
| Azure AI | azure | Azure 订阅 |

### 语音合成服务

| 服务商 | 代码 | 配置要求 |
|--------|------|----------|
| Microsoft Edge TTS | edge-tts | 无需配置 |
| Google TTS | google-tts | 无需配置 |
| Azure AI TTS | azure-tts | Azure 订阅 |
| OpenAI TTS | openai-tts | OpenAI API Key |
| ElevenLabs | elevenlabs | API Key |

## 限制和注意事项

### 文件大小限制

- 单个视频文件: 最大 2GB
- 单个音频文件: 最大 500MB
- 批量处理: 最大 10 个文件

### 并发限制

- 同时处理任务数: 最大 3 个
- API 调用频率: 每分钟最大 100 次

### 支持的文件格式

**视频格式**:
- MP4, AVI, MOV, MKV, FLV, WMV, 3GP

**音频格式**:
- MP3, WAV, FLAC, AAC, OGG, M4A

**字幕格式**:
- SRT, VTT, ASS, SSA

## 更新日志

### v3.80 (当前版本)
- 新增批量处理 API
- 改进错误处理机制
- 优化性能和稳定性

### v3.70
- 新增系统信息 API
- 支持更多语音合成服务
- 修复已知问题

## 获取帮助

如果您在使用 API 时遇到问题：

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord 社区](https://discord.gg/y9gUweVCCJ)
- [官方文档](https://pyvideotrans.com)

---

更多示例和详细说明，请参考项目的 GitHub 仓库和官方文档。