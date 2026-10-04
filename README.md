# pi-linux-voice

Linux voice input for [Pi](https://pi.dev). Record from your microphone with `ffmpeg`, transcribe with the free Groq API, and insert the text into Pi's editor.

## Requirements

- Linux
- Node.js 22+
- `ffmpeg`
- A working PulseAudio/PipeWire microphone, or ALSA
- A free [Groq API key](https://console.groq.com/keys)

Install `ffmpeg` on Debian/Ubuntu:

```bash
sudo apt install ffmpeg
```

## Install

```bash
pi install npm:pi-linux-voice
```

Or install directly from GitHub:

```bash
pi install git:github.com/YOUR_GITHUB_USERNAME/pi-linux-voice
```

Restart Pi after installing the package.

## Configure Groq

Set your API key before starting Pi:

```bash
export GROQ_API_KEY="gsk_..."
pi
```

To make it persistent, add the export to `~/.bashrc` or `~/.zshrc`.

The extension uses these Groq defaults:

- Endpoint: `https://api.groq.com/openai/v1/audio/transcriptions`
- Model: `whisper-large-v3-turbo`

### Groq free-tier limits

Groq limits depend on your account and the selected model. Limits can include
requests per minute/day and audio or token usage per minute/day. Daily limits
reset at **00:00 UTC**; per-minute limits recover after their one-minute
window. Check the current limits for your account at:

<https://console.groq.com/settings/limits>

## Use

- Press **Ctrl+Space** to start recording.
- Press **Ctrl+Space** again to stop and transcribe.
- Or use `/voice start`, `/voice stop`, and `/voice status`.

The transcription is inserted into Pi's editor.

## Configuration

Use ALSA instead of PulseAudio/PipeWire:

```bash
export PI_VOICE_INPUT=alsa
export PI_VOICE_DEVICE=default
```

Choose another microphone device:

```bash
export PI_VOICE_DEVICE="your-device-name"
```

Override the transcription endpoint or model:

```bash
export PI_VOICE_TRANSCRIBE_URL="https://api.groq.com/openai/v1/audio/transcriptions"
export PI_VOICE_TRANSCRIBE_MODEL="whisper-large-v3-turbo"
```

Enable ffmpeg diagnostics:

```bash
export PI_VOICE_DEBUG=1
```

## Security and privacy

Audio is recorded temporarily under the system temporary directory, uploaded to the configured transcription API, and deleted afterward. Do not commit `GROQ_API_KEY` or other secrets to your repository.

## Development

Run the package from a local checkout:

```bash
pi -e .
```

The extension is TypeScript and Pi loads it directly; no build step is required.

## License

MIT
