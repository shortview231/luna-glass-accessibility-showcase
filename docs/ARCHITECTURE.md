# Luna Glass Architecture

## Core Loop

```text
Hotkey or voice command
  -> identify pointer display / focused app
  -> capture screen region or monitor
  -> prefer semantic accessibility text
  -> fallback to OCR
  -> use local numeric analysis for selected spreadsheet regions
  -> use local visual explanation for selected regions when image context is needed
  -> speak result with local TTS and selected voice profile
  -> cleanup temporary artifacts
```

## Main Components

- Electron main process: global hotkeys, capture, audio, and OS integration.
- Renderer UI: settings, visual status, overlays, and user feedback.
- AT-SPI helpers: semantic app/control inspection.
- OCR helpers: local Tesseract screen reading.
- Selection overlay: manual drag-to-select context targeting.
- Spreadsheet analyzer: local selected-region numeric extraction for totals, averages, counts, minimums, maximums, and ranges.
- Ollama/LLaVA helper: local visual explanation for selected regions when image context is needed.
- TTS helpers: Piper voice output, local voice selection, and saved pacing profiles.
- STT helpers: Vosk push-to-talk transcription.

## Privacy Model

The system is designed to keep sensitive data local:

- no cloud OCR
- no cloud STT
- no cloud TTS
- no cloud visual explanation
- no continuous microphone
- temporary files are cleaned up
- action automation remains deferred

## Current Reliability Notes

Luna Glass has reached a usable v1 boundary for read/explain workflows.
Pointer reading, full-screen reading, manual selected-region explanation, selected image/poster explanation, spreadsheet math, push-to-talk, and local voice output are working.

Highlighted text is the most important near-term reliability gap because Linux applications vary in how they expose selected text through accessibility APIs.

Selected-region visual explanation is now working locally through Ollama/LLaVA. Selected-region spreadsheet math is also working locally for visible numeric cells. The strongest explanation path is manual region selection because it gives Luna a precise target and avoids noisy full-screen context.

The remaining reliability work is latency reduction, always-visible microphone/listening/thinking/speaking status feedback, low-resolution OCR hardening, and representative-app validation. Luna can still misclassify unfamiliar software or infer incorrectly from visual context, so the system reports uncertainty and keeps action automation out of scope. Broad full-screen explanation remains less dependable than selected-region explanation because full-screen captures can include mixed windows, sidebars, media, and unrelated text.

## Demo Evidence

The showcase includes `assets/video/luna-glass-first-demo-2026-07-12.mp4` as a first working demo of the voice-to-context-to-spoken-response loop.

The clip is intentionally labeled as an early demo because it has presentation limitations: audio is quiet, and the screen recording does not clearly capture the dimmed drag-selection overlay that appears during local use. The engineering value is the demonstrated interaction loop, not production video polish.
