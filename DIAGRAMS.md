Piper TTS Diagrams

Architecture Diagram
┌─────────────────┐ ┌──────────────────────┐
│ User Audio │───▶│ Audio Preprocessor │
│ (WAV) │ │ (librosa 22kHz) │
└─────────────────┘ └──────────┬──────────┘
│
┌─────────────────┐ ┌──────────┴──────────┐
│ Feature │◄───│ Feature Extractor │
│ Extractor │ │ RMS, Pauses, Pitch │
└─────────────────┘ └──────────┬──────────┘
│
┌─────────────┴────────────┐
│ Pattern Learner │
│ Statistics (mean/std) │
└──────────┬───────────────┘
│
┌──────────┴──────────────┐
│ Voice Profile JSON │
│ personalized_profile.json│
└──────────┬───────────────┘
│
┌──────────┴──────────────┐
│ Synthesis Adapter │
│ Speed/Pause Adjust │
└──────────┬───────────────┘
│
┌────────┴──────────────┐
│ Piper TTS Core │
│ en_US-amy-medium │
└────────────────────────┘
│
┌────────┴────────────┐
│ Personalized Speech │
│ Output WAV │
└──────────────────────┘
Data Flow Diagram (DFD)
Level 0 DFD - Piper TTS Personalization System

+---------------+ +---------------------+ +-------------------+
| External | | Personalization | | External |
| Entity |◄─────▶| Engine |◄─────▶| Entity |
| (User) | | | | (Audio Output) |
+---------------+ +----------+----------+ +-------------------+
│
+--------+--------+
│ Data Store │
│ voice_profile │
│ .json │
+----------------+
Sequence Diagram
User Engine Profile Piper TTS
│ │ │ │
│ Upload Audio │ │ │
│─────────────▶│ │ │
│ │ Preprocess │ │
│ │─────────────▶│ │
│ │◄─────────────│ │
│ │ Extract │ │
│ │ Features │ │
│ │ Analyze │ │
│ │─────────────▶│ Save JSON │
│ │◄─────────────│◄────────────│
│ │ │ │
│"Hello World" │ │ │
│─────────────▶│ Load Profile │ │
│ │─────────────▶│─────────────▶│
│ │◄─────────────│◄────────────│
│ │ Generate │ │
│ │ Speech │ │
│ │─────────────▶│ │
│ │◄─────────────│ │
│ Personalized │ │ │
│ WAV │ │ │
│◄─────────────│ │ │
undefined
