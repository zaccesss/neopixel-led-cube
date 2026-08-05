# NeoPixel LED Cube

<p align="center">
  <a href="https://isaacadjei.me">
    <img src="https://img.shields.io/badge/Website-isaacadjei.me-111111?style=for-the-badge&logo=firefox&logoColor=white">
  </a>
  <a href="https://www.linkedin.com/in/isaacadjei">
    <img src="https://img.shields.io/badge/LinkedIn-Isaac_Adjei-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white">
  </a>
  <a href="mailto:eng@isaacadjei.me">
    <img src="https://img.shields.io/badge/Email-Contact-ff6f61?style=for-the-badge&logo=gmail&logoColor=white">
  </a>
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge">
</p>

I built this 4x4x4 NeoPixel LED cube on an Arduino Uno as an academic engineering project. It runs four animated lighting patterns, adapts its brightness to ambient light through an LDR sensor and responds to two physical buttons for power and pattern control.

<h2 align="center">Project Walkthrough</h2>

<p align="center"><em>Click the video below to watch the full demo.</em></p>

https://github.com/user-attachments/assets/58bd4d04-e2ed-466e-9ed1-12fc8279b9ec

## Quick Start

1. Build the wiring setup described in [hardware/README.md](hardware/README.md).
2. Install Adafruit NeoPixel in Arduino IDE through Library Manager.
3. Open [software/neopixel_cube/neopixel_cube.ino](software/neopixel_cube/neopixel_cube.ino).
4. Select Arduino Uno and the correct COM port.
5. Upload and open Serial Monitor at 9600 baud.

## Core Features

- 64 addressable WS2812B LEDs in a 4x4x4 layout
- Four built-in animations: Colour Wipe, Smooth RGB Fade, Fire Effect and Rainbow Cycle
- Auto brightness mapping with an LDR sensor
- Real-time serial debug output
- Power and mode controls through physical buttons

## Tech Stack

<p align="center">
  <img src="https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white">
  <img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white">
  <img src="https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=white">
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white">
  <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white">
  <img src="https://img.shields.io/badge/VS_Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white">
</p>

## Documentation Hub

<p align="center">
  <a href="DOCUMENTATION.md">📖 Documentation</a> &nbsp;•&nbsp;
  <a href="FAQ.md">❓ FAQ</a> &nbsp;•&nbsp;
  <a href="hardware/README.md">🔧 Hardware Guide</a> &nbsp;•&nbsp;
  <a href="software/README.md">💻 Software Guide</a> &nbsp;•&nbsp;
  <a href="media/Gallery.md">🖼️ Gallery</a> &nbsp;•&nbsp;
  <a href="CONTRIBUTING.md">🤝 Contributing</a>
</p>

## Tested Environment

| Item                    | Tested Value             |
| ----------------------- | ------------------------ |
| Arduino IDE              | 2.x                       |
| Board                    | Arduino Uno (ATmega328P)  |
| LED Type                 | WS2812B                   |
| LED Count                | 64                        |
| Supply Used During Demo  | 5V DC, 2A+                |
| Serial Baud              | 9600                      |

## Contact and Support

If you have questions, I encourage you to open an issue in this repository first. You can also reach me directly at eng@isaacadjei.me.
