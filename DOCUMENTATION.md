# Documentation: NeoPixel LED Cube

Full technical documentation for the NeoPixel LED Cube project. Covers hardware architecture, software design, build process, troubleshooting and future development notes.

> Back to [README.md](README.md) &nbsp;|&nbsp; [FAQ.md](FAQ.md) &nbsp;|&nbsp; [media/Gallery.md](media/Gallery.md)

---

## Table of Contents

- [1. Project Overview](#1-project-overview)
- [2. Repository Structure](#2-repository-structure)
- [3. Hardware Architecture](#3-hardware-architecture)
  - [3.1 Component List](#31-component-list)
  - [3.2 Pin Mapping](#32-pin-mapping)
  - [3.3 Electrical Notes](#33-electrical-notes)
- [4. Software Architecture](#4-software-architecture)
  - [4.1 Main Runtime Flow](#41-main-runtime-flow)
  - [4.2 Animation Modes](#42-animation-modes)
  - [4.3 Brightness Control](#43-brightness-control)
  - [4.4 Button Handling](#44-button-handling)
  - [4.5 Audio Feedback](#45-audio-feedback)
  - [4.6 Serial Diagnostics](#46-serial-diagnostics)
  - [4.7 Dependencies](#47-dependencies)
- [5. Build and Validation](#5-build-and-validation)
  - [5.1 Build Process](#51-build-process)
  - [5.2 Validation Checklist](#52-validation-checklist)
- [6. Troubleshooting Guide](#6-troubleshooting-guide)
  - [LEDs not responding](#leds-not-responding)
  - [Buttons inconsistent](#buttons-inconsistent)
  - [Brightness not changing](#brightness-not-changing)
  - [Animations look slow or frozen](#animations-look-slow-or-frozen)
  - [Upload fails in Arduino IDE](#upload-fails-in-arduino-ide)
- [7. Media and Related Docs](#7-media-and-related-docs)
- [8. Future Enhancements](#8-future-enhancements)
- [9. Licence](#9-licence)
- [10. Attribution](#10-attribution)

---

## 1. Project Overview

The NeoPixel LED Cube is an interactive 4x4x4 LED display system developed as part of an academic engineering assignment. The system combines a hand-soldered LED matrix with embedded firmware to produce a cube that runs multiple dynamic lighting patterns while automatically adjusting brightness based on ambient light levels.

The cube contains 64 individually addressable WS2812B LEDs arranged in four horizontal layers of 16 LEDs each. All LEDs are chained on a single data line controlled by an Arduino Uno. Physical buttons allow the user to toggle power and cycle through patterns without touching a computer after the initial upload.

The project demonstrates practical application of digital input handling, analog sensing, PWM-based LED control and real-time embedded firmware design.

---

## 2. Repository Structure

```
neopixel-led-cube/
├── README.md                       Project overview and quick start
├── DOCUMENTATION.md                Full technical reference (this file)
├── FAQ.md                          Frequently asked questions
├── CONTRIBUTING.md                 Contribution workflow and standards
├── LICENSE                         MIT licence
│
├── .github/
│   └── ISSUE_TEMPLATE/
│       ├── bug_report.md           Bug report issue template
│       └── docs_update.md          Documentation update issue template
│
├── docs/
│   ├── README.md                   Overview of project documents
│   ├── market-analysis.docx        Competitive market analysis
│   ├── finance-report.xlsx         Component cost and budget tracking
│   └── gantt-chart.xlsx            Project timeline and task plan
│
├── hardware/
│   ├── README.md                   Component list, wiring and circuit design
│   └── hardware-overview.pptx      Visual hardware presentation
│
├── media/
│   ├── README.md                   Media file catalog
│   ├── Gallery.md                  Build photos and embedded demo video
│   └── (image files)               Build and demo photos
│
└── software/
    ├── README.md                   Software architecture and function reference
    └── neopixel_cube/
        ├── README.md               Sketch-level documentation
        └── neopixel_cube.ino       Main Arduino sketch
```

---

## 3. Hardware Architecture

### 3.1 Component List

| Component              | Specification          | Quantity  | Purpose                      |
| ---------------------- | ---------------------- | --------- | ---------------------------- |
| Arduino Uno            | ATmega328P             | 1         | Main microcontroller         |
| WS2812B LEDs           | 5V addressable RGB     | 64        | LED cube matrix              |
| Power Button           | SPST momentary switch  | 1         | System power toggle          |
| Mode Button            | SPST momentary switch  | 1         | Pattern selection            |
| LDR Sensor             | Photoresistor 5-10kOhm | 1         | Ambient brightness detection |
| Resistor               | 10kOhm                 | 2         | Button pull-up resistors     |
| Resistor               | 10kOhm                 | 1         | LDR voltage divider          |
| Buzzer                 | 5V active buzzer       | 1         | Audio feedback               |
| Electrolytic Capacitor | 1000uF, 6.3V or higher | 1         | Power supply smoothing       |
| Breadboard             | Standard 830-point     | 1         | Component mounting           |
| Jumper Wires           | Male-to-male           | ~20       | Circuit connections          |
| Copper Wire            | 22-24 AWG solid core   | ~5 metres | LED cube structure           |
| Power Supply           | 5V DC, 2A minimum      | 1         | System power                 |
| Power Jack             | 2.1mm barrel connector | 1         | Power input                  |
| USB Cable              | Type A to Type B       | 1         | Programming and serial       |
| Enclosure              | Custom wooden box      | 1         | Housing and protection       |

### 3.2 Pin Mapping

| Arduino Pin | Component     | Mode           | Notes                                |
| ----------- | ------------- | -------------- | ------------------------------------ |
| D2          | Power Button  | Digital input  | Pull-up resistor to 5V, active LOW   |
| D3          | Mode Button   | Digital input  | Pull-up resistor to 5V, active LOW   |
| D4          | Buzzer        | Digital output | Active buzzer, HIGH triggers tone    |
| D6          | NeoPixel Data | Digital output | Single-wire data line, keep short    |
| A0          | LDR Sensor    | Analog input   | Voltage divider with 10kOhm resistor |

### 3.3 Electrical Notes

- Use a common ground between the Arduino and the LED power supply. Without shared ground the data signal will not be read correctly by the LEDs.
- Place the 1000uF electrolytic capacitor directly across the 5V and GND rails as close to the first LED in the chain as possible. This absorbs inrush current spikes that occur when many LEDs change state simultaneously.
- Keep the D6 data line as short as reasonably possible. Long or unshielded data lines can introduce signal degradation at higher refresh rates.
- The theoretical maximum current draw is approximately 3.8A when all 64 LEDs display full white (64 LEDs at 60mA each). Use a power supply rated at 5A or higher to maintain voltage stability with adequate headroom.
- During typical mixed-colour operation the draw is closer to 1.5 to 2A.
- Button pull-up resistors hold the input pin at a defined HIGH state when the button is not pressed, preventing floating input noise from triggering false events.

---

## 4. Software Architecture

### 4.1 Main Runtime Flow

The sketch uses a single-threaded loop with non-blocking timing. On every iteration the loop executes the following sequence:

1. Read power button state and compare to previous state to detect a press edge.
2. On power button press, toggle the system power flag and emit a beep.
3. If system is powered on, read mode button state and detect a press edge.
4. On mode button press, increment the pattern index and wrap at 4.
5. Read the LDR analog value from A0.
6. Map the LDR value to a brightness level and apply it to the LED strip.
7. Call the active animation function for one frame.
8. Transmit diagnostic values over serial.

All animation timing uses `millis()` comparisons rather than `delay()` calls. This allows button inputs to remain responsive during pattern execution without blocking the loop.

### 4.2 Animation Modes

The firmware includes four patterns selectable with the mode button.

**Mode 0: Colour Wipe**

Illuminates LEDs one by one from index 0 to 63 in a single solid colour. The wipe runs in red then green then blue before repeating. A 50ms interval between LED updates creates a visible wave that travels across the cube. This mode is useful for verifying individual LED function and solder joint continuity because each LED lights independently in sequence.

**Mode 1: Smooth RGB Fade**

All 64 LEDs simultaneously fade through the full red, green and blue spectrum in sync. The colour value increments on each loop cycle and wraps at 255, producing a continuous ambient glow. The fade rate can be adjusted by changing the step size in the sketch.

**Mode 2: Fire Effect**

Simulates a flame using a heat diffusion algorithm. Each LED holds a heat value that determines its colour. On every frame the algorithm runs three stages:

1. Cooling: each LED heat value decreases by a small random amount to simulate heat loss.
2. Heat diffusion: heat propagates upward from lower layers to higher ones so the base of the cube stays hotter.
3. Sparking: random ignition events at the lowest layer inject new heat to sustain the effect.

The colour mapping translates heat values from black (cold) through red and orange to white (maximum heat), producing a realistic flame appearance. The `Cooling` and `Sparking` constants in the sketch control flame intensity and can be tuned to produce a larger or smaller fire appearance.

**Mode 3: Rainbow Cycle**

Distributes a full HSV rainbow gradient evenly across all 64 LEDs at once. A starting hue offset increments on each frame causing the entire rainbow to rotate continuously around the cube. The `wheel()` helper function converts a 0-255 hue input to a smooth RGB colour output.

### 4.3 Brightness Control

The LDR reads ambient light as an analog value between 0 and 1023. The firmware maps this inversely to LED brightness using the Arduino `map()` function:

- LDR 0 (very dark room) maps to brightness 255 (maximum output)
- LDR 1023 (very bright room) maps to brightness 20 (minimum visible output)

The minimum threshold of 20 ensures the LEDs are never fully off, keeping the cube visible in all conditions. The `setBrightness()` call from the Adafruit NeoPixel library applies the value globally to all LEDs on the next `show()` call.

### 4.4 Button Handling

Both buttons use software debouncing with rising-edge detection. On each loop iteration the firmware reads the current pin state and compares it to the last stored state. A transition from HIGH to LOW (button pressed with pull-up active) triggers the action for that button. A 200ms debounce window prevents multiple triggers from a single physical press.

The power button is active at all times. The mode button only responds when the system power state is on, preventing accidental pattern changes while the cube appears off.

### 4.5 Audio Feedback

A 5V active buzzer on pin D4 confirms power state changes. The `beep()` function sets D4 HIGH for 100ms then LOW. On power-on a single beep plays. On power-off two short beeps play with a 50ms gap between them, making the two states audibly distinct.

### 4.6 Serial Diagnostics

The sketch transmits status information over serial at 9600 baud. Output is sent on significant state changes and includes:

- Power state change messages (System ON / System OFF)
- Active animation name when the mode changes
- Raw LDR sensor value on every loop iteration
- Calculated brightness value on every loop iteration

Connect Serial Monitor in Arduino IDE at 9600 baud to observe live readings during operation. This output is essential for diagnosing brightness issues and verifying button response.

### 4.7 Dependencies

| Library           | Source                  | Purpose             |
| ----------------- | ----------------------- | ------------------- |
| Adafruit NeoPixel | Arduino Library Manager | WS2812B LED control |

Install via Arduino IDE: **Tools > Manage Libraries**, search for "Adafruit NeoPixel" and install the latest version.

---

## 5. Build and Validation

### 5.1 Build Process

1. Cut 64 equal-length copper wire segments for the LED structural legs.
2. Solder LEDs into a 4x4 grid for layer 1, verifying polarity and data chain direction before soldering each LED.
3. Power layer 1 alone and run a basic test sketch to confirm all 16 LEDs respond before moving on.
4. Repeat the solder and test process for layers 2, 3 and 4.
5. Connect the data-out pad of each layer to the data-in pad of the next to form a single continuous chain of 64 LEDs.
6. Mount the breadboard and Arduino inside the enclosure base.
7. Wire the power button to D2 with a 10kOhm pull-up resistor to 5V.
8. Wire the mode button to D3 with a 10kOhm pull-up resistor to 5V.
9. Wire the buzzer positive terminal to D4 and negative to GND.
10. Connect the NeoPixel data-in line to D6 using a short direct wire.
11. Wire the LDR in a voltage divider with a 10kOhm resistor to A0.
12. Place the 1000uF capacitor across the 5V and GND rails close to the first LED.
13. Connect the 5V power supply to the LED power rail and to the Arduino barrel jack.
14. Upload the sketch and verify all four animation modes work on all layers before closing the enclosure.

### 5.2 Validation Checklist

- [x] Power button toggles system state correctly
- [x] Mode button cycles all four patterns in order
- [x] LDR changes brightness in real time as ambient light changes
- [x] Serial output reports power state, active pattern and brightness values
- [x] All 64 LEDs respond to all four animation modes
- [x] Buzzer beeps on power-on and double-beeps on power-off
- [x] No flickering or data corruption observed at the start of any LED layer

---

## 6. Troubleshooting Guide

### LEDs not responding

- Verify 5V and GND wiring from the power supply to the LED rail.
- Confirm shared ground between the Arduino and the LED power supply.
- Check the D6 data line connection to the data-in pad of the first LED in the chain.
- Confirm the Adafruit NeoPixel library is installed and the correct LED count and pin number are set in the sketch.
- Reduce LED count to 1 in the sketch and test a single LED in isolation to identify whether the issue is wiring or firmware.

### Buttons inconsistent

- Check pull-up resistor wiring on D2 and D3.
- Verify the button connects the pin to GND when pressed (active LOW with pull-up).
- Increase the debounce delay constant in the sketch if double-triggers persist.
- Replace the physical button if contacts are worn or corroded.

### Brightness not changing

- Verify the LDR is wired in a voltage divider configuration with a 10kOhm resistor to A0.
- Open Serial Monitor at 9600 baud and observe the raw LDR value while covering and exposing the sensor. The value should change across a wide range between roughly 0 and 1023.
- If the value is stuck at 0 or 1023 the wiring polarity or resistor placement is likely incorrect.
- Check that `setBrightness()` is called before `show()` in the sketch.

### Animations look slow or frozen

- Confirm the sketch does not use `delay()` inside any animation function. All timing should use `millis()` comparisons.
- Check for a missing `break` statement in the pattern `switch` block that could cause multiple patterns to execute simultaneously.
- If the loop appears stuck, open Serial Monitor and check whether diagnostic output is still flowing.

### Upload fails in Arduino IDE

- Confirm the correct board is selected: **Tools > Board > Arduino Uno**.
- Confirm the correct COM port is selected: **Tools > Port**.
- Disconnect any wires from D0 or D1 (TX/RX pins) during upload as these share the hardware serial programmer lines.
- Try a different USB cable or USB port if the board is not detected at all.

---

## 7. Media and Related Docs

- Build photos and demo video: [media/Gallery.md](media/Gallery.md)
- Media file catalog: [media/README.md](media/README.md)
- Hardware component and wiring guide: [hardware/README.md](hardware/README.md)
- Software architecture and function reference: [software/README.md](software/README.md)
- Project documents (Gantt chart, finance report, market analysis): [docs/README.md](docs/README.md)
- FAQ: [FAQ.md](FAQ.md)

---

## 8. Future Enhancements

- Wireless control via BLE or Wi-Fi for remote pattern selection and brightness override
- Audio-reactive patterns driven by a microphone or line-in sensor
- Extended 3D animation library with more complex volumetric effects
- Companion mobile app for real-time control without a serial connection
- OTA firmware update support for wireless deployments

---

## 9. Licence

> [!NOTE]
> This project is dual-licensed. The written and visual content is released under CC BY-NC-ND 4.0. The Arduino sketch under `software/neopixel_cube/` is released under the MIT Licence. See [LICENSE](LICENSE) and [NOTICE.md](NOTICE.md) for the full terms.

---

## 10. Attribution

> [!NOTE]
> Lead Developer: Isaac "Zac" Adjei
>
> Team: NeoPixel Innovators
>
> Repository: [github.com/zaccesss/neopixel-led-cube](https://github.com/zaccesss/neopixel-led-cube)

Last Updated: August 2026
