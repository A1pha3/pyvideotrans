# PyVideoTrans 本地 API 指南

PyVideoTrans 内置了一个基于 Flask 的本地 API 服务，允许你通过 HTTP 调用完成字幕翻译、语音识别、配音以及一键视频翻译等任务。本文档基于 `api.py` 的最新实现（默认端口 9011）进行说明。

## 快速开始

```bash
cd /Volumes/mini_matrix/github/factory/pyvideotrans
python api.py
```

默认情况下服务监听 `http://127.0.0.1:9011`。

- 如需修改监听地址或端口，可在项目根目录创建 `host.txt`，写入形如 `0.0.0.0:8080` 的值。
- 生成文件统一保存在 `<项目根目录>/apidata/<task_id>/`。
- 所有接口均返回 JSON，当前版本未启用鉴权。

## 通用约定

### 路径与资源

| 项 | 默认值 | 说明 |
| --- | --- | --- |
| 基础 URL | `http://<host>:<port>` | 无额外前缀（旧版文档中的 `/api/v1` 已废弃） |
| 静态资源 | `/apidata/<task_id>/<filename>` | 可直接通过浏览器下载生成文件 |
| 进度日志 | `/apidata/processinfo/<task_id>.json` | 供内部追踪使用 |

### 返回格式

```json
{
  "code": 0,
  "msg": "ok",
  "task_id": "06c238d250f0b51248563c405f1d7294"
}
```

通用字段说明：

| 字段 | 含义 |
| --- | --- |
| `code` | `0` 表示成功创建任务；`-1` 表示任务仍在队列或执行中；正整数表示错误（详见各接口说明） |
| `msg` | 提示信息、排队进度或错误原因 |
| `task_id` | 任务唯一标识。查询状态与下载结果时使用 |
| `data` | 仅在任务完成时返回，包含生成文件的绝对路径与可访问 URL |

### 任务查询结果

`/task_status` 在任务成功时返回：

```json
{
  "code": 0,
  "msg": "ok",
  "data": {
    "absolute_path": ["/abs/path/apidata/<task_id>/en.srt"],
    "url": ["http://127.0.0.1:9011/apidata/<task_id>/en.srt"]
  }
}
```

执行中：`{"code": -1, "msg": "正在合成声音"}`  \
不存在：`{"code": 1, "msg": "该任务 <task_id> 不存在"}`  \
失败：`{"code": 3, "msg": "错误信息"}`

### 输出目录结构

```
apidata/
├── <task_id>/            # 任务产出目录
│   ├── *.srt / *.m4a ...  # 生成文件
│   └── 文件说明.txt       # 任务摘要
└── processinfo/
    └── <task_id>.json    # 阶段日志
```

## 接口概览

| 接口 | 方法 | 说明 |
| --- | --- | --- |
| `/tts` | POST | 基于字幕生成配音音频 |
| `/translate_srt` | POST | 字幕翻译 |
| `/recogn` | POST | 语音识别（音/视频转文字、字幕） |
| `/trans_video` | POST | 完整视频翻译管线（识别 → 翻译 → 配音 → 合成） |
| `/task_status` | GET / POST | 查询单个任务状态与结果 |
| `/task_status_list` | POST | 批量查询任务状态 |

## `/tts`：字幕配音

- **功能**：将 `.srt` 字幕文件或原始字幕文本转换成指定 TTS 渠道的音频。
- **返回**：成功时 `code=0`，稍后通过 `/task_status` 获取结果音频与字幕。

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `name` | string | ✅ | 字幕路径（需与服务同机）或完整的 SRT 字符串 |
| `tts_type` | integer | ✅ | 语音渠道编号，见 [TTS 渠道对照表](#tts-渠道对照表) |
| `voice_role` | string | ✅ | 语音角色名称（各渠道枚举不同） |
| `target_language_code` | string | ✅ | 字幕语言代码（示例：`en`、`zh-cn`） |
| `voice_rate` | string | ❌ | 语速，`+0%`～`±50%` |
| `volume` | string | ❌ | 音量，`+0%`～`±50%`（Edge-TTS 专属） |
| `pitch` | string | ❌ | 音调，`+0Hz`～`±20Hz`（Edge-TTS 专属） |
| `out_ext` | string | ❌ | 输出音频格式，默认 `mp3`（支持 mp3/wav/flac/aac） |
| `voice_autorate` | boolean | ❌ | 自动调节语速以贴合字幕时轴 |

示例：

```json
POST /tts
{
  "name": "C:/videos/sample.srt",
  "tts_type": 0,
  "voice_role": "en-US-AriaNeural",
  "target_language_code": "en",
  "voice_rate": "+0%",
  "out_ext": "wav"
}
```

> 若传入的 `name` 字段包含换行，将视为 SRT 文本并写入临时文件。

## `/translate_srt`：字幕翻译

- **功能**：翻译字幕文件或字幕文本。
- **返回**：成功后 `code=0`，结果字幕文件通过 `/task_status` 下载。

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `name` | string | ✅ | SRT 文件路径或 SRT 字符串 |
| `translate_type` | integer | ✅ | 翻译渠道编号，见 [翻译渠道对照表](#翻译渠道对照表) |
| `target_language` | string | ✅ | 目标语言代码（如 `en`、`ja`） |
| `source_code` | string | ❌ | 源语言代码，可为空表示自动判定 |

示例：

```json
POST /translate_srt
{
  "name": "C:/videos/lecture.srt",
  "translate_type": 4,
  "target_language": "en"
}
```

## `/recogn`：语音识别

- **功能**：对音频/视频文件进行语音识别，生成字幕或文本。
- **返回**：成功后 `code=0`，识别结果在任务完成后提供。

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `name` | string | ✅ | 本地音频/视频绝对路径 |
| `recogn_type` | integer | ✅ | 识别模式编号，见 [语音识别模式表](#语音识别模式表) |
| `model_name` | string | ✅* | Whisper/Faster Whisper 等本地模型名称；云端模式可忽略 |
| `detect_language` | string | ✅ | 源语种代码（`auto` 仅在部分模式可用） |
| `split_type` | string | ❌ | `all`（整段）/`avg`（等长切片），默认 `all` |
| `is_cuda` | boolean | ❌ | 是否启用 CUDA/MPS 加速 |

示例：

```json
POST /recogn
{
  "name": "C:/videos/talk.mp4",
  "recogn_type": 0,
  "model_name": "large-v3",
  "detect_language": "ja",
  "is_cuda": true
}
```

## `/trans_video`：完整视频翻译

- **功能**：一站式完成识别 → 翻译 → 配音 → 合成，可选字幕嵌入、背景音乐保留等。
- **返回**：成功后 `code=0`，多种产物（混音视频、配音、字幕等）会生成在任务目录。

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `name` | string | ✅ | 待处理视频路径 |
| `recogn_type` | integer | ✅ | 语音识别模式编号 |
| `model_name` | string | ✅* | 本地模型名称（云端识别可忽略） |
| `split_type` | string | ❌ | 识别切分方式，默认 `all` |
| `is_cuda` | boolean | ❌ | 是否启用 GPU |
| `translate_type` | integer | ✅ | 翻译渠道编号 |
| `target_language` | string | ✅ | 目标语言代码 |
| `source_language` | string | ❌ | 源语言代码（默认与识别一致） |
| `tts_type` | integer | ✅ | 配音渠道编号 |
| `voice_role` | string | ✅ | 配音角色名称（`"no"` 表示不生成配音） |
| `voice_rate` | string | ❌ | 配音语速，默认 `+0%` |
| `voice_autorate` | boolean | ❌ | 自动语速对齐，默认 `false` |
| `video_autorate` | boolean | ❌ | 根据配音自动调节视频结尾时长 |
| `volume` | string | ❌ | 配音音量，默认 `+0%` |
| `pitch` | string | ❌ | 配音音调，默认 `+0Hz` |
| `subtitle_type` | integer | ❌ | 字幕嵌入策略：0 不嵌入、1 硬字幕、2 软字幕、3 双硬、4 双软 |
| `append_video` | boolean | ❌ | 配音比原视频长时是否自动延长结尾 |
| `back_audio` | string | ❌ | 自定义背景音乐路径 |
| `is_separate` | boolean | ❌ | 是否先执行人声/背景音分离 |
| `subtitles` | string | ❌ | 外部字幕内容（若已存在字幕，可跳过识别环节） |
| `only_video` | boolean | ❌ | 仅输出视频，不额外导出字幕/音频 |

示例（常规工作流）：

```json
POST /trans_video
{
  "name": "C:/videos/demo.mp4",
  "recogn_type": 0,
  "model_name": "small",
  "translate_type": 8,
  "source_language": "zh-cn",
  "target_language": "en",
  "tts_type": 0,
  "voice_role": "en-US-AriaNeural",
  "subtitle_type": 1,
  "voice_autorate": true,
  "is_cuda": true
}
```

> 当 `subtitles` 字段不为空时，服务将跳过语音识别阶段，直接使用提供的字幕。

## 任务状态接口

### `/task_status`

- **GET**：`/task_status?task_id=<uuid>`
- **POST**：`{"task_id": "<uuid>"}`

成功时返回 `code=0` 和 `data` 字段；执行中/失败/不存在的返回值见前文。

### `/task_status_list`

- **POST**：`{"task_id_list": ["id1", "id2"]}`
- 返回结构：`{"code": 0, "data": {"id1": {...}, "id2": {...}}}`

## TTS 渠道对照表

| 数值 | 渠道名称 | 说明 |
| --- | --- | --- |
| 0 | Edge-TTS(免费) | 微软 Edge 在线 TTS |
| 1 | CosyVoice(本地) | 本地 CosyVoice 服务 |
| 2 | ChatTTS(本地) | 本地 ChatTTS |
| 3 | 302.AI | 302.AI 在线语音 |
| 4 | FishTTS(本地) | 本地 FishTTS |
| 5 | Azure-TTS | Azure Speech Service |
| 6 | GPT-SoVITS(本地) | GPT-SoVITS 服务 |
| 7 | clone-voice(本地) | 自建 clone-voice |
| 8 | OpenAI TTS | OpenAI 文本转语音 |
| 9 | Elevenlabs.io | ElevenLabs 语音合成 |
| 10 | Google TTS | Google 在线 TTS |
| 11 | 自定义TTSAPI | 自定义 HTTP 接口 |
| 12 | 字节火山语音合成 | VolcEngine TTS |
| 13 | F5/Index/Spark/Dia TTS | 第三方综合接口 |
| 14 | kokoro-TTS(本地) | 本地 kokoro |
| 15 | Google Cloud TTS | Google Cloud Speech |
| 16 | Gemini TTS | Google Gemini 语音 |
| 17 | ChatterBox | ChatterBox 语音 |
| 18 | Qwen TTS | 通义千问 TTS |

部分渠道对语言有严格限制，调用前建议参考 GUI 中的提示或源码 `videotrans/tts/__init__.py`。

## 翻译渠道对照表

| 数值 | 渠道名称 | 类型 |
| --- | --- | --- |
| 0 | Google(免费) | 在线 |
| 1 | 微软(免费) | 在线 |
| 2 | MyMemory API(免费) | 在线 |
| 3 | 百度翻译 | 在线 |
| 4 | DeepL | 在线 |
| 5 | DeepLx | 自建/代理 |
| 6 | OTT(本地) | 本地 LLM |
| 7 | 腾讯翻译 | 在线 |
| 8 | OpenAI ChatGPT | 在线 |
| 9 | 兼容AI/本地模型 | 本地或自建接口 |
| 10 | 字节火山AI | 在线 |
| 11 | AzureGPT AI | 在线 |
| 12 | Gemini AI | 在线 |
| 13 | 自定义翻译API | 自定义 HTTP |
| 14 | 阿里百炼 | 在线 |
| 15 | Claude AI | 在线 |
| 16 | LibreTranslate(本地) | 本地 |
| 17 | 302.AI | 在线 |
| 18 | 阿里机器翻译 | 在线 |
| 19 | 智谱AI | 在线 |
| 20 | 硅基流动 | 在线 |
| 21 | DeepSeek | 在线 |
| 22 | OpenRouter | 在线 |

> 语言代码映射可参考 `videotrans/translator/__init__.py` 中的 `LANG_CODE` 和 `LANGNAME_DICT`。

## 语音识别模式表

| 数值 | 模式名称 | 说明 |
| --- | --- | --- |
| 0 | faster-whisper(本地) | Faster-Whisper 本地推理 |
| 1 | openai-whisper(本地) | OpenAI Whisper 本地模型 |
| 2 | 阿里FunASR中文(本地) | FunASR 离线模型（部分模型仅支援中文/日韩） |
| 3 | STT语音识别(本地) | 本地自定义 STT API |
| 4 | 字节火山字幕生成 | VolcEngine 识别 |
| 5 | Deepgram.com | Deepgram 语音识别 |
| 6 | OpenAI语音识别 | OpenAI Speech-To-Text |
| 7 | 自定义识别API | 自定义 HTTP |
| 8 | Google识别API(免费) | Google Speech |
| 9 | Gemini大模型识别 | Google Gemini |
| 10 | Faster-Whisper-XXL.exe | Windows 专用加速版 |
| 11 | 302.AI | 302.AI 语音识别 |
| 12 | ElevenLabs.io | ElevenLabs 语音识别 |
| 13 | Parakeet-tdt | 阿里 Parakeet |
| 14 | 阿里百炼 Qwen3-ASR | Ali Qwen3 ASR |

各模式对语言、API Key 等有不同要求，请参考源码 `videotrans/recognition/__init__.py` 中的 `is_allow_lang` 与 `is_input_api` 逻辑。

## 错误代码与排查

| `code` | 场景 | 排查建议 |
| --- | --- | --- |
| 1 | 缺少或非法参数 | 核对请求字段与路径是否可访问 |
| 3 | 任务执行失败 | 查看 `apidata/processinfo/<task_id>.json` 中的 `text` 字段 |
| 4 | 语言不受支持 | 检查 `target_language`/`target_language_code` 与指定渠道的支持范围 |
| 5 | 渠道未配置 | 在 GUI 中补充对应 API Key / URL |
| -1 | 任务排队/执行中 | 使用 `msg` 了解当前阶段或排队顺序 |

## Python 调用示例

```python
import requests

BASE_URL = "http://127.0.0.1:9011"

def submit_job():
    payload = {
        "name": "C:/videos/demo.mp4",
        "recogn_type": 0,
        "model_name": "small",
        "translate_type": 8,
        "source_language": "zh-cn",
        "target_language": "en",
        "tts_type": 0,
        "voice_role": "en-US-AriaNeural"
    }
    res = requests.post(f"{BASE_URL}/trans_video", json=payload, timeout=30)
    res.raise_for_status()
    return res.json()["task_id"]

def wait_task(task_id):
    while True:
        data = requests.get(f"{BASE_URL}/task_status", params={"task_id": task_id}, timeout=15).json()
        if data["code"] == 0:
            print("任务完成", data["data"]["url"])
            break
        if data["code"] > 0:
            raise RuntimeError(data["msg"])
        print("进度:", data["msg"])

if __name__ == "__main__":
    tid = submit_job()
    wait_task(tid)
```

## 常见问题

1. **任务目录为空？**
   - 通常表示处理过程中断或失败。请检查 `/task_status` 返回的错误信息以及日志文件。
2. **语言或渠道提示不支持？**
   - 参考各渠道 `is_allow_lang` 定义，确保目标语言在支持列表内。
3. **性能问题？**
   - 对于本地模型，合理选择模型大小并开启 GPU；外部 API 需关注并发与速率限制。

---

建议在调用前同步查阅 GUI 中的配置说明或阅读相关源码，以确保参数与能力对齐。English reference will be updated同时，请关注 `docs/api/api.en.md` 的后续更新。
