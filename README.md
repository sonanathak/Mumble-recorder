# Mumble

Mumble is a local-first desktop meeting assistant built with Tauri + React + TypeScript + Rust + SQLite.

## What users can do

- Create meetings
- Record microphone audio per meeting
- Play recordings
- Transcribe with local Whisper GGML models
- Manage meetings (clear recording / delete meeting)
- Choose default models in Settings
- Switch Light/Dark mode

## For people who only want to run it (no coding)

Download the macOS `.dmg` from **GitHub Releases** and open it.

After launch:
1. Allow microphone access when prompted
2. In Settings, set your Whisper model path (example: `~/Downloads/ggml-base.bin`)

## For developers (clone + run)

Requirements:
- Node.js + pnpm
- Rust (`rustup`)
- CMake
- macOS

```bash
git clone <your-repo-url>
cd mumble
source "$HOME/.cargo/env"
pnpm install
pnpm tauri dev
```

## Build a `.dmg`

```bash
cd mumble
source "$HOME/.cargo/env"
pnpm tauri build
```

Artifacts are generated under:

```text
src-tauri/target/release/bundle/
```

## Current blocker on this machine

On this specific machine, `pnpm tauri build` currently fails inside `whisper-rs-sys` (`std::filesystem` availability in the Apple SDK toolchain), so `.dmg` could not be produced locally here.

To produce a `.dmg`, run the same build on:
- a newer macOS + Xcode/Command Line Tools setup, or
- a GitHub Actions `macos-latest` runner.

## Data paths

- DB: `~/Library/Application Support/com.a1040811.mumble/mumble.db`
- Audio: `~/Library/Application Support/com.a1040811.mumble/meetings/<meeting_id>/audio.wav`
