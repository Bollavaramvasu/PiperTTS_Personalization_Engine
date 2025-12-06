# Piper TTS Personalization Diagrams

## Architecture Diagram
┌────────────────────┐
│ User Audio │
│ (WAV/MP3) │
└──────────┬─────────┘
│
▼
┌────────────────────┐
│ Audio Preprocessor │
│ librosa 22kHz │
└──────────┬─────────┘
│
▼
┌────────────────────┐
│ Feature Extractor │
│ Pauses/WPM/Pitch │
└──────────┬─────────┘
│
▼
┌────────────────────┐
│ Voice Profile JSON │
│ profile.json 2.5KB │
└──────────┬─────────┘
│
▼
┌────────────────────┐
│ Synthesis Adapter │
│ Piper + Params │
└──────────┬─────────┘
│
▼
┌────────────────────┐
│ Personalized WAV │
│ output.wav 100KB │
└────────────────────┘


## Data Flow Diagram
Level 0 - Context Diagram
+----------+ +---------------------+ +----------+
| User |────▶| Personalization |────▶| Output |
| (Audio) | | Engine (2.8s) | | (Speech) |
+----------+ +----------+----------+ +----------+
│
+--------+--------+
│ JSON Profile │
│ 2.5KB Storage │
+----------------+


## Component Interaction
┌─────────────┐ ┌──────────────────┐ ┌─────────────┐
│ Preprocess │───▶│ Feature Analysis │───▶│ Profile Mgr │
│ 22kHz mono │ │ Pauses/Energy │ │ JSON Export │
└─────────────┘ └──────────────────┘ └─────────────┘
│ │ │
└────────────────────┼────────────────────┘
│
┌──────┴──────┐
│ Piper TTS │
│ + Adapter │
└─────────────┘


## Sequence Flow
User ──Upload───▶ Engine ──Preprocess───▶ Profile
│ │
│───Features───────▶ Store JSON
│ │
"Hello World"────▶ │───Load Profile───▶ Piper TTS
│ │
◀───Personalized WAV───◀

undefined
