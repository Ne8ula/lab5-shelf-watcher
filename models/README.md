# Model handoff

No trained model exists in this repository yet. After training, place the exported `model.tflite` and `labels.txt` here. Do not use the course's stock model as evidence of having trained a custom model.

For automatic webcam bursts or extraction from existing optical recordings, see
[short-burst sample collection](../docs/sample-collection.md). The collector has
been checked with a synthetic video fixture; real webcam collection and model
training remain pending.

Record before deployment:

- Training/export date and model revision: PENDING.
- Actual class names and exported index order: PENDING.
- Training examples per class and session IDs: PENDING.
- Separate held-out capture session/content: PENDING.
- Crop coordinates and camera mounting geometry: PENDING.
- Export type, input tensor shape/dtype, normalization, channel order, quantization if applicable: PENDING.
- Preview errors and iteration changes: PENDING.
- Pi runtime/version and measured results: PENDING.

Match preprocessing to the exported model/runtime. Do not assume score scale or class order without inspecting actual output. Raw optical captures belong in ignored data folders; publish only deliberately selected evidence.
