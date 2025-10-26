# PyVideoTrans API Documentation

PyVideoTrans provides comprehensive API interfaces for programmatic access to all video translation features. This document details all available APIs.

## API Overview

### Basic Information

- **Version**: v3.80
- **Base Path**: `/api/v1`
- **Content Type**: `application/json`
- **Character Encoding**: UTF-8

### Authentication

Currently, the API is primarily for local use and does not require authentication. Future versions may add API Key authentication.

## Core APIs

### 1. Video Translation API

#### Start Translation Task

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

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `input_file` | string | Yes | Input video file path |
| `output_dir` | string | Yes | Output directory path |
| `source_language` | string | Yes | Source language code |
| `target_language` | string | Yes | Target language code |
| `model_name` | string | No | Speech recognition model name (default: small) |
| `translate_service` | string | No | Translation service provider (default: google) |
| `voice_service` | string | No | Text-to-speech service (default: edge-tts) |
| `voice_name` | string | No | Voice name |
| `subtitle_type` | string | No | Subtitle format (srt/vtt/ass) |
| `keep_background_music` | boolean | No | Whether to keep background music |
| `voice_rate` | integer | No | Voice speed adjustment (-50 to 50) |
| `voice_volume` | integer | No | Voice volume (0-100) |
| `background_music_volume` | integer | No | Background music volume (0-100) |

**Response Example**:

```json
{
  "success": true,
  "task_id": "task_123456789",
  "message": "Translation task started",
  "estimated_time": 300
}
```

#### Query Task Status

```http
GET /api/v1/task/{task_id}
```

**Response Example**:

```json
{
  "success": true,
  "task_id": "task_123456789",
  "status": "processing",
  "progress": 45,
  "current_step": "Speech Recognition",
  "estimated_remaining": 180,
  "output_files": []
}
```

**Status Values**:
- `pending`: Waiting
- `processing`: Processing
- `completed`: Completed
- `failed`: Failed
- `cancelled`: Cancelled

### 2. Speech Recognition API

#### Audio to Text

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

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `input_file` | string | Yes | Input audio/video file path |
| `model_name` | string | No | Recognition model name |
| `language` | string | No | Language code (auto for auto-detection) |
| `output_format` | string | No | Output format (srt/txt/json) |

**Response Example**:

```json
{
  "success": true,
  "task_id": "stt_123456789",
  "text": "Recognized text content",
  "subtitle_file": "path/to/output.srt",
  "segments": [
    {
      "start": 0.0,
      "end": 2.5,
      "text": "First segment text"
    }
  ]
}
```

### 3. Text Translation API

#### Translate Text

```http
POST /api/v1/translate-text
Content-Type: application/json

{
  "text": "Text to translate",
  "source_language": "zh",
  "target_language": "en",
  "service": "google"
}
```

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `text` | string | Yes | Text to translate |
| `source_language` | string | Yes | Source language code |
| `target_language` | string | Yes | Target language code |
| `service` | string | No | Translation service provider |

**Response Example**:

```json
{
  "success": true,
  "original_text": "Text to translate",
  "translated_text": "要翻译的文本",
  "source_language": "en",
  "target_language": "zh",
  "service": "google"
}
```

### 4. Text-to-Speech API

#### Text to Speech

```http
POST /api/v1/text-to-speech
Content-Type: application/json

{
  "text": "Text to synthesize",
  "language": "en",
  "voice_name": "en-US-AriaNeural",
  "service": "edge-tts",
  "rate": 0,
  "volume": 100,
  "output_file": "path/to/output.wav"
}
```

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `text` | string | Yes | Text to synthesize |
| `language` | string | Yes | Language code |
| `voice_name` | string | No | Voice name |
| `service` | string | No | TTS service provider |
| `rate` | integer | No | Speech rate adjustment (-50 to 50) |
| `volume` | integer | No | Volume (0-100) |
| `output_file` | string | No | Output file path |

**Response Example**:

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

### 5. System Information API

#### Get System Status

```http
GET /api/v1/system/status
```

**Response Example**:

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

#### Get Supported Languages

```http
GET /api/v1/system/languages
```

**Response Example**:

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

#### Get Available Models

```http
GET /api/v1/system/models
```

**Response Example**:

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

## Batch Processing API

### Batch Translation

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

### Batch Subtitle Generation

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

## Error Handling

### Error Response Format

```json
{
  "success": false,
  "error_code": "INVALID_FILE",
  "message": "The specified file does not exist or is inaccessible",
  "details": {
    "file": "path/to/missing.mp4",
    "timestamp": "2024-01-01T12:00:00Z"
  }
}
```

### Common Error Codes

| Error Code | HTTP Status | Description |
|------------|-------------|-------------|
| `INVALID_FILE` | 400 | File does not exist or format not supported |
| `INVALID_LANGUAGE` | 400 | Unsupported language code |
| `MODEL_NOT_FOUND` | 404 | Specified model not found |
| `INSUFFICIENT_MEMORY` | 500 | Insufficient memory |
| `PROCESSING_ERROR` | 500 | Error occurred during processing |
| `NETWORK_ERROR` | 503 | Network connection error |

## Usage Examples

### Python Example

```python
import requests
import json

class PyVideoTransAPI:
    def __init__(self, base_url="http://localhost:8080"):
        self.base_url = base_url
    
    def translate_video(self, input_file, output_dir, source_lang, target_lang):
        """Translate video"""
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
        """Get task status"""
        url = f"{self.base_url}/api/v1/task/{task_id}"
        response = requests.get(url)
        return response.json()
    
    def speech_to_text(self, audio_file, language="auto"):
        """Speech to text"""
        url = f"{self.base_url}/api/v1/speech-to-text"
        data = {
            "input_file": audio_file,
            "language": language,
            "output_format": "srt"
        }
        
        response = requests.post(url, json=data)
        return response.json()

# Usage example
api = PyVideoTransAPI()

# Start translation task
result = api.translate_video(
    input_file="example.mp4",
    output_dir="./output",
    source_lang="zh",
    target_lang="en"
)

if result["success"]:
    task_id = result["task_id"]
    print(f"Task started, ID: {task_id}")
    
    # Query task status
    status = api.get_task_status(task_id)
    print(f"Task status: {status['status']}")
```

### JavaScript Example

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

// Usage example
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
            console.log(`Task started, ID: ${result.task_id}`);
            
            // Poll task status
            const checkStatus = async () => {
                const status = await api.getTaskStatus(result.task_id);
                console.log(`Task status: ${status.status}`);
                
                if (status.status === 'processing') {
                    setTimeout(checkStatus, 5000); // Check again after 5 seconds
                }
            };
            
            checkStatus();
        }
    } catch (error) {
        console.error('API call failed:', error);
    }
}
```

## Language Code Reference

### Supported Language Codes

| Language | Code | Language | Code |
|----------|------|----------|------|
| Chinese (Simplified) | zh | English | en |
| Chinese (Traditional) | zh-TW | Japanese | ja |
| Korean | ko | French | fr |
| German | de | Spanish | es |
| Russian | ru | Italian | it |
| Portuguese | pt | Arabic | ar |
| Thai | th | Vietnamese | vi |
| Turkish | tr | Dutch | nl |

## Service Provider Configuration

### Translation Services

| Provider | Code | Configuration Required |
|----------|------|----------------------|
| Google Translate | google | None |
| Microsoft Translator | microsoft | API Key |
| DeepL | deepl | API Key |
| ChatGPT | chatgpt | OpenAI API Key |
| Azure AI | azure | Azure Subscription |

### Text-to-Speech Services

| Provider | Code | Configuration Required |
|----------|------|----------------------|
| Microsoft Edge TTS | edge-tts | None |
| Google TTS | google-tts | None |
| Azure AI TTS | azure-tts | Azure Subscription |
| OpenAI TTS | openai-tts | OpenAI API Key |
| ElevenLabs | elevenlabs | API Key |

## Limitations and Notes

### File Size Limits

- Single video file: Maximum 2GB
- Single audio file: Maximum 500MB
- Batch processing: Maximum 10 files

### Concurrency Limits

- Simultaneous processing tasks: Maximum 3
- API call frequency: Maximum 100 per minute

### Supported File Formats

**Video Formats**:
- MP4, AVI, MOV, MKV, FLV, WMV, 3GP

**Audio Formats**:
- MP3, WAV, FLAC, AAC, OGG, M4A

**Subtitle Formats**:
- SRT, VTT, ASS, SSA

## Changelog

### v3.80 (Current)
- Added batch processing API
- Improved error handling
- Optimized performance and stability

### v3.70
- Added system information API
- Support for more TTS services
- Fixed known issues

## Getting Help

If you encounter issues while using the API:

- [GitHub Issues](https://github.com/jianchang512/pyvideotrans/issues)
- [Discord Community](https://discord.gg/y9gUweVCCJ)
- [Official Documentation](https://pyvideotrans.com)

---

For more examples and detailed instructions, please refer to the project's GitHub repository and official documentation.