# Diagrams

## Architecture
graph TB
A[Your Audio] --> B[Preprocess]
B --> C[Features]
C --> D[Profile JSON]
D --> E[Piper TTS]
E --> F[Your Voice WAV]
## Data Flow
A[Upload Audio] --> B[Analyze]
B --> C[Save Profile]
C --> D[Generate Speech]
## Components
graph LR
P[Personalization] --> T[Piper TTS]
