#  Piper TTS Personalization Diagrams

##  Architecture Diagram
ARCHITECTURE.md

---

##  Data Flow Diagram (Level 0 - Context)
flowchart LR
U[User
(Audio Input)] -->|2.8s Processing| P[Personalization Engine]
P --> O[Output
(Personalized Speech)]
P --> J[JSON Profile
2.5KB Storage]

---

##  Component Interaction
flowchart TD
A[Preprocess
22kHz Mono] --> B[Feature Analysis
Pauses / Energy]
B --> C[Profile Manager
JSON Export]

A -.->|Shared Data| D[Piper TTS + Adapter]
B -.->|Shared Data| D
C -.->|Profile Import| D
---

##  Sequence Flow
sequenceDiagram
participant User
participant Engine
participant Profile
participant Piper

User ->> Engine: Upload Audio File
Engine ->> Profile: Preprocess & Extract Features
Profile ->> Profile: Store Profile (profile.json)
User ->> Piper: Text Input ("Hello World")
Piper ->> Profile: Load Voice Profile
Piper ->> User: Return Personalized WAV Output
