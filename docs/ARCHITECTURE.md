# Luna Glass Architecture

## Core Loop

```text
Hotkey or voice command
  -> identify pointer display / focused app
  -> capture screen region or monitor
  -> prefer semantic accessibility text
  -> fallback to OCR
  -> use local visual explanation for selected regions when text is weak
  -> speak result with local TTS
  -> cleanup temporary artifacts
```

## Main Components

- Electron main process: global hotkeys, capture, audio, and OS integration.
- Renderer UI: settings, visual status, overlays, and user feedback.
- AT-SPI helpers: semantic app/control inspection.
- OCR helpers: local Tesseract screen reading.
- Selection overlay: manual drag-to-select context targeting.
- Ollama/LLaVA helper: local visual explanation for selected regions when OCR is weak.
- TTS helpers: Piper voice output.
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

Pointer and full-screen reading are the strongest current paths.

Highlighted text is the most important near-term reliability gap because Linux applications vary in how they expose selected text through accessibility APIs.

Selected-region visual explanation is now working locally through Ollama/LLaVA. The strongest explanation path is manual region selection because it gives Luna a precise target and avoids noisy full-screen context.

The remaining reliability work is representative-app validation. Luna can still misclassify unfamiliar software or infer incorrectly from visual context, so the system reports uncertainty and keeps action automation out of scope. Broad full-screen explanation remains less dependable than selected-region explanation because full-screen captures can include mixed windows, sidebars, media, and unrelated text.
