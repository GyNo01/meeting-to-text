# Agent Handoff: meeting-to-text

This package contains a Codex/OpenClaw-style skill for converting local audio or video files into speaker-separated text transcripts.

## What Changed

- `skills/meeting-to-text/scripts/meeting_to_text.py` now transcribes the full normalized audio timeline, then maps each transcript chunk to the best matching diarized speaker.
- Output speaker labels are normal UTF-8 Chinese labels such as `说话人1`.
- FFmpeg decoding supports a broader set of common audio and video containers.
- `skills/meeting-to-text/SKILL.md` documents the updated behavior and result fields.

## Skill Entry

Use:

```powershell
python skills/meeting-to-text/scripts/meeting_to_text.py --input "<SOURCE_PATH>" --output "<OUTPUT_TARGET>"
```

Optional:

```powershell
--work-dir "<TEMP_DIR>"
```

## Required Runtime Assets

The script expects these local assets, either in the default project layout or through environment variables:

- `MEETING_TO_TEXT_FFMPEG`: path to `ffmpeg.exe`
- `MEETING_TO_TEXT_SENSEVOICE`: local `SenseVoiceSmall` model directory
- `MEETING_TO_TEXT_VAD`: local `fsmn-vad` model directory
- `MEETING_TO_TEXT_3D_SPEAKER`: local `3D-Speaker` repo directory
- `MEETING_TO_TEXT_3D_SPEAKER_CACHE`: optional model cache for 3D-Speaker weights

Install Python dependencies from:

```powershell
pip install -r requirements.txt
```

## Verification Already Run

- Python syntax check passed for `meeting_to_text.py`.
- Lightweight core segmentation test passed: when diarization covers only part of the audio, the transcription plan still covers the full audio duration.

Full end-to-end ASR verification still requires the real local model/runtime environment.
