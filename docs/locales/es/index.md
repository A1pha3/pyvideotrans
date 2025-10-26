# PyVideoTrans - Herramienta de Traducción y Doblaje de Videos

[中文](../../README.md) | [English](../en/index.md) | [Português](../pt-br/index.md) | [Italiano](../it/index.md)

PyVideoTrans es una herramienta de código abierto para traducción y doblaje de videos que proporciona soluciones de procesamiento de video multilingüe de alta calidad.

## ✨ Características Principales

- **🎯 Traducción con Un Clic**: Traduce automáticamente videos de un idioma a otro
- **🎙️ Clonación de Voz**: Preserva las características del hablante original en el audio traducido
- **🎵 Preservación de Música de Fondo**: Separa inteligentemente las voces de la música de fondo
- **📝 Generación de Subtítulos**: Genera subtítulos precisos en múltiples formatos (SRT, VTT, ASS)
- **🌍 Más de 30 Idiomas**: Soporte para más de 30 idiomas para reconocimiento, traducción y síntesis
- **🚀 Aceleración GPU**: Soporte de aceleración por hardware CUDA y MPS
- **📦 Procesamiento por Lotes**: Procesa múltiples videos simultáneamente
- **🎨 Interfaz Amigable**: Interfaz gráfica intuitiva construida con PySide6

## 🎬 Video de Demostración

[![Demo de PyVideoTrans](https://img.youtube.com/vi/your-video-id/0.jpg)](https://www.youtube.com/watch?v=your-video-id)

## 🚀 Inicio Rápido

### Método 1: Descargar Paquete Pre-construido (Recomendado)

1. **Descargar**: Visita [Releases](https://github.com/jianchang512/pyvideotrans/releases) y descarga la última versión para tu SO
2. **Extraer**: Descomprime el archivo descargado
3. **Ejecutar**: Ejecuta `sp.exe` (Windows) o `sp` (macOS/Linux)

### Método 2: Instalar desde el Código Fuente

#### Prerrequisitos

- Python 3.9-3.11
- FFmpeg
- Git

#### Pasos de Instalación

```bash
# Clonar repositorio
git clone https://github.com/jianchang512/pyvideotrans.git
cd pyvideotrans

# Crear entorno virtual
python -m venv venv

# Activar entorno virtual
# Windows
.\venv\Scripts\activate
# macOS/Linux
source ./venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar aplicación
python sp.py
```

## 📖 Guía del Usuario

### Flujo de Trabajo Básico

1. **Seleccionar Video**: Elige tu archivo de video de entrada
2. **Configurar Ajustes**: 
   - Idioma de origen (detección automática disponible)
   - Idioma de destino
   - Servicio de traducción
   - Opciones de síntesis de voz
3. **Iniciar Procesamiento**: Haz clic en "Iniciar Traducción"
4. **Obtener Resultados**: Encuentra el video traducido en el directorio de salida

### Características Avanzadas

#### Clonación de Voz
- Habilita la clonación de voz para mantener las características del hablante original
- Requiere descargas de modelos adicionales
- Mejores resultados con audio claro de un solo hablante

#### Preservación de Música de Fondo
- Separa automáticamente las voces de la música de fondo
- Preserva la atmósfera de audio original
- Niveles de volumen ajustables para voces y fondo

#### Personalización de Subtítulos
- Múltiples formatos de subtítulos soportados
- Fuente, tamaño y posicionamiento personalizables
- Opciones de subtítulos bilingües

## 🔧 Configuración

### Servicios de Traducción

PyVideoTrans soporta múltiples servicios de traducción:

- **Google Translate** (Gratis, sin configuración requerida)
- **Microsoft Translator** (Requiere clave API)
- **DeepL** (Requiere clave API, alta calidad)
- **ChatGPT** (Requiere clave API de OpenAI)
- **Azure AI** (Requiere suscripción de Azure)

### Servicios de Texto a Voz

- **Microsoft Edge TTS** (Gratis, más de 200 voces)
- **Azure AI TTS** (Requiere suscripción, calidad premium)
- **OpenAI TTS** (Requiere clave API, voces naturales)
- **ElevenLabs** (Requiere clave API, clonación de voz)

### Modelos de Reconocimiento de Voz

- **Faster Whisper** (Recomendado, procesamiento más rápido)
- **OpenAI Whisper** (Alta precisión, más lento)

## 🌍 Idiomas Soportados

PyVideoTrans soporta más de 30 idiomas:

**Idiomas Principales**: Chino (Simplificado/Tradicional), Inglés, Japonés, Coreano, Francés, Alemán, Español, Ruso, Árabe, etc.

**Lista Completa**: 
- 🇨🇳 Chino (Simplificado/Tradicional)
- 🇺🇸 Inglés
- 🇯🇵 Japonés
- 🇰🇷 Coreano
- 🇫🇷 Francés
- 🇩🇪 Alemán
- 🇪🇸 Español
- 🇷🇺 Ruso
- 🇸🇦 Árabe
- 🇹🇷 Turco
- 🇮🇳 Hindi
- 🇺🇦 Ucraniano
- 🇰🇿 Kazajo
- 🇮🇩 Indonesio
- 🇲🇾 Malayo
- 🇨🇿 Checo
- 🇵🇱 Polaco
- 🇳🇱 Holandés
- 🇸🇪 Sueco
- Y más...

## 📋 Requisitos del Sistema

### Requisitos Mínimos
- **SO**: Windows 10/11, macOS 10.15+, Ubuntu 18.04+
- **RAM**: 4GB (8GB recomendado)
- **Almacenamiento**: 2GB de espacio libre
- **Internet**: Requerido para servicios en línea

### Recomendado para Mejor Rendimiento
- **RAM**: 16GB o más
- **GPU**: GPU NVIDIA con soporte CUDA o Apple Silicon
- **Almacenamiento**: SSD con 10GB+ de espacio libre

## 🛠️ Solución de Problemas

### Problemas Comunes

#### Problemas de Instalación
```bash
# Si pip install falla, intenta:
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir

# Para usuarios de Windows con errores SSL:
pip install --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host files.pythonhosted.org -r requirements.txt
```

#### FFmpeg No Encontrado
- **Windows**: Descarga desde [sitio oficial de FFmpeg](https://ffmpeg.org/download.html)
- **macOS**: `brew install ffmpeg`
- **Linux**: `sudo apt install ffmpeg` (Ubuntu/Debian)

#### Problemas de Aceleración GPU
- Asegúrate de que los drivers CUDA estén instalados para GPUs NVIDIA
- Verifica la compatibilidad de GPU con PyTorch
- Verifica la disponibilidad de memoria GPU

### Optimización de Rendimiento

#### Para Procesamiento Más Rápido
- Usa modelos Whisper más pequeños (tiny, base, small)
- Habilita aceleración GPU
- Cierra aplicaciones innecesarias
- Usa almacenamiento SSD para archivos temporales

#### Para Mejor Calidad
- Usa modelos Whisper más grandes (medium, large)
- Elige servicios de traducción premium (DeepL, ChatGPT)
- Usa servicios TTS de alta calidad (Azure, OpenAI)

## 🤝 Contribuir

¡Damos la bienvenida a las contribuciones! Por favor consulta nuestra [Guía de Contribución](../../contributing.md) para más detalles.

### Formas de Contribuir
- 🐛 Reportar errores y problemas
- 💡 Sugerir nuevas características
- 📝 Mejorar documentación
- 🌍 Agregar traducciones
- 💻 Enviar mejoras de código

## 💰 Apoyar el Proyecto

Si PyVideoTrans te ayuda, considera apoyar el proyecto:

### Apoyo Financiero
- [Donación Ko-fi](https://ko-fi.com/jianchang512)
- WeChat Pay / Alipay (códigos QR en README principal)

### Otras Formas de Apoyar
- ⭐ Dar estrella al proyecto en GitHub
- 📢 Compartir con amigos y colegas
- 💬 Unirse a nuestras discusiones comunitarias
- 📝 Escribir reseñas y tutoriales

## 📄 Licencia

Este proyecto está licenciado bajo la [Licencia GPL-3.0](https://github.com/jianchang512/pyvideotrans/blob/main/LICENSE).

## 🔗 Enlaces

- **GitHub**: https://github.com/jianchang512/pyvideotrans
- **Sitio Web Oficial**: https://pyvideotrans.com
- **Comunidad Discord**: https://discord.gg/y9gUweVCCJ
- **Documentación**: [Guía del Usuario](../guides/user-guide.md)

## 📞 Contacto

- **Email**: jianchang512@gmail.com
- **Discord**: https://discord.gg/y9gUweVCCJ
- **Issues**: https://github.com/jianchang512/pyvideotrans/issues

---

**Descargo de responsabilidad**: PyVideoTrans se proporciona "tal como está" para fines educativos y de investigación. Por favor respeta los derechos de autor y propiedad intelectual al usar esta herramienta.

¡Gracias por elegir PyVideoTrans! ¡Rompamos las barreras del idioma juntos! 🌍✨