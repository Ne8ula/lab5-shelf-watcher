# Hardware, cables, tools, and software

Inventory confirmed by Hao Chen Xiong in planning conversation; operation has not been tested.

| Item | Inventory | Use / remaining check |
|---|---|---|
| Raspberry Pi 4 and kit | Have | OS, architecture, Python, kit power/cooling/storage pending |
| EH-1080P6 USB webcam, DC 5V label | Have | Check Linux capture and shelf image quality; model label alone is not compatibility proof |
| Speaker | Have | Confirm USB audio versus AUX plus separate power |
| Adafruit miniPiTFT, 240×135 label | Have | Consistent with 1.14-inch model; verify board/connector before wiring |
| SparkFun 0.91-inch OLED V1.0 | Have | Spare, excluded from initial build |
| Zio 16 Servo Controller V1 | Have | Optional future motion, excluded initially |
| Miuzei MS18 9g servo | Have | Optional future motion, excluded initially |
| 3D printer access | Available | Dimensions, CAD, fit check, and full print pending |
| Laptop/desktop, monitor, network | Needed | VNC, training, and screen under observation |
| Phone/camera with microphone | Needed | Record voice and physical demonstrations |
| Mug, bottle, book, other objects | Needed | PyTorch examples |

## Cables and connectors

| Item | Need |
|---|---|
| Suitable Pi 4 USB-C power supply | Required; verify kit supply |
| Webcam USB lead | Required; usually attached to webcam |
| Speaker USB audio or 3.5mm AUX lead | Required according to speaker interface |
| Speaker power lead/adapter | Required if separate; USB power alone does not imply USB audio |
| 40-pin 2×20 male-to-female GPIO extension | For remote display in robot; purchase not confirmed |
| 2×20 plug-in socket riser | Conditional: connector clearance; approximately 6mm exposed pins on Adafruit #4079 |
| USB extension | Optional if shelf distance requires it |
| Micro-HDMI to HDMI and local input devices | Optional if not using VNC |
| Ethernet | Optional alternative to Wi-Fi |

Candidate extension: UCTRONICS 40-pin male-to-female 8-inch cable. Selection is based on its stated type, not physical verification. Avoid substituting short solder-tail PCB headers for a plug-in riser. No breakout breadboard is required. Adafruit alternatives: [extension #4823](https://www.adafruit.com/product/4823), [riser #4079](https://www.adafruit.com/product/4079).

The miniPiTFT uses a 2×12 female socket aligned to physical pins 1–24 at the pin-1 end of the Pi's 2×20 header. It is not centered. Its Qwiic/STEMMA QT socket is for I²C accessories, not the primary display connection. Consult the [manufacturer pinout](https://learn.adafruit.com/adafruit-mini-pitft-135x240-color-tft-add-on-for-raspberry-pi/pinouts), and disconnect power before GPIO changes. The enclosure must support the display mechanically rather than hanging its weight from the cable.

## Assembly

PLA, ruler/digital calipers, small screwdriver, mounting screws/spacers chosen after measurement, removable mounting tape, nonslip feet, cable ties, and optional file/cutters for print cleanup. Cardboard is useful for the first layout mockup. No soldering is expected if the display connector is already fitted. Measure lens position and full webcam housing; do not design from the model name alone. Separate the face direction from the camera direction. Keep ventilation and button access clear.

## Software

Python/venv/pip; Git; VNC; OpenCV; PyTorch/torchvision; MediaPipe; Teachable Machine browser training and TFLite runtime via the lab wrapper; Ollama/Moondream; `requests`; `aplay`/`pactl`; Adafruit Blinka/RGB display/Pillow for the face. Start with the [upstream requirement reference](../requirements.upstream.txt). It is not a tested lockfile for this machine. Exact working versions will be recorded after installation. No paid AI API is part of this design.
