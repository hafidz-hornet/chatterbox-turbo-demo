---
title: Chatterbox Turbo Demo
emoji: ⚡
colorFrom: blue
colorTo: purple
sdk: gradio
sdk_version: 6.0.2
app_file: app.py
pinned: false
license: mit
short_description: Text-to-Speech with Chatterbox Turbo - Natural voice synthesis with emotional expressions
---

# ⚡ Chatterbox Turbo Demo

A high-quality Text-to-Speech (TTS) demo powered by **Chatterbox Turbo** from ResembleAI. This application provides natural voice synthesis with support for emotional expressions and event tags like laughter, coughs, sighs, and more.

## Features

- **Natural Voice Synthesis**: Generate high-quality speech from text using advanced neural TTS models
- **Emotional Expressions**: Insert event tags like `[chuckle]`, `[sigh]`, `[cough]`, `[laugh]` for more expressive speech
- **Voice Cloning**: Upload reference audio or record your voice to clone speaking style
- **Advanced Controls**: Fine-tune generation with temperature, top-p, top-k, and other sampling parameters
- **Loudness Normalization**: Automatic audio normalization to -27 LUFS
- **GPU Acceleration**: Optimized for CUDA GPUs with support for CPU and Apple Silicon (MPS)

## Technology Stack

- **T3 Model**: Text-to-speech token generation using transformer architecture
- **S3Gen**: High-quality audio generation with flow matching
- **Voice Encoder**: Speaker embedding extraction for voice cloning
- **Gradio**: Interactive web interface
- **PyTorch**: Deep learning framework
- **Perth Watermarking**: Audio watermarking for provenance tracking

## Installation

### Prerequisites

- Python 3.10+ (3.12 recommended)
- CUDA-capable GPU (optional, but recommended for faster generation)
- Hugging Face account and token

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd chatterbox-turbo-demo
   ```

2. **Create virtual environment**
   ```bash
   python -m venv env
   
   # Windows
   .\env\Scripts\Activate.ps1
   
   # Linux/Mac
   source env/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   
   Copy `.env.example` to `.env` (or create `.env`) and add your Hugging Face token:
   ```
   HF_TOKEN=your_huggingface_token_here
   ```
   
   Get your token from: https://huggingface.co/settings/tokens

5. **Run the application**
   ```bash
   python app.py
   ```

   The Gradio interface will launch at `http://127.0.0.1:7860`

## Usage

### Basic Text-to-Speech

1. Enter your text in the text box (max 300 characters)
2. Upload a reference audio file or use the default voice
3. Click "Generate ⚡" to synthesize speech
4. Download or play the generated audio

### Adding Emotional Expressions

Click on any event tag button to insert it into your text:
- `[clear throat]` - Throat clearing sound
- `[sigh]` - Sighing sound
- `[shush]` - Shushing sound
- `[cough]` - Coughing sound
- `[groan]` - Groaning sound
- `[sniff]` - Sniffing sound
- `[gasp]` - Gasping sound
- `[chuckle]` - Light laughter
- `[laugh]` - Full laughter

**Example:**
```
Oh, that's hilarious! [chuckle] Um anyway, we do have a new model in store.
```

### Advanced Options

- **Random Seed**: Set to 0 for random generation, or use a specific number for reproducible results
- **Temperature** (0.05-2.0): Controls randomness (higher = more creative, lower = more consistent)
- **Top P** (0.0-1.0): Nucleus sampling threshold
- **Top K** (0-1000): Limits vocabulary to top K tokens
- **Repetition Penalty** (1.0-2.0): Reduces repetitive speech patterns
- **Min P** (0.0-1.0): Minimum probability threshold (0 to disable)
- **Normalize Loudness**: Enable/disable automatic loudness normalization

## Project Structure

```
chatterbox-turbo-demo/
├── app.py                      # Main Gradio application
├── requirements.txt            # Python dependencies
├── .env                        # Environment variables (create this)
├── README.md                   # This file
└── chatterbox/
    ├── __init__.py
    ├── tts_turbo.py           # Main TTS class
    ├── tts.py                 # Standard TTS implementation
    ├── mtl_tts.py             # Multi-task learning TTS
    ├── vc.py                  # Voice conversion utilities
    └── models/
        ├── t3/                # Text-to-token model
        ├── s3gen/             # Speech generation model
        ├── s3tokenizer/       # Speech tokenizer
        ├── tokenizers/        # Text tokenizers
        └── voice_encoder/     # Speaker embedding model
```

## Models

This project uses the following models from **ResembleAI/chatterbox-turbo**:
- `t3_turbo_v1.safetensors` - Text-to-token transformer model
- `s3gen_meanflow.safetensors` - Flow-based speech generator
- `ve.safetensors` - Voice encoder for speaker embeddings
- `conds.pt` - Pre-built voice conditionals

Models are automatically downloaded from Hugging Face on first run.

## Troubleshooting

### Token Error
```
LocalTokenNotFoundError: Token is required
```
**Solution**: Set your HF_TOKEN in `.env` file or run:
```bash
huggingface-cli login
```

### NumPy Build Error (Python 3.12)
```
ModuleNotFoundError: No module named 'distutils'
```
**Solution**: The requirements.txt has been updated to use numpy>=1.24.0 which supports Python 3.12

### CUDA Out of Memory
**Solution**: Use CPU mode by changing device to "cpu" in app.py, or reduce batch processing

### Import Error: spaces
**Solution**: Install the spaces package:
```bash
pip install spaces
```

## Requirements

Key dependencies:
- numpy>=1.24.0
- torch==2.6.0
- torchaudio==2.6.0
- transformers==4.46.3
- gradio==5.44.1
- librosa==0.11.0
- safetensors==0.5.3
- resemble-perth==1.0.1 (audio watermarking)
- pyloudnorm (audio normalization)
- spaces (Hugging Face GPU management)

See `requirements.txt` for complete list.

## License

MIT License

## Credits

- **ResembleAI** for the Chatterbox Turbo model
- Built with Gradio, PyTorch, and Hugging Face Transformers

## Links

- Model Repository: https://huggingface.co/ResembleAI/chatterbox-turbo
- Hugging Face Spaces Config: https://huggingface.co/docs/hub/spaces-config-reference