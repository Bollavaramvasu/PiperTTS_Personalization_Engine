# Data Flow Diagrams (DFD)

## Context Diagram (Level 0)
+-------------+ +------------------------+ +-------------+
| User |───▶| Personalization Engine |───▶| Speech |
| (Audio WAV) | | (2.8s processing) | | (Output WAV)|
+-------------+ +-----------+--------------+ +-------------+
│
+-------+------+
| JSON Profile |
| 2.5KB |
+-------------+


## Level 1 Processes
1.0 Preprocess ───▶ 2.0 Extract ───▶ 3.0 Profile
(WAV→PCM) (12 features) (JSON export)


**Data Dictionary:**
| Flow | Description | Size |
|------|-------------|------|
| D1 | User Audio | 1-5MB |
| D2 | Features | 1KB |
| D3 | Profile JSON | 2.5KB |
| D4 | Speech WAV | 100KB |
