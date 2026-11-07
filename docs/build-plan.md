# Build plan — fastest route to full coverage

Current state: repository and documentation only. Commands below run on the Raspberry Pi unless stated otherwise. Do not reimage a working course setup merely to follow this plan. Expected effort is roughly one focused day plus unknown installation/download delays; this is an estimate, not a deadline.

## 1. Record environment and validate basic I/O

Run `cat /etc/os-release`, `uname -m`, `python3 --version`, and `df -h`. Save relevant version summaries in the experiment notebook. Establish VNC desktop access. Test the USB webcam and local speaker before ML installation. Confirm camera index, orientation, and actual capture dimensions; verify the speaker interface rather than assuming USB audio. Close one camera demo before starting another.

## 2. Retrieve original course examples

From this repository directory, the following keeps a separate, Git-ignored upstream checkout:

```bash
git clone --branch Fall2025 --single-branch https://github.com/IRL-CT/Interactive-Lab-Hub.git upstream
git -C upstream checkout 9ef02d4ead28bafc0a803116a6a952f3908b7463
cd 'upstream/Lab 5'
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

This upstream pin was inspected for planning. The course pins may not install on every Pi OS/Python combination; if installation fails, record the exact error and resolve that compatibility issue before changing multiple versions. Keep experiments in isolated environments if necessary. The exact tested install procedure remains pending.

Ollama is a separate service, not supplied by `requirements.txt`. After following its official Linux installation instructions and starting it, run `ollama pull moondream`. Ensure Python `requests` is available for the demo. The hand demo also needs working `aplay` and `pactl`, an audio output, and `chmod +x loop_audio.sh`.

## 3. Correct the supplied MediaPipe argument mismatch

In the upstream working copy, change `detectionCon=int(0.7)` to `detectionCon=0.7` in `hand_pose.py`. Replace the positional `Hands(...)` call in `HandTrackingModule.py` with:

```python
self.hands = self.mpHands.Hands(
    static_image_mode=self.mode,
    max_num_hands=self.maxHands,
    model_complexity=0,
    min_detection_confidence=self.detectionCon,
    min_tracking_confidence=self.trackCon,
)
```

The pinned MediaPipe API's third argument is model complexity, not detection confidence. This is a source-inspection fix, not a claim of Pi execution. Record the change and actual outcome. Also handle failed camera reads before image processing when building the final program.

## 4. Capture all Part A explorations

Run `infer.py`, `hand_pose.py`, `moondream_simple.py`, and `tml_example.py` from the course Lab 5 directory in the appropriate environment. Film/record evidence immediately. PyTorch's supplied script reports predictions in the terminal rather than a GUI image window. Record object presentation with those predictions. Test both gestures in MediaPipe. Record Moondream prompts, answers, and timing. Run the stock Teachable Machine model before replacing it. Complete the reading and notebook prompts in parallel with downloads, without claiming an unperformed demo as complete.

## 5. Fix shelf geometry before collecting data

Mount the camera temporarily, aim at the physical monitor, select a fixed crop, and lock the bracket. Check that work/video screen layouts remain distinguishable in the processed camera image. Use your usual applications and viewing site initially. Face direction and camera direction may differ. Do not print the full housing before a fit test.

## 6. Train and export

Collect about 200 varied optical frames each for WORK, VIDEO, and NEUTRAL. Keep raw captures in ignored `data/raw/`. Apply the intended crop consistently. Train by uploading these images to Teachable Machine on the computer; do not substitute screenshots. Hold out a separate capture session and unseen content. Screenshot training counts, preview, and export. Export TensorFlow Lite and labels, preserving exact label spelling/order. Record export type and preprocessing requirements in `models/README.md`. Compare a small held-out set before decorating the robot.

## 7. Implement the controller and local output

Implementation remains pending in `src/`. Start with the course wrapper and a diagnostic preview, then add timed state transitions from README/config. Model indices must map through exported labels; do not assume a fixed index ordering. Do not equate the neutral class with all unknown inputs. Use fresh frames, monotonic timing, non-overlapping playback, cooldown, and explicit error/override states. Log predictions and actions separately. Record a short local voice clip and keep the audio output non-blocking so buttons remain responsive.

Run the face/buttons using the direct Python miniPiTFT approach after verifying the exact board. Start with static expressions; no animation engine is necessary. Compare face-only versus speech feedback and immediate versus persistent alerts. Keep sampling-rate/threshold choices experimental until measured.

## 8. Fit and print the simple robot

Use `cad/README.md` for measurements. Print the screen/camera fit piece first. Print one hollow body plus rear cover with integrated feet. Keep the Pi/speaker behind it initially, and leave the servo unused. Install components with screws or removable mounts, route cables with strain relief, and recheck the trained camera view after assembly. If it changes, repeat calibration/data evaluation.

## 9. Test and iterate

Follow `docs/test-plan.md` and fill actual rows in `experiments/trials.csv`. Perform one controlled before/after improvement and retest affected cases. Preserve real failures. Record tests of cooldown, break expiration, override, missing camera, and recovery.

## 10. Finish the deliverable

Replace PENDING items only with actual evidence. Film characterization and final use, update the evidence manifest and README, record final code/model/config revisions and exact launch command, and audit every requirement. Check private-repository/media access with the course submission route. Do not publish the repository or invite people without an instruction identifying the intended recipients.
