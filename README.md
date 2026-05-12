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

A 4x4x4 interactive NeoPixel LED cube built on Arduino Uno with multiple animation modes, adaptive brightness via LDR and physical button controls.

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

- 64 addressable WS2812B LEDs in 4x4x4 layout
- Four built-in animations: Colour Wipe, Smooth RGB Fade, Fire Effect, Rainbow Cycle
- Auto brightness mapping with LDR sensor
- Real-time serial debug output
- Power and mode controls through physical buttons

## Tech Stack

| <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/arduino/arduino-original.svg" width="65" /> | <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/c/c-original.svg" width="65" /> | <img src="https://techstack-generator.vercel.app/cpp-icon.svg" width="65" /> | <img src="https://techstack-generator.vercel.app/python-icon.svg" width="65" /> | <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" width="65" /> | <img src="https://techstack-generator.vercel.app/github-icon.svg" width="65" /> | <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg" width="65" /> |
| :------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------: | :-----------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------: |
|                                               **Arduino**                                                |                                            **C**                                             |                                   **C++**                                    |                                   **Python**                                    |                                             **Git**                                              |                                   **GitHub**                                    |                                              **VS Code**                                               |

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
| Arduino IDE             | 2.x                      |
| Board                   | Arduino Uno (ATmega328P) |
| LED Type                | WS2812B                  |
| LED Count               | 64                       |
| Supply Used During Demo | 5V DC, 2A+               |
| Serial Baud             | 9600                     |

## Contact and Support

If you have questions, open an issue in this repository first.

You can also contact me directly at eng@isaacadjei.me.

<p align="center">
  <b>Project Status:</b> Completed<br>
  <b>Last Updated:</b> May 2026
</p>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer" />
</p>
