# Shelf Watcher — Lab 5: Observant Systems

**Author:** Hao Chen Xiong

**Collaborators:** None

**Deadline:** None specified

**Status:** Design and submission scaffold. Hardware execution, training, implementation, and demonstrations are pending.

Shelf Watcher is a small robot mascot placed on a shelf beside a work desk. A USB webcam observes the physical monitor, and a custom image classifier recognizes selected work, video, and neutral screen appearances. Sustained video detection is intended to trigger a spoken reminder and a suspicious expression on a miniPiTFT face. Break and work-video overrides give the user control over interruptions.

**Scope:** optical camera capture only; no screen sharing, screenshot API, browser history, or application telemetry. A screen appearance is not proof that the user is unproductive. A tutorial can be work; a static page can be distracting.

This document contains completed design rationale and explicitly labeled **planned**, **hypothesized**, and **PENDING** items. No performance measurements, successful hardware runs, fabricated observations, or finished media are claimed.

## Navigation

- [Requirement-by-requirement checklist](docs/deliverables.md)
- [Build sequence and setup](docs/build-plan.md)
- [Hardware, cables, and tools](docs/materials.md)
- [Test protocol](docs/test-plan.md) and [trial sheet](experiments/trials.csv)
- [Experiment notebook](experiments/notebook.md)
- [Evidence index and recording plan](evidence/README.md)
- [Source references](docs/sources.md)

## Preparation

The target is a Raspberry Pi 4 with an EH-1080P6 USB webcam (label: DC 5V), a speaker, and an Adafruit miniPiTFT labeled 240×135. These are owner-reported inventory, not verified operating connections. Raspberry Pi OS release, CPU architecture, Python version, camera capture, speaker interface, and display operation remain PENDING.

The robot will use a simple rounded box body, integrated feet, a removable back, a screen face, and an independently aimable chest camera. Initial construction leaves the Pi and speaker behind the mascot. The exact display connector clearance and all enclosure dimensions must be measured before CAD or printing. The servo and spare OLED are excluded from the first build.

| Preparation task | Status / evidence |
|---|---|
| Obtain Fall2025 starter files | PENDING on Pi; pinned retrieval instructions in build plan |
| Establish VNC desktop access | PENDING |
| Install and record dependency versions | PENDING |
| Verify camera, speaker, and display | PENDING |
| Read OpenCV, PyTorch, MediaPipe, and Teachable Machine introductions | PENDING author reading |
| Read Bellotti et al., *Making Sense of Sensing Systems* | PENDING author reading; source linked below |

After reading the paper, relate its five questions to the actual interface: how to address the device, recognize its attention, understand available actions, interpret its response, and recover from errors. Record the author's interpretation in the notebook; this prompt is not a completed reading reflection.

## Part A — Play with sense-making algorithms

### A1. PyTorch / MobileNet

**Planned exploration:** Run `infer.py` on the Pi, present a mug, bottle, book, and other household objects, and compare ordinary and difficult views. Inspect preprocessing and camera settings; compare one resolution/FPS configuration change. Record measured inference throughput rather than adopting the assignment's example FPS as a result.

**Design rationale:** A general pretrained image classifier is useful for exploring recognition without training a custom dataset. Its stock object labels are not the chosen WORK/VIDEO/NEUTRAL categories, motivating a custom model for Shelf Watcher.

| Observation | Result |
|---|---|
| Objects tested and predicted top labels | PENDING |
| Successful classification | PENDING |
| Incorrect classification and possible explanation | PENDING |
| Baseline and changed configuration / measured FPS | PENDING |
| Evidence | PENDING — A-PYT in evidence index |

### A2. MediaPipe

**Planned exploration:** Run `hand_pose.py`, demonstrate both pinch percentage control and Quiet Coyote, and test distance, rotation, and partial occlusion. See the build guide for identified starter-code fixes.

**Proposed pose interaction:** A deliberate hand gesture could pause reminders or acknowledge an alert. Landmark positions support continuous controls such as a pinch-controlled reminder delay. Shelf Watcher's final camera faces the monitor, so physical buttons are the simpler planned override; gesture control remains an explored alternative, not an implemented feature.

| Observation | Result |
|---|---|
| Pinch control and resulting percentage/audio behavior | PENDING |
| Quiet Coyote and resulting percentage/audio behavior | PENDING |
| Lost tracking / false trigger / distance sensitivity | PENDING |
| Evidence | PENDING — A-MP |

### A3. Moondream

**Planned exploration:** Start Ollama, pull Moondream, run `moondream_simple.py`, and ask a description question plus a targeted follow-up about a captured scene. Record exact prompts, answers, and elapsed times. Separate first-request loading time from any later warm request if measured.

**Design rationale:** A delayed image description could support an occasional desk summary. A reminder loop benefits from short, predictable responses, so a small custom classifier is the proposed final approach. The assignment warns that Moondream responses may take minutes on a Pi; actual timing here is PENDING. Moondream observes a captured still in this demo, not a continuously refreshed video.

| Observation | Result |
|---|---|
| Captured scene and exact question(s) | PENDING |
| Exact answer(s), including errors | PENDING |
| Request timing and Pi environment | PENDING |
| How the measured delay affected the experience | PENDING |
| Evidence | PENDING — A-MOON |

### A4. Teachable Machine

**Planned exploration:** Run the stock `tml_example.py`, then train an Image Project / Standard model for the final camera view. Collect about 200 varied optical images per class (the assignment suggests over 150). Preview, iterate, export TensorFlow Lite and labels, and deploy to the Pi.

| Class | Planned training examples | Collected / held out |
|---|---|---|
| WORK | Actual editor, documents, spreadsheets, and work browsing | PENDING / PENDING |
| VIDEO | Different videos, player layouts, window sizes, and content | PENDING / PENDING |
| NEUTRAL | Blank monitor, desktop, and specific neutral scenes | PENDING / PENDING |

Training and inference must use the same fixed monitor crop and image preprocessing. Hold out a separate capture session and unseen content for testing; neighboring frames from the same recording are not independent validation. NEUTRAL is a trained category, not a guarantee of detecting every unknown image. Low-confidence output gets a separate uncertain behavior.

**Affordances comparison (design analysis):** Teachable Machine lets the designer define categories through examples, at the cost of collecting representative data. MediaPipe exposes landmarks suited to geometric gesture rules and continuous controls. OpenCV provides capture and image-processing primitives from which a designer can build explicit visual rules. These approaches can be combined: Shelf Watcher proposes OpenCV capture/cropping plus a learned classifier.

**PENDING:** stock-model observation; training counts; preview mistakes; changes between model versions; export details; Pi inference outcome; training/preview/export screenshots (A-TM).

## Part B — Fold: construct an interaction

### Proposed interaction

The familiar's face points toward the user while the camera bracket points toward the monitor. The bracket is locked before dataset capture. The model classifies camera frames, and a time-based controller decides when to remind the user. Speech is a prerecorded local line: **“Hey. Back to work.”** No generative speech service is needed.

| Input / condition | Planned output |
|---|---|
| Confident WORK | Relaxed face; clear pending video timer |
| Confident VIDEO | Suspicious face; begin/continue persistence timer |
| VIDEO persists 15 seconds and cooldown permits | Play one reminder; annoyed face; start cooldown |
| NEUTRAL or low-confidence / unstable prediction | Neutral/puzzled face; clear pending video timer; no reminder |
| Missing/stale frame or camera read failure | Camera-error state; clear pending timer; no reminder |
| Break button | Pause reminders for five minutes; show break status |
| Work-video button | Toggle visible work-video override until user clears it |

Starting parameters, not calibrated results: one inference/second, minimum top score 0.85, persistence 15 seconds, cooldown 60 seconds, and break duration 300 seconds. See [configuration proposal](config/settings.example.json). Use elapsed monotonic time rather than assuming a frame rate. Reset pending detection across non-video states, overrides, and capture gaps. Avoid overlapping audio and repeated triggers within the cooldown.

### Planned input/output experiments

1. Compare full camera frame versus fixed monitor crop on the same held-out scenes.
2. Compare immediate triggering versus a 15-second persistence rule.
3. Compare face-only feedback versus face plus speech.
4. Exercise break and work-video overrides with actual video viewing.

**PENDING:** implemented code, measured comparison, selected final settings, setup photograph, and integrated-system video (B-SYSTEM). The table above is a specification, not current executable behavior.

## Part C — Flight test

Use the [test protocol](docs/test-plan.md) and [trial sheet](experiments/trials.csv). The following are hypotheses and intended mitigations, not observations.

| Required question | Design-stage answer / remaining evidence |
|---|---|
| When does it work? | Hypothesis: stable camera, clear monitor view, and familiar layouts represented in training. PENDING measured successes. |
| When does it fail? | Candidate cases: unseen layouts, split screens, glare, occlusion, camera movement, and work videos. PENDING observed failures. |
| Why does it fail? | Possible causes: dataset gaps, small screen details after resizing, background shortcuts, or category ambiguity. Verify using captured examples. |
| Other scenarios that could cause problems? | A paused video, animated work content, a second monitor, another person blocking the camera, theme changes, and display sleep. |
| Are users aware of uncertainty? | Plan: puzzled/error expressions and visible override state; numerical scores in the diagnostic preview. PENDING user reaction. |
| Consequences of misclassification? | False reminders interrupt legitimate work; missed detections reduce usefulness. A score does not establish intent or productivity. |
| How could the interaction address errors? | Persistence, cooldown, manual overrides, camera-error suppression, and easy repositioning. PENDING verification of each implemented behavior. |
| Algorithm optimizations to try? | Fixed crop, representative examples, lower sampling rate, threshold tuning, and retraining. Compare one change on held-out scenes and report the tradeoff. |

**Results summary:** PENDING. Report correct/incorrect/uncertain counts, false reminders during work, missed reminders during video, and end-to-end delay. Keep classifier performance separate from controller correctness. Do not count a work tutorial as leisure ground truth merely because it is a video.

## Part D — Reflect: characterize the system

| Question | Initial characterization to test |
|---|---|
| What can it be used for? | A voluntary personal reminder for familiar screen-viewing habits. It is not a productivity measurement or employee-monitoring tool. |
| Good environment? | Stable shelf mount, clear view of one monitor, and lighting/layouts represented in training. |
| Bad environment? | Strong glare, steep angle, frequent monitor movement, rapidly changing applications, or mixed work/video layouts. |
| When will it break? | Hypothesis: out-of-distribution scenes, obstructed lens, camera disconnect, or changes to crop/mount. Actual cases PENDING. |
| How will it break? | It may confidently choose a wrong class, switch labels, miss a video, or fail to capture. Intended control behavior suppresses alerts on known uncertainty/errors but cannot catch all confident mistakes. |
| Other properties/behaviors? | There is a deliberate 15-second grace period plus inference/playback latency. It needs installation-specific data and manual intent overrides. |
| How does it feel? | Design intent: amusing and gently corrective. Actual author/user experience, including annoyance, is PENDING. |

**Required characterization video:** PENDING — D-CHAR. Demonstrate and narrate the questions above using real successes, faults, and recovery.

## Part 2 — Finished system in use

**Status: NOT BUILT / NOT DEMONSTRATED.**

Planned final sequence: show shelf installation and optical camera view; work normally; switch to a video; wait for the real grace period; hear the reminder; return to work; demonstrate a legitimate tutorial override; show a failure and recovery. Label any edited time compression. Do not imply a prerecorded face sequence is live classification.

- Final integrated demo link: PENDING — FINAL-DEMO.
- Finished enclosure photo: PENDING — FINAL-PHOTO.
- Final code / model / settings revision: PENDING.
- Reproducible final launch command: PENDING implementation and Pi verification.
- Final limitations and improvements: PENDING tests; retain known camera-view and intent limitations.

## References and attribution

- [Official Lab 5, Fall2025](https://github.com/IRL-CT/Interactive-Lab-Hub/tree/Fall2025/Lab%205)
- [Pinned assignment](https://github.com/IRL-CT/Interactive-Lab-Hub/blob/9ef02d4ead28bafc0a803116a6a952f3908b7463/Lab%205/README.md)
- [Bellotti et al. paper](https://sites.cc.gatech.edu/people/home/keith/pubs/chi2002-sensing.pdf)
- [Detailed source and hardware references](docs/sources.md)

This repository is a standalone private student project, not an upstream fork. Original course code is retrieved separately with provenance. Documentation scaffolding and design organization were assisted by Codex; experimental observations must be supplied and reviewed by the author. Course-specific disclosure and submission rules remain to be checked by the author.
