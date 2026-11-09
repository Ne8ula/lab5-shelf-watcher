# Deliverable checklist

Source: [Fall2025 assignment](https://github.com/IRL-CT/Interactive-Lab-Hub/blob/9ef02d4ead28bafc0a803116a6a952f3908b7463/Lab%205/README.md). Read 2026-11-07. Boxes refer to completed work with evidence, not the existence of a plan. Only the legacy Audio_optional and CV_optional exercises are explicitly optional; all four named Part A explorations are retained for coverage.

## Preparation

- [x] Identify author: Hao Chen Xiong; collaborators: none.
- [x] Choose and document Shelf Watcher concept and inventory.
- [x] Retrieve course starter files on Pi (A1 executed; unchanged starter script confirmed by author).
- [ ] Verify Pi, webcam, VNC, audio, and dependencies; record environment.
- [ ] Read OpenCV, PyTorch, MediaPipe, and Teachable Machine introductions.
- [ ] Read Bellotti et al. and record reflection.

## A — Play

- [x] A-PYT: run PyTorch/MobileNet with several objects; capture pictures/video and observations. [Evidence](../evidence/a1/README.md).
- [ ] A-PYT: author reads `infer.py` and becomes familiar with the code (completion not yet confirmed).
- [x] A-PYT: record requested camera configuration, observed frame size, and actual performance. Configuration/model changes are optional in the assignment; the documented run used the unchanged starter script.
- [x] A-MP: demonstrate hand tracking, pinch percentage/audio control, Quiet Coyote, and recovery; test distance and rotation. [Video and evidence](../evidence/a2/README.md).
- [x] A-MP: explain a position-based interaction and how the observed failure affects its design. [A2 reflection](../README.md#a2-mediapipe); proposed feature, not implemented.
- [x] A-MOON: run Ollama/Moondream demo with camera image and question(s); record response(s). [Setup photo, three terminal screenshots, transcription, and timings](../evidence/a3/README.md).
- [x] A-MOON: discuss delayed responses and suitable interactions, grounded in measured timing. [A3 reflection](../README.md#a3-moondream).
- [ ] A-TM: run supplied Teachable Machine example.
- [ ] A-TM: train own Standard image model; aim for over 150 varied examples per class; include neutral/background examples.
- [ ] A-TM: preview and iterate; record changes.
- [ ] A-TM: export TFLite and labels, transfer to Pi, and demonstrate inference.
- [ ] A-TM: include training/preview/export screenshots.
- [ ] A-TM: explain classifier idea and affordances compared with OpenCV/MediaPipe.

## B — Fold

- [ ] Integrate one explored model into a real interaction.
- [ ] Experiment with different inputs and outputs; document before/after choices.
- [ ] Describe implementation and experimentation; replace proposed behavior with verified behavior.
- [ ] B-SYSTEM: video showing the algorithm embedded in the observant system.

## C — Flight test

- [ ] Record successful operation and failures with evidence.
- [ ] Explain likely causes, distinguishing evidence from hypothesis.
- [ ] Identify additional problematic scenarios.
- [ ] Discuss user awareness of uncertainty.
- [ ] Discuss impact of misclassification.
- [ ] Explain and demonstrate error-handling changes.
- [ ] Discuss possible algorithm optimizations; record any attempted comparison.

## D — Reflect

- [ ] Address uses; good environment; bad environment; when it breaks; how it breaks; other behaviors; how it feels.
- [ ] D-CHAR: short video demonstrating those answers, including faults and handling.

## Part 2 and submission

- [ ] Finish integrated system and identify exact code/model/config revision.
- [ ] FINAL-DEMO: short video of finished system in use.
- [ ] Check all evidence links and viewing permissions as the intended grader.
- [ ] Remove unresolved placeholders from final claims, or explicitly document unresolved limitations.
- [ ] Add final launch instructions and dependency/environment record.
- [ ] Confirm how the course expects the standalone repository linked/submitted.
- [ ] If graders need private-repo access, grant only the instructed access; do not make the repo public by default.

Videos may be reused with clear timestamps when they genuinely demonstrate multiple requirements. The separate IDs prevent accidentally omitting the characterization or final-use demonstration. Hardware embellishments, servo motion, transfer learning, and legacy audio/CV are not required for this plan.
