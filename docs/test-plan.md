# Test protocol

Status: planned; no tests executed. Trial counts are this project's proposed protocol, not course-mandated quantities.

## Capture and classification tests

Use five independent presentations for each condition below (35 baseline trials). Vary content within a condition. A fresh presentation is not simply the next adjacent frame. Keep separate training and test sessions. Record model/config version, lighting, crop, and position. Start trials with no active override/cooldown unless the test explicitly requires it.

| ID | Condition | Purpose |
|---|---|---|
| C01 | Normal work layouts | False video classifications and false reminders |
| C02 | Familiar video layouts with held-out content | Baseline detection and reminder delay |
| C03 | Unseen videos/content | Generalization beyond training frames |
| C04 | Windowed or split-screen video | Ambiguity; record primary activity and visual mixture |
| C05 | Brightness, dim room, or glare variation | Lighting robustness; record which variable changed |
| C06 | Occlusion or changed camera angle | Loss of expected view and recovery |
| C07 | Work-related tutorial | Separate visual VIDEO detection from legitimate work intent; test override |

In C07, VIDEO can be visually correct while a reminder is unwanted. Record intended activity separately from visual label. Do not relabel an unseen/ambiguous image after seeing the model prediction merely to count it correct.

## Controller tests

| ID | Action | Expected proposed behavior |
|---|---|---|
| S01 | Video for less than 15 seconds, then work | No reminder; persistence timer resets |
| S02 | Sustained video with cooldown clear | One reminder after persistence plus processing/playback delay |
| S03 | Continued video through cooldown | No repeat before 60 seconds; later repeats follow documented final policy |
| S04 | Start a five-minute break during video | No reminders during break; visible status; no stale instant alert when break expires |
| S05 | Toggle work-video override on/off | Suppression while on; fresh persistence period after clearing |
| S06 | Unplug/block camera; reconnect/unblock | Missing capture gives error and no alert; obscuration may still confidently misclassify and must be reported |
| S07 | Low-confidence output or stale frame gap | Pending video time resets; no alert based on stale evidence |
| S08 | Press buttons during audio playback | Controls remain responsive; playback cannot overlap |

Test physical failure as well as predicted outputs. If an injected/simulated prediction is used to isolate controller logic, label it simulated and do not count it as classifier or hardware validation.

## Measurements

- Visual classification: correct, incorrect, uncertain counts with denominators; optional per-class confusion table.
- Interaction: false reminders during legitimate work, missed reminders during sustained leisure video, and override correctness.
- Timing: capture/inference latency separately from deliberate persistence and cooldown; log alert delay from trial start.
- Experience: author's actual notes about clarity, annoyance, sound audibility, and recovery. No user-study claim without participants.
- Comparison: record baseline settings, one change, same held-out cases, and actual before/after results. Additional data used for retraining is no longer held-out test data.

`trials.csv` contains deliberately blank actual-result columns. `not_run` is a status, not a failure or success. Fill expected visual label and activity before running each trial. Evidence paths or URLs must identify the actual clip/image/log.
