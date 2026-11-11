# Part B: beep and voice experiments

The beep and voice experiments have run on the Pi. [Recordings and checked logs](../evidence/b1/README.md).
The Leviathan V2 is connected by Bluetooth. [Experiment 3 adds the miniTFT display](part-b-display.md).

## Transfer from Windows PowerShell

```powershell
# Run from the repository root.
Compress-Archive -Path scripts,models,assets -DestinationPath "$env:TEMP\shelf-watcher-pi.zip" -Force
scp "$env:TEMP\shelf-watcher-pi.zip" ne8ula@vaultpi.local:~/part-b-pi.zip
```

## Prepare and test on the Pi

Run in the existing Pi SSH terminal, as the desktop user (no sudo):

```bash
cd ~/a4-shelf-watcher
source ~/venv-tml/bin/activate
python -m zipfile -e ~/part-b-pi.zip .
pactl get-default-sink
python scripts/b1_shelf_watcher.py --mode voice --audio-test
```

The test plays the three clips once in creation order. Confirm they come from
the Leviathan V2. A successful player exit alone does not prove the sound was
audible. If they play elsewhere, select the Leviathan as the Pi's default output
and repeat this test. The runner uses `paplay`, or `pw-play` if `paplay` is absent.

## Experiment 1: beep

```bash
python scripts/b1_shelf_watcher.py --mode beep --seconds 180
```

Beep mode uses three 0.3-second beeps with 0.15-second gaps, approximately
6 dB louder in the audio file than the original single beep. It triggers after
five seconds of qualifying VIDEO with **no cooldown**. While qualifying VIDEO
continues, the triple-beep clip repeats as soon as the previous playback ends.
Clips never overlap. WORK, NEUTRAL, or low confidence resets the five-second timer.

## Experiment 2: three voice clips

```bash
python scripts/b1_shelf_watcher.py --mode voice --seconds 180 --persistence 15 --cooldown 15
```

Each run starts after ten seconds. Minimize SSH and VNC, keep the webcam fixed,
and show editor, brief video, editor, sustained video, and desktop scenes. Use
the same sequence for both modes. VIDEO must remain at or above 85% to qualify.
The voice command above uses the tested 15-second trigger and 15-second cooldown.
The script default without the explicit cooldown argument remains 60 seconds.
WORK, NEUTRAL, low scores, and gaps over three seconds reset the VIDEO timer.
The modes now differ in both sound and timing; observations compare the full
configurations. These are initial experiment settings, not calibrated values.

Voice reminders cycle **01 -> 02 -> 03 -> 01**, advancing only after successful
playback. Each new run starts at 01. Clips never overlap. A failed audio player
or camera read stops the run and records the failure. Ctrl+C stops a run early.
The brief all-clips audio test bypasses classifier timing; it is only an audio check.

In voice mode with uninterrupted qualifying VIDEO, three reminders can start approximately
15, 30, and 45 seconds into the VIDEO streak. Scene changes or uncertain
predictions can delay them; do not claim all three played unless the log and
audible demonstration confirm it.

Each run saves a unique folder under `runs/part-b/` containing:

- `camera.mp4`: camera frames, predictions, timer, and active clip caption.
- `predictions.csv`: frame numbers, capture timestamps, predictions, and actions.
- `events.jsonl`: audio start/completion events and triggering frame numbers.
- `metadata.json`: settings, model/audio hashes, status, and frame count.

**The camera MP4 is silent.** Record the physical demonstration with your phone's
microphone to capture the actual speaker output. After both experiments, note
which output you prefer and why, and link the demonstration in Part B.
