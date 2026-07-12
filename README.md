# Luna Glass Accessibility Showcase

Luna Glass is a local-first accessibility assistant project built inside Lucid_Vision. It is designed for low-vision and screen-fatigue workflows that need dependable screen reading and voice assistance while staying private, free, and offline.

This repository is a public-facing portfolio summary. It does not include private audio, screenshots, credentials, databases, or the full private app source.

## What This Project Demonstrates

- Pointer-based screen reading.
- Full-monitor reading by voice command.
- Local OCR with Tesseract.
- Local text-to-speech with Piper.
- Local speech-to-text with Vosk.
- High-contrast reading-region overlay.
- Semantic-first accessibility reading through AT-SPI.
- Push-to-talk voice workflow.
- Immediate stop/cancel workflow.
- Privacy-first cleanup of temporary audio and capture files.
- Drag-to-select context targeting for precise screen regions.
- Local visual explanation using an offline Ollama/LLaVA model when OCR is not enough.
- Local explanation diagnostics that distinguish OCR, semantic text, and image context.

## User Problem

The accessibility workflow needs a tool that can:

- Read what is near the mouse pointer.
- Read the whole monitor when zoom makes context hard.
- Read highlighted text.
- Explain visible UI in plain language.
- Describe selected visual regions when text extraction is not enough.
- Eventually identify likely errors in spreadsheets or forms.
- Eventually perform corrections only after explicit approval.

## Current Working Features

Hotkeys:

- `Ctrl+Alt+P`: read around pointer.
- `Ctrl+Alt+M`: voice command / push-to-talk.
- `Ctrl+Alt+R`: repeat last reading.
- `Ctrl+Alt+X`: stop or cancel.

Working capabilities:

- Pointer-region reading.
- Full-screen monitor reading.
- Piper speech output.
- Vosk microphone transcription.
- Visible listening indicator.
- Visible pointer-region overlay.
- Manual drag-to-select region capture.
- Selected-region visual explanation through local Ollama/LLaVA.
- Local OCR fallback.

## First Demo Video

The live showcase includes a first working demo clip:

- `assets/video/luna-glass-first-demo-2026-07-12.mp4`

This is an early proof recording, not a polished product video. It demonstrates the core loop of speaking to Luna, having Luna process local screen context, and receiving a spoken answer. Known presentation limits: the audio is quiet, and the recording does not clearly show the dimmed selection overlay or drag-select action that was visible during local use.

Current known limitation:

- Highlighted-text reading is implemented but still unreliable in some Linux applications because selected text is not always exposed consistently through AT-SPI.
- Selected-region visual explanation is now working locally, but accuracy is still being validated across more apps, screens, and image types. Luna reports what it can observe and may still misclassify unfamiliar applications.
- Broad full-screen explanation remains less dependable than selected-region explanation because full-screen capture can include too much mixed context.

## Local Technology Stack

- Electron
- React
- Tesseract OCR
- Ollama / LLaVA local vision model
- AT-SPI / pyatspi
- Piper TTS
- Vosk STT
- Local image preprocessing
- Linux audio tools

No paid cloud services are required.

## Safety Boundary

Luna Glass is designed around strict boundaries:

- Fully local and offline by default.
- No paid APIs.
- No background always-on listening.
- No autonomous clicking or system control.
- No purchases, credential handling, or destructive actions.
- Speech and screen captures are temporary by default.
- Corrections require explicit approval in future phases.

## Roadmap

1. Stabilize pointer and full-screen reading.
2. Improve highlighted-text reliability.
3. Expand selected-region visual explanation validation across browsers, Electron apps, media frames, documents, and spreadsheets.
4. Improve explanation accuracy and source diagnostics while staying free/offline.
5. Improve natural Luna voice quality while staying free/offline.
6. Add read-only error detection.
7. Add approval-gated corrective actions later.

## Suggested Portfolio Description

Luna Glass is a fully local accessibility assistant prototype that combines pointer-aware OCR, Linux accessibility APIs, local speech recognition, and offline text-to-speech to help low-vision users read and understand screen context without cloud services.
