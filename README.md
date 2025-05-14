# Video-Audio-Transcription-With-Whisper

Transcribe video/audio files using OpenAI Whisper or faster-whisper.

## Features
- Supports both video and audio input files
- Choose between OpenAI Whisper and faster-whisper backends
- Device selection: CPU, CUDA (NVIDIA GPU), and MPS (Apple Silicon)
- Automatic audio extraction from video
- Optional timestamps in transcript
- Progress reporting and verbose mode

## Requirements
- Python 3.8+
- [PyTorch](https://pytorch.org/) (tested with 2.7.0)
- [openai-whisper](https://github.com/openai/whisper) (tested with 20240930)
- [faster-whisper](https://github.com/SYSTRAN/faster-whisper) (optional)
- ffmpeg (for audio extraction)

## Device Compatibility Notes
- **CPU:** Fully supported for both OpenAI Whisper and faster-whisper.
- **CUDA:** Supported for NVIDIA GPUs (not available on Apple Silicon).
- **MPS (Apple Silicon):**
  - **Not supported for OpenAI Whisper in this setup.** PyTorch MPS backend is detected as available, but OpenAI Whisper currently fails to run on MPS with recent versions (PyTorch 2.7.0, Whisper 20240930). You may see only backend fallback logs and no explicit error.
  - If you attempt to use MPS and encounter issues, use `--device cpu` for reliable transcription.
  - MPS support may improve in future releases of PyTorch or Whisper. Check their official documentation for updates.

## Usage

```bash
# Transcribe a video file using OpenAI Whisper on CPU
python transcribe.py input.mp4 -v --backend openai-whisper --device cpu

# Transcribe an audio file using faster-whisper on CPU
python transcribe.py input.mp3 -v --backend faster-whisper --device cpu

# Attempt to use MPS (Apple Silicon) [NOT SUPPORTED for OpenAI Whisper]
python transcribe.py input.mp4 -v --backend openai-whisper --device mps
# If you see only backend fallback logs and no transcript, use CPU instead.
```

## Troubleshooting
- If you encounter errors or fallback logs when using MPS, switch to CPU.
- Ensure your PyTorch and Whisper versions are compatible with your hardware.
- For the latest device support, consult:
  - [PyTorch MPS documentation](https://pytorch.org/docs/stable/notes/mps.html)
  - [OpenAI Whisper GitHub](https://github.com/openai/whisper)

## License
MIT
