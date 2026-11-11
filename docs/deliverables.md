# Deliverables

[Lab 5 assignment](https://github.com/IRL-CT/Interactive-Lab-Hub/blob/9ef02d4ead28bafc0a803116a6a952f3908b7463/Lab%205/README.md) · Hao Chen Xiong

| Part | Included work | Evidence |
|---|---|---|
| A1: PyTorch | Six objects, predictions, frame dimensions, throughput, and limitations | [Recordings and log](../evidence/a1/README.md) |
| A2: MediaPipe | Pinch volume, Quiet Coyote, distance and rotation tests, and recovery | [Video and timestamps](../evidence/a2/README.md) |
| A3: Moondream | Three questions, answers, measured response times, and interaction reflection | [Setup and terminal screenshots](../evidence/a3/README.md) |
| A4: Teachable Machine | Stock demo, two training iterations, previews, export, and Pi inference | [Training and evaluation](../evidence/a4/README.md) |
| B: Interaction | Beep, voice, and voice-plus-display experiments | [Three demonstrations and logs](../evidence/b1/README.md) |
| C: Flight test | Successes, failures, informal feedback from two participants, and proposed improvements | [Reflection](../README.md#part-c-flight-test) |
| D: Characterization | Seven answers, normal walkthrough, split-screen failure, and lights-off test | [Videos and timestamps](../evidence/d1/README.md) |
| Part 2: Finished system | Cardboard enclosure, attached face, final demonstration, and three build photos | [Video, photos, and final logs](../evidence/part2/README.md) |

## Implementation

- [Final launch command](part2-run.md): 10-second VIDEO trigger, 7-second cooldown, 85% confidence threshold.
- [Controller](../scripts/b1_shelf_watcher.py), [display](../scripts/b1_display.py), and [camera/model wrapper](../scripts/a4_camera.py).
- [Trained model and labels](../models/a4-pi-v2/README.md), [audio](../assets/audio/README.md), and [hardware](materials.md).
- [Sources](sources.md) and [evidence manifest](../evidence/manifest.csv).

## Submission checks still open

- Confirm completion of the assigned introductory readings, Bellotti reading, and review of infer.py; these are not recorded here.
- Check repository and media access using the course's submission route after pushing.
- Confirm the standalone repository is linked from the required course submission location.

The recordings document the tested configurations. A pause button, tutorial override, broader evaluation, and a fresh dependency inventory remain future work.
