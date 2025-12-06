# Sequence Diagrams

## Personalization Training Sequence
User Engine Preprocessor Extractor Profile Store
│ │ │ │ │
│Upload─────▶│ │ │ │
│audio.wav │ │ │ │
│ │Load────────▶│ │ │
│ │audio───────▶│ │ │
│ │←────────────│Preprocess │ │
│ │ │─────────▶│ │
│ │ │←─────────│Extract │
│ │ │ │─────────▶│
│ │ │ │←─────────│Save JSON
│ │←─────────────│ │ │
│Profile │ │ │ │
│Ready!─────▶│ │ │ │

## Inference Sequence
User Engine Profile Piper TTS Output
│ │ │ │ │
│"Hello"────▶│ │ │ │
│ │Load─────▶│ │ │
│ │JSON─────▶│ │ │
│ │←Profile │ │ │
│ │Prepare───▶│Text Input│ │
│ │Params │─────────▶│ │
│ │ │ │Generate │
│ │ │ │◄─────────│
│ │Execute───▶│ │WAV──────▶│
│Personalized│←─────────│ │ │
│WAV◄────────│ │ │ │
undefined
