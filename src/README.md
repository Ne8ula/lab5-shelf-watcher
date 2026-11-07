# Application implementation — pending

This repository currently contains the design and deliverable scaffold, not a runnable Shelf Watcher application. No hardware behavior is claimed.

Proposed small implementation:

- `capture.py`: USB capture, fixed monitor crop, frame freshness/error reporting.
- `classifier.py`: exported model and label mapping, actual score handling.
- `controller.py`: persistence, cooldown, break, override, and error states.
- `outputs.py`: diagnostic preview, miniPiTFT face/buttons, non-overlapping local audio.
- `main.py`: connect the loop and write prediction/action logs.

Start with the upstream Teachable Machine example. Keep the controller independent of capture so timing/recovery logic can be checked without pretending those checks validate the camera or classifier. Final filenames and launch instructions should reflect actual implementation.
