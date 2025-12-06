# Sequence Diagrams

## Training Sequence
User → Engine → Preprocessor → Extractor → Profile Store
| | | | |
Upload | Load | Extract | Save
audio.wav | audio | features | profile.json

## Inference Sequence  
User → Engine → Profile → Piper TTS → Output
| | Loader | | |
"Hello" | Load JSON | Adjust | Generate
|←Profile─────→|←Params──▶|←WAV────▶


**Timings:** Training=2.8s, Inference=0.7s
