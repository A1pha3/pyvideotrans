# PyVideoTrans - Video Translation and Dubbing Tool

[中文](../../readme.md) | [Español](../es/readme.md) | [Português](../pt-br/readme.md) | [Italiano](../it/readme.md)

PyVideoTrans is an open-source video translation and dubbing tool that provides high-quality multilingual video processing solutions.

## ✨ Key Features

- **🎯 One-Click Translation**: Automatically translate videos from one language to another
- **🎙️ Voice Cloning**: Preserve original speaker characteristics in translated audio
- **🎵 Background Music Preservation**: Intelligently separate vocals and background music
- **📝 Subtitle Generation**: Generate accurate subtitles in multiple formats (SRT, VTT, ASS)
- **🌍 30+ Languages**: Support for over 30 languages for recognition, translation, and synthesis
- **🚀 GPU Acceleration**: CUDA and MPS hardware acceleration support
- **📦 Batch Processing**: Process multiple videos simultaneously
- **🎨 User-Friendly Interface**: Intuitive graphical interface built with PySide6

## 🎬 Demo Video

[![PyVideoTrans Demo](https://img.youtube.com/vi/your-video-id/0.jpg)](https://www.youtube.com/watch?v=your-video-id)

## 🚀 Quick Start

### Method 1: Download Pre-built Package (Recommended)

1. **Download**: Visit [Releases](https://github.com/jianchang512/pyvideotrans/releases) and download the latest version for your OS
2. **Extract**: Unzip the downloaded file
3. **Run**: Execute `sp.exe` (Windows) or `sp` (macOS/Linux)

### Method 2: Install from Source

#### Prerequisites

- Python 3.9-3.11
- FFmpeg
- Git

#### Installation Steps

```bash
# Clone repository
git clone https://github.com/jianchang512/pyvideotrans.git
cd pyvideotrans

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows
.\venv\Scripts\activate
# macOS/Linux
source ./venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run application
python sp.py
```

## 📖 User Guide

### Basic Workflow

1. **Select Video**: Choose your input video file
2. **Configure Settings**: 
   - Source language (auto-detection available)
   - Target language
   - Translation service
   - Voice synthesis options
3. **Start Processing**: Click "Start Translation"
4. **Get Results**: Find translated video in output directory

### Advanced Features

#### Voice Cloning
- Enable voice cloning to maintain original speaker characteristics
- Requires additional model downloads
- Best results with clear, single-speaker audio

#### Background Music Preservation
- Automatically separates vocals from background music
- Preserves original audio atmosphere
- Adjustable volume levels for vocals and background

#### Subtitle Customization
- Multiple subtitle formats supported
- Customizable font, size, and positioning
- Bilingual subtitle options

## 🔧 Configuration

### Translation Services

PyVideoTrans supports multiple translation services:

- **Google Translate** (Free, no setup required)
- **Microsoft Translator** (Requires API key)
- **DeepL** (Requires API key, high quality)
- **ChatGPT** (Requires OpenAI API key)
- **Azure AI** (Requires Azure subscription)

### Text-to-Speech Services

- **Microsoft Edge TTS** (Free, 200+ voices)
- **Azure AI TTS** (Requires subscription, premium quality)
- **OpenAI TTS** (Requires API key, natural voices)
- **ElevenLabs** (Requires API key, voice cloning)

### Speech Recognition Models

- **Faster Whisper** (Recommended, faster processing)
- **OpenAI Whisper** (High accuracy, slower)

## 🌍 Supported Languages

PyVideoTrans supports over 30 languages:

**Major Languages**: Chinese (Simplified/Traditional), English, Japanese, Korean, French, German, Spanish, Russian, Arabic, etc.

**Complete List**: 
- 🇨🇳 Chinese (Simplified/Traditional)
- 🇺🇸 English
- 🇯🇵 Japanese
- 🇰🇷 Korean
- 🇫🇷 French
- 🇩🇪 German
- 🇪🇸 Spanish
- 🇷🇺 Russian
- 🇸🇦 Arabic
- 🇹🇷 Turkish
- 🇮🇳 Hindi
- 🇺🇦 Ukrainian
- 🇰🇿 Kazakh
- 🇮🇩 Indonesian
- 🇲🇾 Malay
- 🇨🇿 Czech
- 🇵🇱 Polish
- 🇳🇱 Dutch
- 🇸🇪 Swedish
- And more...

## 📋 System Requirements

### Minimum Requirements
- **OS**: Windows 10/11, macOS 10.15+, Ubuntu 18.04+
- **RAM**: 4GB (8GB recommended)
- **Storage**: 2GB free space
- **Internet**: Required for online services

### Recommended for Best Performance
- **RAM**: 16GB or more
- **GPU**: NVIDIA GPU with CUDA support or Apple Silicon
- **Storage**: SSD with 10GB+ free space

## 🛠️ Troubleshooting

### Common Issues

#### Installation Problems
```bash
# If pip install fails, try:
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir

# For Windows users with SSL errors:
pip install --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host files.pythonhosted.org -r requirements.txt
```

#### FFmpeg Not Found
- **Windows**: Download from [FFmpeg official site](https://ffmpeg.org/download.html)
- **macOS**: `brew install ffmpeg`
- **Linux**: `sudo apt install ffmpeg` (Ubuntu/Debian)

#### GPU Acceleration Issues
- Ensure CUDA drivers are installed for NVIDIA GPUs
- Check GPU compatibility with PyTorch
- Verify GPU memory availability

#### Model Download Issues
- Check internet connection
- Try using VPN if downloads fail
- Manually download models if automatic download fails

### Performance Optimization

#### For Faster Processing
- Use smaller Whisper models (tiny, base, small)
- Enable GPU acceleration
- Close unnecessary applications
- Use SSD storage for temporary files

#### For Better Quality
- Use larger Whisper models (medium, large)
- Choose premium translation services (DeepL, ChatGPT)
- Use high-quality TTS services (Azure, OpenAI)

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](../../contributing.md) for details.

### Ways to Contribute
- 🐛 Report bugs and issues
- 💡 Suggest new features
- 📝 Improve documentation
- 🌍 Add translations
- 💻 Submit code improvements

## 💰 Support the Project

If PyVideoTrans helps you, consider supporting the project:

### Financial Support
- [Ko-fi Donation](https://ko-fi.com/jianchang512)
- WeChat Pay / Alipay (QR codes in main README)

### Other Ways to Support
- ⭐ Star the project on GitHub
- 📢 Share with friends and colleagues
- 💬 Join our community discussions
- 📝 Write reviews and tutorials

## 📄 License

This project is licensed under the [GPL-3.0 License](https://github.com/jianchang512/pyvideotrans/blob/main/LICENSE).

## 🔗 Links

- **GitHub**: https://github.com/jianchang512/pyvideotrans
- **Official Website**: https://pyvideotrans.com
- **Discord Community**: https://discord.gg/y9gUweVCCJ
- **Documentation**: [User Guide](../guides/user-guide.md)

## 📞 Contact

- **Email**: jianchang512@gmail.com
- **Discord**: https://discord.gg/y9gUweVCCJ
- **Issues**: https://github.com/jianchang512/pyvideotrans/issues

---

**Disclaimer**: PyVideoTrans is provided "as is" for educational and research purposes. Please respect copyright and intellectual property rights when using this tool.

Thank you for choosing PyVideoTrans! Let's break down language barriers together! 🌍✨