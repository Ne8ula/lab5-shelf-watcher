# Part 2: launch the finished companion

This uses the existing Raspberry Pi installation, USB webcam, miniPiTFT, and
connected speaker. Stop any other camera script before launching. The final
recorded settings are 10 seconds of sustained VIDEO at or above 85%, with a
7-second minimum interval between reminder starts. Audio never overlaps.
The command below reproduces the recorded configuration.

From Windows PowerShell:

```powershell
ssh ne8ula@vaultpi.local
```

In the Pi terminal, as the desktop user:

```bash
cd ~/a4-shelf-watcher
source ~/venv-tml/bin/activate
pactl get-default-sink
python scripts/b1_shelf_watcher.py --mode voice --audio-test
```

Confirm the three clips are audible through the intended speaker, then run:

```bash
python scripts/b1_shelf_watcher.py \
  --mode voice \
  --display mini-pitft \
  --persistence 10 \
  --cooldown 7 \
  --threshold 0.85 \
  --start-delay 10 \
  --seconds 300
```

After the ten-second countdown, the run records for up to five minutes. Ctrl+C
stops it early and saves the files. Use `--display-rotation 270` if required by
the screen orientation. The video evidence is a shorter phone recording, not
proof that the program ran for all five minutes.

## Implementation and environment

- Controller and recorder: [b1_shelf_watcher.py](../scripts/b1_shelf_watcher.py).
- Display: [b1_display.py](../scripts/b1_display.py).
- Camera/model wrapper: [a4_camera.py](../scripts/a4_camera.py).
- Model: [Pi-trained v2 TFLite](../models/a4-pi-v2/model.tflite) and [labels](../models/a4-pi-v2/labels.txt).
- Voice clips: [audio assets](../assets/audio/README.md).
- Existing platform: Raspberry Pi 4, Debian 12 Bookworm, aarch64, Python 3.11.2
  as previously reported. [Display setup](part-b-display.md) and
  [audio setup](part-b-run.md) document the installed hardware workflow.
- Local source/model/audio hashes are recorded in the [Part 2 receipt](../evidence/part2/receipt.json).
  The final run's recorded model and audio hashes match these local assets.
  Source hashes identify the repository snapshot; the deployed source was not
  independently hashed. A fresh dependency inventory has not been collected.

Each run writes a unique directory under `~/a4-shelf-watcher/runs/part-b/` with
`predictions.csv`, `events.jsonl`, `metadata.json`, and `camera.mp4`.
The Pi camera MP4 is silent; the [phone demonstration](../evidence/part2/finished-companion.mp4)
preserves the physical speaker audio. See the [evidence notes](../evidence/part2/README.md)
for the availability and scope of the final run logs.
