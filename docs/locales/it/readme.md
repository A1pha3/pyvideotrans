# PyVideoTrans - Strumento di Traduzione e Doppiaggio Video

[中文](../../README.md) | [English](../en/readme.md) | [Español](../es/readme.md) | [Português](../pt-br/readme.md)

PyVideoTrans è uno strumento open-source per la traduzione e il doppiaggio di video che fornisce soluzioni di elaborazione video multilingue di alta qualità.

## ✨ Caratteristiche Principali

- **🎯 Traduzione con Un Clic**: Traduce automaticamente video da una lingua all'altra
- **🎙️ Clonazione Vocale**: Preserva le caratteristiche del parlante originale nell'audio tradotto
- **🎵 Preservazione Musica di Sottofondo**: Separa intelligentemente le voci dalla musica di sottofondo
- **📝 Generazione Sottotitoli**: Genera sottotitoli accurati in formati multipli (SRT, VTT, ASS)
- **🌍 Oltre 30 Lingue**: Supporto per oltre 30 lingue per riconoscimento, traduzione e sintesi
- **🚀 Accelerazione GPU**: Supporto accelerazione hardware CUDA e MPS
- **📦 Elaborazione Batch**: Elabora più video simultaneamente
- **🎨 Interfaccia User-Friendly**: Interfaccia grafica intuitiva costruita con PySide6

## 🎬 Video Dimostrativo

[![Demo PyVideoTrans](https://img.youtube.com/vi/your-video-id/0.jpg)](https://www.youtube.com/watch?v=your-video-id)

## 🚀 Avvio Rapido

### Metodo 1: Scarica Pacchetto Pre-costruito (Raccomandato)

1. **Scarica**: Visita [Releases](https://github.com/jianchang512/pyvideotrans/releases) e scarica l'ultima versione per il tuo OS
2. **Estrai**: Decomprimi il file scaricato
3. **Esegui**: Esegui `sp.exe` (Windows) o `sp` (macOS/Linux)

### Metodo 2: Installa dal Codice Sorgente

#### Prerequisiti

- Python 3.9-3.11
- FFmpeg
- Git

#### Passaggi di Installazione

```bash
# Clona repository
git clone https://github.com/jianchang512/pyvideotrans.git
cd pyvideotrans

# Crea ambiente virtuale
python -m venv venv

# Attiva ambiente virtuale
# Windows
.\venv\Scripts\activate
# macOS/Linux
source ./venv/bin/activate

# Installa dipendenze
pip install -r requirements.txt

# Esegui applicazione
python sp.py
```

## 📖 Guida Utente

### Flusso di Lavoro Base

1. **Seleziona Video**: Scegli il tuo file video di input
2. **Configura Impostazioni**: 
   - Lingua sorgente (rilevamento automatico disponibile)
   - Lingua di destinazione
   - Servizio di traduzione
   - Opzioni sintesi vocale
3. **Avvia Elaborazione**: Clicca "Inizia Traduzione"
4. **Ottieni Risultati**: Trova il video tradotto nella directory di output

### Caratteristiche Avanzate

#### Clonazione Vocale
- Abilita la clonazione vocale per mantenere le caratteristiche del parlante originale
- Richiede download di modelli aggiuntivi
- Migliori risultati con audio chiaro di un singolo parlante

#### Preservazione Musica di Sottofondo
- Separa automaticamente le voci dalla musica di sottofondo
- Preserva l'atmosfera audio originale
- Livelli di volume regolabili per voci e sottofondo

#### Personalizzazione Sottotitoli
- Formati multipli di sottotitoli supportati
- Font, dimensione e posizionamento personalizzabili
- Opzioni sottotitoli bilingui

## 🔧 Configurazione

### Servizi di Traduzione

PyVideoTrans supporta servizi di traduzione multipli:

- **Google Translate** (Gratuito, nessuna configurazione richiesta)
- **Microsoft Translator** (Richiede chiave API)
- **DeepL** (Richiede chiave API, alta qualità)
- **ChatGPT** (Richiede chiave API OpenAI)
- **Azure AI** (Richiede sottoscrizione Azure)

### Servizi Text-to-Speech

- **Microsoft Edge TTS** (Gratuito, oltre 200 voci)
- **Azure AI TTS** (Richiede sottoscrizione, qualità premium)
- **OpenAI TTS** (Richiede chiave API, voci naturali)
- **ElevenLabs** (Richiede chiave API, clonazione vocale)

### Modelli Riconoscimento Vocale

- **Faster Whisper** (Raccomandato, elaborazione più veloce)
- **OpenAI Whisper** (Alta accuratezza, più lento)

## 🌍 Lingue Supportate

PyVideoTrans supporta oltre 30 lingue:

**Lingue Principali**: Cinese (Semplificato/Tradizionale), Inglese, Giapponese, Coreano, Francese, Tedesco, Spagnolo, Russo, Arabo, ecc.

**Lista Completa**: 
- 🇨🇳 Cinese (Semplificato/Tradizionale)
- 🇺🇸 Inglese
- 🇯🇵 Giapponese
- 🇰🇷 Coreano
- 🇫🇷 Francese
- 🇩🇪 Tedesco
- 🇪🇸 Spagnolo
- 🇷🇺 Russo
- 🇸🇦 Arabo
- 🇹🇷 Turco
- 🇮🇳 Hindi
- 🇺🇦 Ucraino
- 🇰🇿 Kazako
- 🇮🇩 Indonesiano
- 🇲🇾 Malese
- 🇨🇿 Ceco
- 🇵🇱 Polacco
- 🇳🇱 Olandese
- 🇸🇪 Svedese
- E altro...

## 📋 Requisiti di Sistema

### Requisiti Minimi
- **OS**: Windows 10/11, macOS 10.15+, Ubuntu 18.04+
- **RAM**: 4GB (8GB raccomandato)
- **Storage**: 2GB spazio libero
- **Internet**: Richiesto per servizi online

### Raccomandato per Migliori Prestazioni
- **RAM**: 16GB o più
- **GPU**: GPU NVIDIA con supporto CUDA o Apple Silicon
- **Storage**: SSD con 10GB+ spazio libero

## 🛠️ Risoluzione Problemi

### Problemi Comuni

#### Problemi di Installazione
```bash
# Se pip install fallisce, prova:
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir

# Per utenti Windows con errori SSL:
pip install --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host files.pythonhosted.org -r requirements.txt
```

#### FFmpeg Non Trovato
- **Windows**: Scarica dal [sito ufficiale FFmpeg](https://ffmpeg.org/download.html)
- **macOS**: `brew install ffmpeg`
- **Linux**: `sudo apt install ffmpeg` (Ubuntu/Debian)

#### Problemi Accelerazione GPU
- Assicurati che i driver CUDA siano installati per GPU NVIDIA
- Verifica compatibilità GPU con PyTorch
- Verifica disponibilità memoria GPU

### Ottimizzazione Prestazioni

#### Per Elaborazione Più Veloce
- Usa modelli Whisper più piccoli (tiny, base, small)
- Abilita accelerazione GPU
- Chiudi applicazioni non necessarie
- Usa storage SSD per file temporanei

#### Per Migliore Qualità
- Usa modelli Whisper più grandi (medium, large)
- Scegli servizi di traduzione premium (DeepL, ChatGPT)
- Usa servizi TTS di alta qualità (Azure, OpenAI)

## 🤝 Contribuire

Accogliamo contributi! Per favore consulta la nostra [Guida Contribuzione](../../contributing.md) per dettagli.

### Modi per Contribuire
- 🐛 Segnalare bug e problemi
- 💡 Suggerire nuove caratteristiche
- 📝 Migliorare documentazione
- 🌍 Aggiungere traduzioni
- 💻 Inviare miglioramenti codice

## 💰 Supporta il Progetto

Se PyVideoTrans ti aiuta, considera di supportare il progetto:

### Supporto Finanziario
- [Donazione Ko-fi](https://ko-fi.com/jianchang512)
- WeChat Pay / Alipay (codici QR nel README principale)

### Altri Modi per Supportare
- ⭐ Metti stella al progetto su GitHub
- 📢 Condividi con amici e colleghi
- 💬 Partecipa alle nostre discussioni della comunità
- 📝 Scrivi recensioni e tutorial

## 📄 Licenza

Questo progetto è licenziato sotto la [Licenza GPL-3.0](https://github.com/jianchang512/pyvideotrans/blob/main/LICENSE).

## 🔗 Collegamenti

- **GitHub**: https://github.com/jianchang512/pyvideotrans
- **Sito Web Ufficiale**: https://pyvideotrans.com
- **Comunità Discord**: https://discord.gg/y9gUweVCCJ
- **Documentazione**: [Guida Utente](../guides/user-guide.md)

## 📞 Contatto

- **Email**: jianchang512@gmail.com
- **Discord**: https://discord.gg/y9gUweVCCJ
- **Issues**: https://github.com/jianchang512/pyvideotrans/issues

---

**Disclaimer**: PyVideoTrans è fornito "così com'è" per scopi educativi e di ricerca. Per favore rispetta i diritti d'autore e di proprietà intellettuale quando usi questo strumento.

Grazie per aver scelto PyVideoTrans! Abbattiamo insieme le barriere linguistiche! 🌍✨