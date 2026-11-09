# A3 evidence — Moondream

I ran this experiment on November 9, 2026, using Ollama on the Raspberry Pi in CPU-only mode. The three terminal screenshots show a timed rerun of the course demo. My setup photo shows a mug on the left, a ceramic teapot near the center, and a black computer mouse on the right, with the webcam facing them against a dark backdrop.

[My observations and interaction idea](../../README.md#a3-moondream)

## Image files

| File | Content | Dimensions |
|---|---|---|
| [Setup photo](setup.png) | External view of the webcam and three objects | 1368 × 1824 |
| [Request 1](request-1-description.png) | Capture sequence, description, and 237.971-second timing | 1102 × 559 |
| [Request 2](request-2-objects.png) | Object-list question, answer, and 27.407-second timing | 1099 × 322 |
| [Request 3](request-3-urn.png) | Handle-and-spout question, “urn” answer, and 3.628-second timing | 1046 × 297 |

These PNG files were recovered from the four supplied conversation attachments without further image editing or re-encoding. The setup photo is the chat-resized 1368 × 1824 version of the supplied 2160 × 2880 photo. All four are embedded in the main README.

## Questions, answers, and timing

The following is a manual transcription of the supplied screenshots, with terminal line wrapping removed. It is not an exported terminal log. All three requests used the same `captured_image.jpg`.

| Request | Start shown in terminal | Elapsed time | Outcome |
|---|---|---|---|
| 1 | `2026-11-09T14:06:46-05:00` | 237.971 seconds | Description returned |
| 2 | `2026-11-09T14:10:56-05:00` | 27.407 seconds | Object list returned |
| 3 | `2026-11-09T14:11:29-05:00` | 3.628 seconds | Incorrect “urn” answer returned |

**Request 1:** What do you see in this image? Describe it.

```text
The image features a teapot and a computer mouse placed on a table. The teapot is a pink color and has a floral design on it. It is positioned on the left side of the table, while the computer mouse is located on the right side. The table appears to be made of wood, and the background is black, providing a contrast to the objects on the table.
```

**Request 2:** What objects are visible in this image?

```text
In the image, there is a teapot and a computer mouse sitting on a table. The teapot is pink and has a flower design on it, while the computer mouse is black. The objects are placed next to each other, creating a visually interesting scene.
```

**Request 3:** Which object has a handle and a spout?

```text
urn
```

All three screenshots report `ANSWER RETURNED`. The last screenshot shows `quit` followed by `Done!`.

## Measurement and evidence details

- The launch command shown is `python -u moondream_timed.py`, recorded with the Linux `script` command. The timing wrapper calls the original course demo and measures each `ask_moondream` call with `time.perf_counter()`.
- Elapsed times include image encoding, the Ollama request, model processing/loading if any, and receiving and printing the answer. They exclude camera capture and the user's typing time. They are not isolated inference benchmarks.
- This was a rerun. Model residency/loading was not measured, and prompts and response lengths differed; these three times do not establish a controlled cold-versus-warm comparison.
- The script sends each question and the same image independently, without previous answers as conversation history.
- The visible Pi directory is `/home/ne8ula/lab5-a3-evidence/run-20261109-133330-JhV5YK`, and the shell shows the `.venv-a1` environment active.
- The setup photo is an external view of the arrangement, not the webcam's saved input image. Both descriptions omit the mug visible in that photo, but the exact webcam framing cannot be checked from the supplied evidence. The photo also shows a cream/brown teapot and a dark covered surface, unlike the pink teapot and wooden table in the generated description.
- The three terminal screenshots and setup photo are included in this directory. The Pi's `captured_image.jpg`, raw terminal log, and A3 environment file are not included; the transcription above is based on the screenshots.

Course reference: [moondream_simple.py](https://github.com/IRL-CT/Interactive-Lab-Hub/blob/9ef02d4ead28bafc0a803116a6a952f3908b7463/Lab%205/moondream_simple.py).
