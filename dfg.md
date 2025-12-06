# Data Flow Diagrams (DFD)

## Context Diagram (Level 0)
                       +───────────────────+
                       │    Personalization │
              +────────│       Engine      │────────+
              │        +───────────────────+        │
              │                                    │
+──────────────+─▼──────────────┬───────────────────────▼──────────────+
│ │ │ │ │
│ User │ Voice │ Piper TTS System │ Audio │
│ (Uploads) │ Profile │ │ Output │
│ │ (JSON) │ │ (WAV) │
+──────────────+────────────────┼───────────────────────────────┼──────────────+
│
+────────────┼────────────+
│ Data Store │
│ profile.json│
+────────────┘

## Level 1 DFD
+──────────────┐ +──────────────┐ +──────────────┐
│ 1.0 │ │ 2.0 │ │ 3.0 │
│ Preprocessing│───▶│ Feature │───▶│ Profile │
│ │ │ Extraction │ │ Creation │
+──────────────┘ +──────────────┘ +──────────────┘
│ │ │
│ │ │
+──────────────┐ +──────────────┐ +──────────────┐
│ Input: WAV │ │ Output: JSON │ │ Runtime Load │
+──────────────┘ +──────────────┘ +──────────────┘

## Data Dictionary
| Data Flow | Description | Volume |
|-----------|-------------|--------|
| User Audio | WAV/MP3 files | 1-5MB |
| Features | 12 acoustic metrics | 1KB |
| Profile | JSON voice profile | 2.5KB |
| Speech | WAV output | 100KB |
