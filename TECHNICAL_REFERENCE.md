# Technical Reference — NeoPixel LED Cube

Full technical documentation for the NeoPixel LED Cube project. Covers hardware architecture, software design, build validation, troubleshooting and future development notes.

> Back to [README.md](README.md) &nbsp;|&nbsp; [FAQ.md](FAQ.md) &nbsp;|&nbsp; [media/Gallery.md](media/Gallery.md)

---

## Table of Contents

- [1. Project Overview](#1-project-overview)
- [2. Hardware Architecture](#2-hardware-architecture)
  - [2.1 Component List](#21-component-list)
  - [2.2 Pin Mapping](#22-pin-mapping)
  - [2.3 Electrical Notes](#23-electrical-notes)
- [3. Software Architecture](#3-software-architecture)
  - [3.1 Main Runtime Flow](#31-main-runtime-flow)
  - [3.2 Implemented Animation Modes](#32-implemented-animation-modes)
  - [3.3 Brightness Control](#33-brightness-control)
  - [3.4 Dependencies](#34-dependencies)
- [4. Build and Validation](#4-build-and-validation)
  - [4.1 Build Process Summary](#41-build-process-summary)
  - [4.2 Validation Checklist](#42-validation-checklist)
- [5. Troubleshooting Guide](#5-troubleshooting-guide)
  - [LEDs not responding](#leds-not-responding)
  - [Buttons inconsistent](#buttons-inconsistent)
  - [Brightness not changing](#brightness-not-changing)
- [6. Media and Related Docs](#6-media-and-related-docs)
- [7. Future Enhancements](#7-future-enhancements)
- [8. License](#8-license)
- [9. Attribution](#9-attribution)
- [10. Last Updated](#10-last-updated)

---

## 1. Project Overview

The NeoPixel LED Cube Project is an interactive 4x4x4 LED display system developed as part of an academic engineering assignment. This adaptive lighting system combines hardware assembly with embedded software to create a functional LED cube that displays multiple dynamic patterns while automatically adjusting brightness based on ambient light.

The system demonstrates practical applications of digital input handling, analog sensing, PWM-based LED control and real-time embedded logic.

## 2. Hardware Architecture

### 2.1 Component List

| Component              | Specification            | Quantity | Purpose                      |
| ---------------------- | ------------------------ | -------- | ---------------------------- |
| Arduino Uno            | ATmega328P               | 1        | Main microcontroller         |
| WS2812B LEDs           | 5V addressable RGB       | 64       | LED cube matrix              |
| Power Button           | Digital momentary switch | 1        | System power toggle          |
| Mode Button            | Digital momentary switch | 1        | Pattern selection            |
| LDR Sensor             | Analog light sensor      | 1        | Ambient brightness detection |
| Buzzer                 | 5V active buzzer         | 1        | Audio feedback               |
| Electrolytic Capacitor | 1000uF, 6.3V+            | 1        | Power supply smoothing       |
| Breadboard             | Standard size            | 1        | Component mounting           |
| Power Supply           | 5V, 2A+                  | 1        | System power                 |
| Enclosure              | Custom wooden box        | 1        | Housing and protection       |

### 2.2 Pin Mapping

| Arduino Pin | Component     | Function        |
| ----------- | ------------- | --------------- |
| D2          | Power Button  | Digital input   |
| D3          | Mode Button   | Digital input   |
| D4          | Buzzer        | Digital output  |
| D6          | NeoPixel Data | LED data output |
| A0          | LDR Sensor    | Analog input    |

### 2.3 Electrical Notes

- Use a common ground between Arduino and LED power supply.
- Keep NeoPixel data line short for signal stability.
- Use a 1000uF capacitor on 5V rail to reduce voltage spikes.
- Confirm PSU can handle peak current demand from the LED array.

## 3. Software Architecture

### 3.1 Main Runtime Flow

1. Initialize LED strip and peripherals in setup.
2. Read button states with debounce logic.
3. Toggle system power and cycle pattern mode based on input.
4. Read LDR value and map to LED brightness.
5. Execute active pattern loop.
6. Print diagnostics to Serial Monitor.

### 3.2 Implemented Animation Modes

- Mode 0: Colour Wipe
- Mode 1: Smooth RGB Fade
- Mode 2: Fire Effect
- Mode 3: Rainbow Cycle

### 3.3 Brightness Control

- Sensor range: 0 to 1023
- Brightness range: 20 to 255
- Mapping: inverse relationship between ambient light and LED brightness

### 3.4 Dependencies

- Adafruit NeoPixel library

## 4. Build and Validation

### 4.1 Build Process Summary

- Constructed the 4x4x4 matrix layer by layer.
- Verified LED continuity during each stage.
- Integrated components into an enclosure.
- Tested input handling, brightness adaptation and all patterns.

### 4.2 Validation Checklist

- [x] Power button toggles state correctly
- [x] Mode button cycles all patterns
- [x] LDR changes brightness in real time
- [x] Serial output reports sensor and state values
- [x] All 64 LEDs respond correctly

## 5. Troubleshooting Guide

### LEDs not responding

- Verify 5V power and ground continuity.
- Check D6 data line routing to first LED.
- Confirm NeoPixel library installation.

### Buttons inconsistent

- Recheck wiring and pull-up/pull-down behavior.
- Adjust debounce delay if needed.

### Brightness not changing

- Verify LDR wiring to A0.
- Confirm mapped brightness values in serial output.

## 6. Media and Related Docs

- Visual gallery: [media/Gallery.md](media/Gallery.md)
- Media catalog: [media/README.md](media/README.md)
- Hardware details: [hardware/README.md](hardware/README.md)
- Software details: [software/README.md](software/README.md)
- FAQ: [FAQ.md](FAQ.md)

## 7. Future Enhancements

- Wireless control via BLE or Wi-Fi
- Audio-reactive patterns
- Extended 3D animation library
- Companion mobile control app
- Additional thermal and reliability monitoring

## 8. License

This project is released under the MIT License. See [LICENSE.md](LICENSE.md).

## 9. Attribution

Lead Developer: Isaac Zac Adjei

Team: NeoPixel Innovators

Repository: https://github.com/zaccesss/neopixel-led-cube

## 10. Last Updated

May 2026
