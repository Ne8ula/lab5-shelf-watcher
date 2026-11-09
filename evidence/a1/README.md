# A1 evidence — PyTorch / MobileNet

Experiment date: 2026-11-09. The author confirmed that both recordings show the same run, that the course starter script was unchanged, and that the webcam was course-provided with model unknown. The network/model used by the script is known: quantized MobileNet v2. No new hardware experiment was performed during documentation review.

| File | Provenance / use |
|---|---|
| [objects.mp4](objects.mp4) | Original `IMG_8353.mov`, remuxed to MP4 without re-encoding video/audio. About 50.76 s. Shows the objects and camera handling. |
| [terminal.mp4](terminal.mp4) | Byte-for-byte copy of `Recording 2026-11-09 122702.mp4`. About 63.00 s. Shows terminal predictions and FPS. |
| [Text log](a1-final-20261109-122444-WnQoJV.txt) | Byte-for-byte copy of the author's Pi log, transferred through Windows Downloads. Original Pi path: `/home/ne8ula/lab5-a1-evidence/a1-final-20261109-122444-WnQoJV.txt`. |
| [Object stills](objects-contact-sheet.jpg) | Six phone-video frames at 1, 7, 14, 21, 30, and 44 s, arranged in presentation order. These are external views, not recorded webcam inputs. |
| [Terminal still](terminal-52s.png) | Frame at 52 s of the terminal recording; shows aircraft-carrier and syringe predictions during the late figure sequence. |

The recordings have different start/end times and are not frame-synchronized. The log has no per-frame timestamps or object annotations. Sequence-based interpretations and the author's reported candle confusion are identified as such in the main README. No per-object accuracy or exact synchronized ground truth is inferred.

## Measurement method

- Count lines beginning `image `: **425**, all `image (144, 176, 3)`.
- Count prediction lines matching `^[0-9.]+% `: **850**, two per classified frame.
- Parse lines matching `^([0-9.]+) fps$`: **54** throughput readings.
- First two readings: **0.6681618772**, **2.7498992520 FPS**. Report these separately as startup readings.
- Remaining **52** readings: minimum **6.0306799749**, maximum **7.4034690876**, median **7.2431834928 FPS**. The median averages the middle two sorted readings. It is a median of periodic reports, not total frames divided by total runtime.
- Example label maxima were computed over top-ranked predictions in the entire log, not over manually labeled object intervals: teapot **94.59%** (frame 23), mouse **99.88%** (frame 84), cup **89.28%** (frame 173), coffee mug **64.36%** (frame 182). Frames are numbered from 1.
- The starter script requests 224 × 224 capture at 36 FPS. The observed array dimensions establish a different captured size, 176 × 144; no camera mode/FPS readback was recorded.

The original log includes TorchVision/PyTorch deprecation and quantization warnings before predictions. They are preserved, not silently removed. The run nevertheless produced 425 classification results; this does not establish that every warning is harmless in all environments.

## Integrity and source

SHA-256 of the copied log, verified against the supplied Downloads file:

```text
4689fb08840da711200847255fa3b35fdd8a40bc14613dae45f2980227f575ec
```

SHA-256 of the terminal recording, verified against the supplied original:

```text
15b949b9bde62868acc2cec1eec5a8dd0df27ee7da57b1e246c7178157801148
```

Course references: [A1 instructions](https://github.com/IRL-CT/Interactive-Lab-Hub/blob/9ef02d4ead28bafc0a803116a6a952f3908b7463/Lab%205/README.md#pytorch-for-object-recognition), [infer.py](https://github.com/IRL-CT/Interactive-Lab-Hub/blob/9ef02d4ead28bafc0a803116a6a952f3908b7463/Lab%205/infer.py), and [classes.json](https://github.com/IRL-CT/Interactive-Lab-Hub/blob/9ef02d4ead28bafc0a803116a6a952f3908b7463/Lab%205/classes.json). Unchanged-script status is author-confirmed; no byte comparison against the Pi's file was performed.

These selected media files are included by specific `.gitignore` exceptions. Local links have been checked; remote publication and grader access have not been tested. The other lab demonstrations remain separate requirements. The author should complete the requested reading of `infer.py` if not already done.
