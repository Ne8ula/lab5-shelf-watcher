# Short-burst sample collection

This is a collection workflow, not a trained model or completed Part B/C/D evidence.
The course suggests over 150 samples per class. Collecting 200 is our convenience
target, not an additional course requirement.

Use the physical-monitor camera view. Direct computer screenshots or downloaded
video frames miss the viewing angle, glare, exposure, and surrounding scene the
camera will see. Existing videos can be used if they were filmed through that
camera. Keep its position and crop fixed across classes and eventual inference.

## Windows / Kiyo

The script uses the installed FFmpeg tools and records video only, without audio.
Close Teachable Machine's webcam preview or other apps using the Kiyo first.
Run from the repository root in PowerShell:

```powershell
.\scripts\Collect-Samples.ps1 -Label WORK -Scene editor
```

Each invocation gives a five-second countdown, then records eight seconds and extracts up to 40 images at five frames
per second. Five short bursts yield about 200 images, without taking individual
photos. Change the content between bursts; hundreds of identical neighboring
frames are not hundreds of independent examples.

| Class | Five suggested bursts, all filmed through the same camera |
| --- | --- |
| WORK | Code editor; document; spreadsheet; work webpage; different work layout |
| VIDEO | Different clips; different scenes; full-screen player; windowed player; another player layout |
| NEUTRAL | Desktop; different desktop background; blank page; display asleep; another intended neutral view |

Display only the intended class during each capture. Keep the collection tool on
another screen if available, or minimize it before capture begins. Do not film
the Teachable Machine training page as a work example unless that is deliberately
one of the desired appearances. Choose content you are comfortable retaining.

For a fixed monitor crop, add `-Crop 'width:height:x:y'` using pixel coordinates
from a camera preview. The script then scales to fit a 224x224 square and adds
black padding. These exact preprocessing steps must also be used at inference;
the final application is not yet implemented.

Raw silent videos and receipts go under ignored `data/raw/`. Upload-ready JPEGs
go under ignored `data/processed/train/<CLASS>/<SESSION>/`. Each receipt records
the source hash, class, scene, count, sampling rate, crop, and preprocessing.
Use the matching class's **Upload** control in Teachable Machine and select the
JPEGs. Save the Teachable Machine project after adding samples.

## Existing optical recordings

```powershell
.\scripts\Collect-Samples.ps1 -Label VIDEO -Scene player-clip `
  -SourceVideo 'C:\clips\camera-recording.mp4' -StartSeconds 3
```

Select a segment containing only that class. This extracts images; it does not
infer labels or establish that the supplied file originated from a webcam.

## Keep evaluation separate

After training collection, capture new content in a separate session with
`-Split test`. Never upload those frames into the training classes. If a failed
test is used for retraining, collect new held-out tests afterward.

- **Part B:** train and export the model, implement a response, and record the
  real integrated interaction. Training data alone does not complete Part B.
- **Part C:** run the working interaction on held-out content and difficult
  conditions; record actual errors, delays, and recovery using the test plan.
- **Part D:** narrate and demonstrate the observed strengths, limitations, and
  failure behavior. A montage of training images is not a characterization demo.

No samples, classifier accuracy, or hardware test results are claimed by this guide.
