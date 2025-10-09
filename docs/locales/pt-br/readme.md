# PyVideoTrans - Ferramenta de Tradução e Dublagem de Vídeos

[中文](../../README.md) | [English](../en/readme.md) | [Español](../es/readme.md) | [Italiano](../it/readme.md)

PyVideoTrans é uma ferramenta de código aberto para tradução e dublagem de vídeos que fornece soluções de processamento de vídeo multilíngue de alta qualidade.

## ✨ Principais Recursos

- **🎯 Tradução com Um Clique**: Traduz automaticamente vídeos de um idioma para outro
- **🎙️ Clonagem de Voz**: Preserva as características do falante original no áudio traduzido
- **🎵 Preservação de Música de Fundo**: Separa inteligentemente vozes da música de fundo
- **📝 Geração de Legendas**: Gera legendas precisas em múltiplos formatos (SRT, VTT, ASS)
- **🌍 Mais de 30 Idiomas**: Suporte para mais de 30 idiomas para reconhecimento, tradução e síntese
- **🚀 Aceleração GPU**: Suporte de aceleração por hardware CUDA e MPS
- **📦 Processamento em Lote**: Processa múltiplos vídeos simultaneamente
- **🎨 Interface Amigável**: Interface gráfica intuitiva construída com PySide6

## 🎬 Vídeo de Demonstração

[![Demo do PyVideoTrans](https://img.youtube.com/vi/your-video-id/0.jpg)](https://www.youtube.com/watch?v=your-video-id)

## 🚀 Início Rápido

### Método 1: Baixar Pacote Pré-construído (Recomendado)

1. **Baixar**: Visite [Releases](https://github.com/jianchang512/pyvideotrans/releases) e baixe a versão mais recente para seu SO
2. **Extrair**: Descompacte o arquivo baixado
3. **Executar**: Execute `sp.exe` (Windows) ou `sp` (macOS/Linux)

### Método 2: Instalar do Código Fonte

#### Pré-requisitos

- Python 3.9-3.11
- FFmpeg
- Git

#### Passos de Instalação

```bash
# Clonar repositório
git clone https://github.com/jianchang512/pyvideotrans.git
cd pyvideotrans

# Criar ambiente virtual
python -m venv venv

# Ativar ambiente virtual
# Windows
.\venv\Scripts\activate
# macOS/Linux
source ./venv/bin/activate

# Instalar dependências
pip install -r requirements.txt

# Executar aplicação
python sp.py
```

## 📖 Guia do Usuário

### Fluxo de Trabalho Básico

1. **Selecionar Vídeo**: Escolha seu arquivo de vídeo de entrada
2. **Configurar Ajustes**: 
   - Idioma de origem (detecção automática disponível)
   - Idioma de destino
   - Serviço de tradução
   - Opções de síntese de voz
3. **Iniciar Processamento**: Clique em "Iniciar Tradução"
4. **Obter Resultados**: Encontre o vídeo traduzido no diretório de saída

### Recursos Avançados

#### Clonagem de Voz
- Habilite a clonagem de voz para manter as características do falante original
- Requer downloads de modelos adicionais
- Melhores resultados com áudio claro de um único falante

#### Preservação de Música de Fundo
- Separa automaticamente vozes da música de fundo
- Preserva a atmosfera de áudio original
- Níveis de volume ajustáveis para vozes e fundo

#### Personalização de Legendas
- Múltiplos formatos de legendas suportados
- Fonte, tamanho e posicionamento personalizáveis
- Opções de legendas bilíngues

## 🔧 Configuração

### Serviços de Tradução

PyVideoTrans suporta múltiplos serviços de tradução:

- **Google Translate** (Grátis, sem configuração necessária)
- **Microsoft Translator** (Requer chave API)
- **DeepL** (Requer chave API, alta qualidade)
- **ChatGPT** (Requer chave API do OpenAI)
- **Azure AI** (Requer assinatura do Azure)

### Serviços de Texto para Fala

- **Microsoft Edge TTS** (Grátis, mais de 200 vozes)
- **Azure AI TTS** (Requer assinatura, qualidade premium)
- **OpenAI TTS** (Requer chave API, vozes naturais)
- **ElevenLabs** (Requer chave API, clonagem de voz)

### Modelos de Reconhecimento de Fala

- **Faster Whisper** (Recomendado, processamento mais rápido)
- **OpenAI Whisper** (Alta precisão, mais lento)

## 🌍 Idiomas Suportados

PyVideoTrans suporta mais de 30 idiomas:

**Idiomas Principais**: Chinês (Simplificado/Tradicional), Inglês, Japonês, Coreano, Francês, Alemão, Espanhol, Russo, Árabe, etc.

**Lista Completa**: 
- 🇨🇳 Chinês (Simplificado/Tradicional)
- 🇺🇸 Inglês
- 🇯🇵 Japonês
- 🇰🇷 Coreano
- 🇫🇷 Francês
- 🇩🇪 Alemão
- 🇪🇸 Espanhol
- 🇷🇺 Russo
- 🇸🇦 Árabe
- 🇹🇷 Turco
- 🇮🇳 Hindi
- 🇺🇦 Ucraniano
- 🇰🇿 Cazaque
- 🇮🇩 Indonésio
- 🇲🇾 Malaio
- 🇨🇿 Tcheco
- 🇵🇱 Polonês
- 🇳🇱 Holandês
- 🇸🇪 Sueco
- E mais...

## 📋 Requisitos do Sistema

### Requisitos Mínimos
- **SO**: Windows 10/11, macOS 10.15+, Ubuntu 18.04+
- **RAM**: 4GB (8GB recomendado)
- **Armazenamento**: 2GB de espaço livre
- **Internet**: Necessário para serviços online

### Recomendado para Melhor Performance
- **RAM**: 16GB ou mais
- **GPU**: GPU NVIDIA com suporte CUDA ou Apple Silicon
- **Armazenamento**: SSD com 10GB+ de espaço livre

## 🛠️ Solução de Problemas

### Problemas Comuns

#### Problemas de Instalação
```bash
# Se pip install falhar, tente:
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir

# Para usuários Windows com erros SSL:
pip install --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host files.pythonhosted.org -r requirements.txt
```

#### FFmpeg Não Encontrado
- **Windows**: Baixe do [site oficial do FFmpeg](https://ffmpeg.org/download.html)
- **macOS**: `brew install ffmpeg`
- **Linux**: `sudo apt install ffmpeg` (Ubuntu/Debian)

#### Problemas de Aceleração GPU
- Certifique-se de que os drivers CUDA estejam instalados para GPUs NVIDIA
- Verifique a compatibilidade da GPU com PyTorch
- Verifique a disponibilidade de memória da GPU

### Otimização de Performance

#### Para Processamento Mais Rápido
- Use modelos Whisper menores (tiny, base, small)
- Habilite aceleração GPU
- Feche aplicações desnecessárias
- Use armazenamento SSD para arquivos temporários

#### Para Melhor Qualidade
- Use modelos Whisper maiores (medium, large)
- Escolha serviços de tradução premium (DeepL, ChatGPT)
- Use serviços TTS de alta qualidade (Azure, OpenAI)

## 🤝 Contribuindo

Damos as boas-vindas às contribuições! Por favor consulte nosso [Guia de Contribuição](../../contributing.md) para detalhes.

### Formas de Contribuir
- 🐛 Reportar bugs e problemas
- 💡 Sugerir novos recursos
- 📝 Melhorar documentação
- 🌍 Adicionar traduções
- 💻 Enviar melhorias de código

## 💰 Apoiar o Projeto

Se PyVideoTrans te ajuda, considere apoiar o projeto:

### Apoio Financeiro
- [Doação Ko-fi](https://ko-fi.com/jianchang512)
- WeChat Pay / Alipay (códigos QR no README principal)

### Outras Formas de Apoiar
- ⭐ Dar estrela ao projeto no GitHub
- 📢 Compartilhar com amigos e colegas
- 💬 Participar de nossas discussões da comunidade
- 📝 Escrever avaliações e tutoriais

## 📄 Licença

Este projeto está licenciado sob a [Licença GPL-3.0](https://github.com/jianchang512/pyvideotrans/blob/main/LICENSE).

## 🔗 Links

- **GitHub**: https://github.com/jianchang512/pyvideotrans
- **Site Oficial**: https://pyvideotrans.com
- **Comunidade Discord**: https://discord.gg/y9gUweVCCJ
- **Documentação**: [Guia do Usuário](../guides/user-guide.md)

## 📞 Contato

- **Email**: jianchang512@gmail.com
- **Discord**: https://discord.gg/y9gUweVCCJ
- **Issues**: https://github.com/jianchang512/pyvideotrans/issues

---

**Isenção de responsabilidade**: PyVideoTrans é fornecido "como está" para fins educacionais e de pesquisa. Por favor respeite os direitos autorais e de propriedade intelectual ao usar esta ferramenta.

Obrigado por escolher PyVideoTrans! Vamos quebrar as barreiras do idioma juntos! 🌍✨