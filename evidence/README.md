# Evidence index and filming plan

No media has been captured or uploaded. The [manifest](manifest.csv) tracks expected evidence without broken placeholder links.

| ID | Required content | Status |
|---|---|---|
| PREP | Environment and setup evidence | PENDING |
| A-PYT | Several objects with terminal predictions and measured FPS | PENDING |
| A-MP | Pinch and Quiet Coyote with resulting controls | PENDING |
| A-MOON | Captured scene, prompts, answers, timing | PENDING |
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

Keep raw screen captures and working videos in ignored `evidence/private/` or `data/raw/`. Add selected, reviewed screenshots under `evidence/` and reference actual paths. Large videos are ignored by default; add viewing links in the manifest/README and verify access for the grader. Do not commit credentials or unrelated personal monitor content. The repository is private, but evidence should still be deliberately selected.
