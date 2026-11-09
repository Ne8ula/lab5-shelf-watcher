# Evidence index and filming plan

A1 recordings, stills, and the original log are in [a1/](a1/README.md). My A2 hand-tracking video and rotation comparison are in [a2/](a2/README.md). My A3 setup photo, three terminal screenshots, and transcribed questions, answers, and timings are in [a3/](a3/README.md). Remote publication and grader access have not been tested. The [manifest](manifest.csv) separates available local evidence from pending demonstrations.

| ID | Required content | Status |
|---|---|---|
| PREP | Environment and setup evidence | PARTIAL — A1 environment reported in main README; other hardware pending |
| A-PYT | Several objects with terminal predictions and measured FPS | DOCUMENTED LOCALLY — [recordings, stills, and log](a1/README.md) |
| A-MP | Pinch and Quiet Coyote with resulting controls | DOCUMENTED LOCALLY — [video, timestamps, and rotation comparison](a2/README.md) |
| A-MOON | Scene setup, prompts, answers, timing | DOCUMENTED LOCALLY — [setup photo, screenshots, and transcription](a3/README.md); raw webcam input not included |
| A-TM | Stock demo; training counts, preview, export screenshots; custom Pi inference | PENDING |
| B-SYSTEM | Algorithm integrated with feedback, input/output comparison | PENDING |
| C-FAULTS | Actual errors, effects, and recovery; trial links | PENDING |
| D-CHAR | Video answering all seven characterization questions | PENDING |
| FINAL-DEMO | Finished physical system in real use | PENDING |
| FINAL-PHOTO | Printed robot, camera direction, connections | PENDING |

## Recording sequence

1. Film exploration clips during each demo, including faults.
2. Characterization: explain intended use and good conditions; show bad conditions and an actual failure; demonstrate handling; discuss latency and how it feels.
3. Final use: show the shelf robot and real optical preview, switch work to video, wait through the actual grace period, capture audible reminder and face, return to work, then show tutorial override.

One recording can support multiple requirements with explicit timestamps. Label time compression and simulations. A staged face animation without live inference is not a final-system demonstration.

## Storage

Keep raw screen captures and working videos in ignored `evidence/private/` or `data/raw/`. Add selected, reviewed screenshots under `evidence/` and reference actual paths. Large videos are ignored by default; the selected A1 and A2 recordings have explicit exceptions and relative viewing/download links. Verify access for the grader after publication. Do not commit credentials or unrelated personal monitor content. The repository is private, but evidence should still be deliberately selected.
