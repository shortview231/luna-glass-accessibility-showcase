# Luna Glass Architecture

## Core Loop

```text
Hotkey or voice command
  -> identify pointer display / focused app
  -> capture screen region or monitor
  -> prefer semantic accessibility text
  -> fallback to OCR
  -> speak result with local TTS
  -> cleanup temporary artifacts
```

## Main Components

- Electron main process: global hotkeys, capture, audio, and OS integration.
- Renderer UI: settings, visual status, overlays, and user feedback.
- AT-SPI helpers: semantic app/control inspection.
- OCR helpers: local Tesseract screen reading.
- TTS helpers: Piper voice output.
- STT helpers: Vosk push-to-talk transcription.

## Privacy Model

The system is designed to keep sensitive data local:

- no cloud OCR
- no cloud STT
- no cloud TTS
- no continuous microphone
- temporary files are cleaned up
- action automation remains deferred

## Current Reliability Notes

Pointer and full-screen reading are the strongest current paths.

Highlighted text is the most important near-term reliability gap because Linux applications vary in how they expose selected text through accessibility APIs.

Contextual explanation is currently diagnostic groundwork, not an accepted visual-understanding feature. The implementation can route spoken explanation requests and collect text context from accessibility, OCR, and application surfaces, but live testing still shows that broad "explain what I see" commands may receive no usable visual context. The next engineering step is a runtime capture audit that verifies DOM text, AT-SPI text, OCR text, screenshot pixels, display coordinates, and window containment before deciding whether a local image-understanding adapter is required.
